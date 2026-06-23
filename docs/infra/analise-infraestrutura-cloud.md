# Análise de Infraestrutura — e-engineer

## 1. Resumo Executivo

- O projeto está pronto para um staging simples, mas ainda precisa de pequenos ajustes antes de uma publicação estável.
- A melhor opção equilibrada para agora é: frontend estático em Vercel/Netlify + backend e Postgres em Railway/Render, com S3 real quando uploads/downloads precisarem funcionar de ponta a ponta.
- A alternativa mais barata e controlável é um VPS único com Docker Compose, mas exige mais operação manual: SSL, backups, updates, segurança e rollback.
- O maior bloqueio técnico antes do staging é o CORS hardcoded para localhost no backend.
- O segundo ponto crítico é upload/download: o backend tem upload para S3, mas o frontend hoje tende a abrir caminhos `s3://...`, que não são URLs navegáveis.
- Para validar com Lucas, Gabriel e Leonardo, dá para subir um staging barato, separado da produção, com banco próprio e dados fake/controlados.

## 2. Estrutura Detectada do Projeto

- Monorepo funcional com dois projetos principais:
  - `e-engineer-backend`
  - `e-engineer-frontend`
- Há `docker-compose.yml` na raiz para ambiente local/dev.
- Backend e frontend têm `package.json`, `.env.example` e Dockerfile próprios.
- Documentação relevante existe em:
  - `master.md`
  - `docs/API-CONTRACTS.md`
  - `README-CODEX-PROMPT.md`
  - `e-engineer-backend/docs/codex.md`
  - `e-engineer-frontend/codex.md`

## 3. Backend

| Item | Encontrado | Impacto |
| --- | --- | --- |
| Framework | NestJS 11 | Bom para deploy em container/PaaS |
| Runtime | Node `>=24` | Melhor usar Dockerfile para garantir versão |
| Porta | `APP_PORT` ou `PORT`, default `3000` | Simples expor atrás de HTTPS |
| Healthcheck | `GET /health` | Bom para Railway/Render/VPS |
| Banco | PostgreSQL via TypeORM | Precisa Postgres separado no staging |
| Auth | JWT Bearer | Sem cookies; CORS precisa estar correto |
| CORS | Hardcoded para `localhost:5173/5174` | Precisa ajuste antes do staging |
| Upload | S3 manual via `fetch` | Precisa bucket real ou ajuste |
| Workers/Redis/Cron | Não detectado | Infra mais simples |
| WebSocket | `VITE_WS_URL` existe, mas não há uso real detectado | Não precisa provisionar agora |
| Logs | Console/Nest padrão | Suficiente para staging inicial |

Backend principal:

- `e-engineer-backend/src/main.ts`
- `e-engineer-backend/src/app.module.ts`
- `e-engineer-backend/src/shared/infrastructure/config/env.validation.ts`
- `e-engineer-backend/src/shared/infrastructure/database/typeorm.config.ts`

## 4. Frontend

| Item | Encontrado | Impacto |
| --- | --- | --- |
| Framework | Vue 3 + Vite | SPA moderna |
| UI | Vuetify | Identidade visual centralizada |
| Estado | Pinia | Estado no frontend |
| HTTP | Axios | Consome API via `VITE_API_URL` |
| Build | SPA estática | Pode hospedar em CDN/static hosting |
| Runtime após build | Não precisa Node | Reduz custo |
| API env | `VITE_API_URL` | Precisa apontar para API staging |
| Router | History mode | Host precisa fallback para `index.html` |

O frontend é ideal para hospedagem estática em Vercel, Netlify, Render Static Site ou Nginx/Caddy num VPS.

Arquivos relevantes:

- `e-engineer-frontend/package.json`
- `e-engineer-frontend/vite.config.ts`
- `e-engineer-frontend/src/shared/http/http-client.ts`
- `e-engineer-frontend/src/router/index.ts`

## 5. Banco de Dados

- Banco esperado: PostgreSQL.
- O projeto usa variáveis separadas:
  - `DB_HOST`
  - `DB_PORT`
  - `DB_USERNAME`
  - `DB_PASSWORD`
  - `DB_DATABASE`
