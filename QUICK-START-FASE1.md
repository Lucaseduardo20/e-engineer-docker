# 🚀 QUICK START: Próximos Passos Imediatos

**Localização:** Projeto E-Engineer  
**Data:** 25 de maio de 2026  
**Objetivo:** Implementar Fase 1 para ter MVP funcional em ~7-10 dias

---

## 📍 Onde Tudo Está

### Documentação Mestre
- **[../master.md](../master.md)** — Leia SEMPRE antes de implementar qualquer coisa importante
- **[../ANALISE-MVP-2026-05-25.md](../ANALISE-MVP-2026-05-25.md)** — Análise completa (este documento)

### Backend
- **Path:** `/home/lkt/work/e_engineer/e-engineer-backend`
- **Documentação:** [codex.md](e-engineer-backend/codex.md) (histórico de decisões)
- **Começar por:** `src/modules/identity/` (criar autenticação)

### Frontend
- **Path:** `/home/lkt/work/e_engineer/e-engineer-frontend`
- **Documentação:** [codex.md](e-engineer-frontend/codex.md) (notas de continuidade)
- **Documentação Agente:** [frontend-agent.md](e-engineer-frontend/frontend-agent.md) (guia operacional)
- **Começar por:** `src/modules/auth/` (criar login)

---

## ✅ Checklist de Implementação: Fase 1

### Dia 1-2: Backend — Autenticação

#### Backend setup
```bash
cd /home/lkt/work/e_engineer/e-engineer-backend
npm install  # Se não estiver instalado
npm run start:dev
```

**Criar a estrutura Identity Module:**
- [ ] `src/modules/identity/domain/entities/user.ts` — Entidade User
- [ ] `src/modules/identity/domain/errors/` — Erros de domínio
- [ ] `src/modules/identity/domain/repositories/user.repository.ts` — Interface repositório
- [ ] `src/modules/identity/application/use-cases/login.use-case.ts` — Use case com JWT
- [ ] `src/modules/identity/application/dto/login.dto.ts` — DTOs
- [ ] `src/modules/identity/infrastructure/persistence/typeorm/user.orm-entity.ts` — Mapeamento ORM
- [ ] `src/modules/identity/infrastructure/persistence/typeorm/typeorm-user.repository.ts` — Implementação
- [ ] `src/modules/identity/presentation/controllers/auth.controller.ts` — POST /auth/login
- [ ] `src/shared/infrastructure/auth/jwt.strategy.ts` — JWT strategy
- [ ] `src/shared/infrastructure/auth/auth.guard.ts` — Guard autenticação
- [ ] Atualizar `app.module.ts` para importar IdentityModule

**Validações:**
```bash
npm run lint
npm run test
npm run build
npm run start:dev  # Validar que /auth/login está disponível
```

### Dia 2-3: Backend — GetProjects

**Adicionar GetProjects use case:**
- [ ] `src/modules/projects/application/use-cases/get-projects.use-case.ts` — Lista por org
- [ ] `src/modules/projects/application/dto/get-projects.dto.ts` — DTO de saída
- [ ] Adicionar `GET /projects` em `projects.controller.ts`
- [ ] Testes do use case

**Validações:**
```bash
npm run test
npm run build
# Testar manualmente: GET /projects com header Authorization
```

### Dia 2-3: Seed do Banco

**Scripts de seed:**
- [ ] Criar arquivo de seed para organização
- [ ] Criar arquivo de seed para usuário
- [ ] Documentar como rodar: `npm run seed`

---

### Dia 3-5: Frontend — Autenticação + API

#### Frontend setup
```bash
cd /home/lkt/work/e_engineer/e-engineer-frontend
source ~/.nvm/nvm.sh
nvm use 22
npm install
npm install axios  # Adicionar axios
npm run dev
```

**Criar estrutura Auth:**
- [ ] `src/shared/http/http-client.ts` — Wrapper Axios com interceptor
- [ ] `src/stores/auth.store.ts` — Pinia store para auth + token
- [ ] `src/modules/auth/pages/LoginPage.vue` — Form de login
- [ ] `src/router/guards/auth.guard.ts` — Route guard
- [ ] Atualizar `src/router/index.ts` com rota `/login` e guard

**Criar Projects List:**
- [ ] `src/modules/projects/pages/ProjectsListPage.vue` — Componente lista
- [ ] `src/modules/projects/composables/use-projects.ts` — Composable para chamar API
- [ ] Atualizar router com rota `/projects`
- [ ] Adicionar link no dashboard ou sidebar para projects