- Não foi detectado suporte atual a `DATABASE_URL`.
- Não foi detectado suporte explícito a SSL de banco, como `DB_SSL=true`.
- Há migrations em `e-engineer-backend/src/database/migrations`.
- Há seed em `e-engineer-backend/src/database/seeds/seed.ts`.

Cuidados:

- Em staging, usar banco separado.
- Não usar `DB_SYNCHRONIZE=true`.
- Preferir migrations.
- Rodar seed apenas de forma controlada, não em todo boot.
- Se o Postgres gerenciado exigir SSL, será necessário pequeno ajuste no backend.

## 6. Uploads e Arquivos

O backend tem suporte a upload de documentos via endpoints como:

- `POST /documents/:id/versions`
- `POST /documents/:id/upload`

Também há upload de assets de organização.

Ponto crítico:

- Se as variáveis de S3 não estiverem configuradas, o backend retorna caminhos tipo `s3://local-documents/...`, mas não persiste arquivo real.
- Mesmo com S3 real, o frontend hoje tende a abrir `latestVersion.filePath`.
- Se `filePath` for `s3://bucket/key`, o navegador não consegue baixar diretamente.

Antes de validar upload/download real, recomenda-se:

- Criar endpoint de download/presigned URL; ou
- Salvar URL HTTPS assinada/baixável; ou
- Ajustar frontend para pedir uma URL de download ao backend.

Para staging inicial sem foco em download, dá para validar cadastro/metadados de documentos, mas não é ideal.

## 7. Autenticação

- Login via `POST /auth/login`.
- JWT salvo no frontend e enviado como `Authorization: Bearer`.
- Existe refresh de token.
- JWT carrega:
  - `sub`
  - `organizationId`
  - `roles`
  - `isPlatformAdmin`
  - campos de impersonation/actor.

Risco para produção futura:

- O refresh parece aceitar token expirado desde que a assinatura seja válida.
- Para staging interno, isso é aceitável.
- Para produção, vale revisar estratégia de refresh token, expiração e revogação.

## 8. Multi-tenancy

- O backend usa `organizationId` no JWT e nos fluxos.
- Controllers e use cases usam `request.user.organizationId`.
- Tabelas e entidades possuem `organization_id`.
- Isso é positivo para staging multiusuário.

Cuidados:

- Nunca compartilhar banco de staging com produção.
- Criar tenant demo específico.
- Validar seeds/usuários: Lucas e Leonardo aparecem no seed, mas Gabriel precisa ser confirmado/criado.

## 9. Variáveis de Ambiente

### Backend atuais

| Variável | Obrigatória | Observação |
| --- | ---: | --- |
| `NODE_ENV` | Sim | `development`, `test` ou `production` |
| `PORT` / `APP_PORT` | Sim | Porta HTTP |
| `DB_HOST` | Sim | Host Postgres |
| `DB_PORT` | Sim | Porta Postgres |
| `DB_USERNAME` | Sim | Usuário Postgres |
| `DB_PASSWORD` | Sim | Senha Postgres |
| `DB_DATABASE` | Sim | Database |
| `DB_SYNCHRONIZE` | Sim | Usar `false` |
| `DB_LOGGING` | Sim | Usar `false` em staging |
| `DB_MIGRATIONS_RUN` | Sim | Pode ser `false` e rodar job separado |
| `JWT_SECRET` | Sim | Gerar segredo forte |
| `JWT_EXPIRES_IN` | Sim | Exemplo: `24h` |
| `AWS_REGION` | Opcional | Necessário para S3 real |
| `AWS_S3_BUCKET` | Opcional | Necessário para S3 real |
| `AWS_ACCESS_KEY_ID` | Opcional | Necessário para S3 real |
| `AWS_SECRET_ACCESS_KEY` | Opcional | Necessário para S3 real |

### Recomendações de novas variáveis

| Variável | Motivo |
| --- | --- |
| `CORS_ORIGINS` | Remover localhost hardcoded |
| `FRONTEND_URL` | Links públicos e CORS |
| `DB_SSL` | Postgres gerenciado com SSL |
| `API_PUBLIC_URL` | URLs públicas |
| `S3_PUBLIC_DOWNLOAD_MODE` ou endpoint de download | Resolver acesso a arquivos |

### Frontend

| Variável | Observação |
| --- | --- |
| `VITE_API_URL` | Obrigatória |
| `VITE_WS_URL` | Existe, mas parece não usada agora |

## 10. Scripts e Comandos

### Backend

- Instalação: `npm ci`
- Desenvolvimento: `npm run start:dev`
- Build: `npm run build`
- Produção: `npm run start:prod`
- Typecheck: `npm run type-check`
- Testes: `npm run test`
- Migração: `npm run db:migration:run`
- Seed: `npm run db:seed`

### Frontend

- Instalação: `npm ci`
- Desenvolvimento: `npm run dev`
- Build: `npm run build`
- Preview: `npm run preview`
- Typecheck: `npm run type-check`
- Testes: `npm run test:unit`

## 11. Docker / Containerização

O `docker-compose.yml` atual é ótimo para desenvolvimento local, mas não é produção.

Ele sobe:

- Postgres
- Backend em modo dev
- Frontend em modo dev

Problemas para staging/produção:

- Backend roda `start:dev`.
- Frontend roda Vite dev server.
- Seed roda automaticamente no comando do backend.
- Não há reverse proxy/HTTPS.
- Não há backup configurado.
- Não há estratégia de frontend estático.

Dockerfiles:

- Backend tem Dockerfile multi-stage mais próximo de produção.
- Frontend Dockerfile atual é dev; para produção seria melhor usar host estático ou criar build com Nginx/Caddy.

## 12. Necessidades Reais do Staging

Para Lucas, Gabriel e Leonardo testarem:

Obrigatório:

- URL HTTPS pública.
- Frontend estático.
- API pública protegida por JWT.
- Banco Postgres separado.
- Migrations aplicadas.
- Usuários demo.
- CORS liberando a URL do frontend.
- Logs básicos.
- Backup simples ou snapshot.

Opcional no primeiro corte:

- Domínio próprio.
- S3 real.
- Download real de documentos.
- CI/CD completo.
- Observabilidade avançada.
- Redis/filas/workers.

## 13. Comparativo de Estratégias Cloud

| Opção | Custo | Setup | Manutenção | Segurança | Melhor uso |
| --- | ---: | ---: | ---: | ---: | --- |
| VPS + Docker Compose | Baixo | Médio | Médio/alto | Depende de você | Staging barato com controle |
| Vercel/Netlify + Railway/Render | Baixo/médio | Baixo | Baixo | Boa | Melhor staging rápido |
| AWS mínimo | Médio/alto | Alto | Médio | Excelente | Produção futura |
| Render/Railway full stack | Baixo/médio | Baixo | Baixo | Boa | MVP/staging simples |
| Local tunnel | Quase zero | Baixo | Alto risco | Fraca | Demo temporária de horas |

## 14. Recomendação Principal

Minha recomendação principal para agora:

- Frontend: Vercel ou Netlify.
- Backend: Railway ou Render usando Dockerfile do backend.
- Banco: Postgres gerenciado na mesma plataforma do backend.
- Arquivos: AWS S3 quando upload/download real for prioridade.
- URL temporária:
  - Frontend: `https://e-engineer-staging.vercel.app`
  - API: `https://e-engineer-api-staging.up.railway.app`

Por quê:

- Menor fricção.
- Não exige administrar servidor.
- Tem HTTPS automático.
- Tem logs.
- Tem deploy mais simples.
- Escala melhor que um túnel/local.
- Evita overengineering de AWS nesse momento.

## 15. Recomendação Alternativa Barata

Alternativa barata e previsível:

- VPS: AWS Lightsail, Hetzner ou similar.
- Stack: Caddy/Nginx + backend Node + frontend estático + Postgres em container.
- Custo provável: baixo, mas com mais trabalho operacional.
- URL: `https://staging.seudominio.com.br` ou domínio temporário.

Essa opção faz sentido se:

- Há preferência por custo fixo.
- Há conforto com SSH/Docker.
- O time aceita cuidar de backup, SSL, firewall e updates.

Essa opção não é ideal se:

- A prioridade é velocidade e pouca manutenção.

## 16. Caminho de Evolução Develop / Staging / Produção