**Formulário de criar projeto:**
- [ ] Form simples no Projects page (ou botão no dashboard)
- [ ] POST /projects integrado
- [ ] Feedback visual de loading/erro/sucesso

**Validações:**
```bash
npm run type-check
npm run build
npm run dev  # Verificar que tudo levanta sem erros
```

---

### Dia 5-7: Testes End-to-End

**Setup:**

Terminal 1 — Backend:
```bash
cd e-engineer-backend
source ~/.nvm/nvm.sh
nvm use 22  # Ou use sua versão
npm run seed  # Criar user de teste
npm run start:dev
```

Terminal 2 — Frontend:
```bash
cd e-engineer-frontend
source ~/.nvm/nvm.sh
nvm use 22
npm run dev
```

**Manual E2E Testing:**
- [ ] Abrir http://localhost:5173 (ou porta que subir)
- [ ] Redireciona para /login ✅
- [ ] Login com credenciais do seed (ex: admin@test.com / password123)
- [ ] Token salvo em localStorage ✅
- [ ] Redireciona para /dashboard ✅
- [ ] Dashboard carrega normalmente ✅
- [ ] Clicar em "Projects" ou link no dashboard ✅
- [ ] GET /projects funciona e mostra lista vazia ou com projetos existentes ✅
- [ ] Botão "New Project" abre form ✅
- [ ] Preencher form e enviar ✅
- [ ] Novo projeto aparece na lista ✅
- [ ] Logout limpa token e redireciona para /login ✅
- [ ] Tentar acessar /dashboard sem token → redireciona para /login ✅

---

## 🏁 Pronto para Apresentação?

Se tudo acima funcionar, você tem um MVP que pode ser apresentado:

✅ **Login funcional**  
✅ **Criar projeto com persistência real**  
✅ **Listar projetos**  
✅ **Fluxo end-to-end**  
✅ **Multi-tenancy testado**  

**Próximo:** Fase 2 (Deliverables + Documents) para validação com usuários reais.

---

## 🔗 Referência Rápida de Comandos

### Backend
```bash
# Setup e development
cd e-engineer-backend
npm install
npm run start:dev

# Testes
npm run test
npm run test:cov

# Build
npm run build

# Seed do banco
npm run seed
```

### Frontend
```bash
# Setup (com Node 22)
cd e-engineer-frontend
source ~/.nvm/nvm.sh
nvm use 22
npm install
npm install axios  # Se necessário

# Development
npm run dev

# Testes
npm run test:unit
npm run test:coverage

# Type checking
npm run type-check

# Build
npm run build
```

---

## 📌 Decisões Principais Já Tomadas

✅ **Multi-tenancy:** Single database, single schema, isolamento por organizationId  
✅ **Backend:** NestJS + TypeORM + Clean Architecture + DDD  
✅ **Frontend:** Vue 3 + Vite + TypeScript + Pinia + Vue Router  
✅ **Node:** 22.x para build/testes/dev (18.x não funciona com Vite)  
✅ **JWT:** Token no Authorization header  
✅ **Event Bus:** In-process (evoluir para outbox/mensageria depois)

---

## ⚠️ Pontos de Atenção

| Ponto | Ação |
|-------|------|
| Node 18 vs 22 | Usar NVM com Node 22 para frontend |
| Vuetify 3 | Ainda não instalado (pode ficar para Fase 3) |
| Validação | Zod ou Yup? Decidir quando formulários ficarem reais |
| Seed do banco | Documentar credenciais de teste |
| CORS | Pode ser necessário ativar CORS no backend |
| Environment | Usar .env para URLs da API |

---

## 📚 Referência Documentos

| Documento | Leitura | Quando Ler |
|-----------|---------|-----------|
| [master.md](../master.md) | OBRIGATÓRIA | Antes de qualquer decisão arquitetural |
| [ANALISE-MVP-2026-05-25.md](../ANALISE-MVP-2026-05-25.md) | COMPLETA | Visão geral e roadmap |
| [backend/codex.md](e-engineer-backend/codex.md) | SE NECESSÁRIO | Para entender decisões anteriores |
| [frontend/codex.md](e-engineer-frontend/codex.md) | SE NECESSÁRIO | Para setup do frontend |
| [frontend/frontend-agent.md](e-engineer-frontend/frontend-agent.md) | IMPORTANTE | Guia do agente frontend |

---

**Bom desenvolvimento! 🚀 Qualquer dúvida, releia o master.md e a análise completa.**