- Local: Docker Compose atual.
- Develop futuro: ambiente automático para branch `develop`, dados descartáveis.
- Staging: ambiente estável para validação com usuários internos.
- Produção: ambiente separado, banco gerenciado, storage real, backups, domínio próprio, monitoramento e deploy controlado.

Separação mínima:

- Banco local diferente do banco de staging.
- Banco de staging diferente do banco de produção.
- Bucket staging diferente do bucket produção.
- JWT secret staging diferente do JWT secret produção.
- Seeds demo apenas em local/staging.

## 17. Arquitetura Sugerida para Staging

```txt
Usuários
  ↓
Vercel/Netlify Static Frontend
  ↓ HTTPS
Railway/Render Backend NestJS
  ↓
Postgres Gerenciado
  ↓ opcional
AWS S3 para documentos
```

Configuração:

- `VITE_API_URL=https://api-staging...`
- `NODE_ENV=production`
- `DB_SYNCHRONIZE=false`
- `DB_MIGRATIONS_RUN=false`
- `JWT_SECRET` forte
- `CORS_ORIGINS=https://frontend-staging...`

## 18. Arquitetura Sugerida para Produção Futura

```txt
Cloudflare / DNS
  ↓
Frontend estático CDN
  ↓
API backend containerizada
  ↓
Postgres gerenciado com backup/PITR
  ↓
S3 privado + URLs assinadas
  ↓
Logs, métricas e alertas
```

Produção futura pode ir para:

- AWS ECS/App Runner + RDS + S3 + CloudFront.
- Fly.io/Render/Railway com planos maiores.
- VPS robusto, se houver disciplina operacional.

## 19. Checklist de Implementação do Staging

Antes do deploy:

- Ajustar CORS para env.
- Definir `VITE_API_URL`.
- Definir banco staging.
- Rodar migrations.
- Criar/validar usuários Lucas, Gabriel e Leonardo.
- Gerar `JWT_SECRET` forte.
- Garantir `DB_SYNCHRONIZE=false`.
- Decidir se upload real entra agora.

Deploy:

- Subir frontend estático.
- Subir backend.
- Configurar Postgres.
- Rodar `npm run db:migration:run`.
- Rodar seed controlado, se necessário.
- Testar login.
- Testar troca de tenant.
- Testar projeto, entregáveis, documentos, revisões, knowledge e tags.

Depois:

- Validar logs.
- Criar rotina simples de backup.
- Registrar URLs e credenciais demo.
- Bloquear dados sensíveis/reais.

## 20. Riscos e Cuidados

- CORS atual bloqueia staging se não for alterado.
- Upload/download real ainda precisa ajuste de URL assinada ou endpoint de download.
- Seed atual pode não ter todos os usuários desejados.
- Docker Compose atual não deve ser usado como produção sem adaptação.
- Banco gerenciado com SSL pode exigir suporte a `DB_SSL`.
- Não rodar seed automaticamente em produção.
- Não usar dados reais sensíveis em staging.
- Não expor Swagger público sem controle se houver dados sensíveis.

## 21. Perguntas Pendentes para Lucas

- Vocês já têm domínio para staging?
- Gabriel já deve existir no seed ou será criado manualmente?
- Upload/download de documentos precisa funcionar no primeiro staging?
- Pode usar Vercel/Railway/Render ou há preferência por VPS?
- O staging terá dados reais ou apenas dados fake?
- Quem terá acesso administrativo?

## 22. Decisão Recomendada

Seguir com:

- Agora: Vercel/Netlify + Railway/Render + Postgres gerenciado.
- Corte mínimo antes: CORS por env + validar migrations + usuários demo.
- Se documento for obrigatório: corrigir download com URL assinada antes.
- Depois: domínio próprio, S3 privado, backups melhores e pipeline CI/CD.

## Fontes Consultadas

- Vercel pricing: https://vercel.com/pricing
- Railway pricing: https://railway.com/pricing
- Render pricing: https://render.com/pricing
- Fly.io pricing: https://fly.io/docs/about/pricing/
- AWS Lightsail pricing: https://aws.amazon.com/lightsail/pricing/
- AWS RDS PostgreSQL pricing: https://aws.amazon.com/rds/postgresql/pricing/
- AWS S3 pricing: https://aws.amazon.com/s3/pricing/
- Hetzner Cloud: https://www.hetzner.com/cloud/
