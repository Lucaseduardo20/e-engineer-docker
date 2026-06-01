# 📋 Análise Completa: Estado Atual E-Engineer e Roadmap MVP

**Data:** 25 de maio de 2026  
**Objetivo:** Mapeamento de próximos passos para MVP funcional + validação de produto

---

## 📊 RESUMO EXECUTIVO

### O que foi feito ✅
- **Backend:** Fundação sólida com Clean Architecture + DDD, Shared Kernel pronto, módulo Projects como exemplo, multi-tenancy implementado, Docker + PostgreSQL configurados.
- **Frontend:** Layout autenticado, dashboard mockado com componentes reutilizáveis, estrutura modular iniciada, Vue 3 + Vite + TypeScript.
- **Documentação:** Protocol de trabalho estabelecido (master.md), auditoria de decisões (codex.md), guia do agente frontend.

### O que falta para MVP funcional ❌
**Crítico e bloqueador:**
1. **Autenticação Real** — Login/JWT, contexto de usuário, proteção de rotas
2. **Integração Frontend-Backend** — Axios, interceptores de auth, tratamento de erros
3. **Dados Reais do Banco** — Criar e listar projetos com persistência real
4. **Validação em Formulários** — Feedback visual, tratamento de erros

### Prioridade para Validação 🎯
O produto pode ser validado com usuários-chave após **Fase 1 (MVP Mínimo)**, que entrega:
- Login funcional
- Criar projeto
- Listar projetos
- Fluxo end-to-end testável

---

## 🏗️ ARQUITETURA ATUAL

### Backend: Clean Architecture + DDD

```
src/
├── shared/
│   ├── domain/          ✅ Entity, AggregateRoot, ValueObject, DomainEvents, OrganizationId
│   ├── application/     ✅ Result, TenantScope, DomainEventPublisher interface
│   ├── infrastructure/  ✅ TypeORM config, TenantScopedOrmEntity, EventBus
│
├── modules/
│   ├── projects/
│   │   ├── domain/      ✅ Project entity, ProjectStatus, ProjectRepository interface
│   │   ├── application/ ✅ CreateProjectUseCase (com testes), DTOs
│   │   ├── infrastructure/ ✅ TypeORM mapper e repository implementation
│   │   └── presentation/ ✅ ProjectsController (POST /projects)
│   │
│   ├── identity/        ⏳ Stub (não tem login ainda)
│   ├── organizations/   ⏳ Stub
│   ├── templates/       ⏳ Stub
│   ├── deliverables/    ⏳ Stub
│   ├── documents/       ⏳ Stub
│   ├── reviews/         ⏳ Stub
│   ├── knowledge-base/  ⏳ Stub
│   └── audit/           ⏳ Stub
│
└── app.module.ts        ✅ Setup da aplicação
```

**Stack:** NestJS 11, TypeORM 0.3, PostgreSQL, Docker, TypeScript

**Key Decisions:**
- Single database, single schema, isolamento por `organizationId`
- TenantScope explícito em repositórios e use cases
- TypeORM isolado na infrastructure (não é entidade de domínio)
- Event bus in-process pronto para evolução

### Frontend: Modular Architecture

```
src/
├── app/
│   ├── layouts/         ✅ AuthenticatedLayout.vue
│   └── styles/          ✅ global.css
│
├── modules/
│   ├── dashboard/
│   │   ├── components/  ✅ DashboardMetricCard, PendingReviewList, etc
│   │   ├── pages/       ✅ DashboardPage.vue (dados mockados)
│   │   ├── mocks/       ✅ dashboard.mock.ts (dados realistas)
│   │   └── types/       ✅ dashboard.types.ts
│   │
│   ├── projects/        ⏳ Não tem lista real ainda
│   ├── deliverables/    ⏳ Não existe
│   ├── documents/       ⏳ Não existe
│   ├── reviews/         ⏳ Não existe
│   └── ...
│
├── shared/
│   ├── components/      ✅ BasePageHeader, BaseStatusChip
│   ├── types/           ✅ status-tone.types
│   └── formatters/      ✅ date.formatter
│
├── router/              ✅ Vue Router setup com redirecionamento /
├── stores/              ✅ Pinia ready (sem stores reais ainda)
└── main.ts              ✅ Bootstrap da app
```

**Stack:** Vue 3, Vite 8, TypeScript, Pinia, Vue Router, Vitest

**Key Decisions:**
- Sem Vuetify 3 ainda (CSS customizado por enquanto)
- Sem Axios ainda (use cases precisam de integração HTTP)
- Composable API com `<script setup lang="ts">`
- Tipagem forte em todos os componentes

---

## 🚀 FLUXO DE IMPLEMENTAÇÃO (Ordem Recomendada)

### Fase 1: MVP Mínimo Viável (Bloqueador Principal) 🔴

**Duração estimada:** 3-5 dias de desenvolvimento  
**Objetivo:** Produzir fluxo end-to-end testável: Login → Criar Projeto → Ver em Lista

#### 1.1 Autenticação Backend (Identity Module)
**Arquivos a criar/modificar:**
- `src/modules/identity/domain/entities/user.ts` — Entidade User com validações
- `src/modules/identity/domain/errors/` — Erros de domínio (invalid email, etc)
- `src/modules/identity/domain/repositories/user.repository.ts` — Interface do repositório
- `src/modules/identity/application/use-cases/login.use-case.ts` — Orquestração de login + JWT issuance
- `src/modules/identity/infrastructure/persistence/typeorm/user.orm-entity.ts` — Mapeamento ORM
- `src/modules/identity/infrastructure/persistence/typeorm/typeorm-user.repository.ts` — Implementação
- `src/modules/identity/presentation/controllers/auth.controller.ts` — POST /auth/login
- `src/modules/identity/application/dto/login.dto.ts` — DTO de entrada/saída
- `src/shared/infrastructure/auth/jwt.strategy.ts` — JWT strategy NestJS
- `src/shared/infrastructure/auth/auth.guard.ts` — Guard de autenticação
- Atualizar `app.module.ts` com módulo Identity

**Validações:**
- Use case de login tem teste unitário
- Controller valida entrada (email, password não vazias)
- Token JWT gerado e retornado

#### 1.2 Integração Frontend: Login Page + Axios

**Arquivos a criar/modificar:**
- Instalar `axios` via npm
- `src/shared/http/http-client.ts` — Wrapper customizado com interceptor de auth
- `src/stores/auth.store.ts` — Pinia store para autenticação (token, user)
- `src/modules/auth/pages/LoginPage.vue` — Formulário de login (html puro ou validação simples)
- `src/router/guards/auth.guard.ts` — Route guard que protege /dashboard
- Atualizar `src/router/index.ts` com rota /login e guard

**Validações:**
- Formulário faz POST /auth/login com credentials
- Token salvo no store e localStorage
- Interceptor adiciona Authorization header em requisições
- Rota /dashboard redirecionada se não autenticado
- Login bem-sucedido redireciona para /dashboard

#### 1.3 GetProjects UseCase Backend

**Arquivos a criar/modificar:**
- `src/modules/projects/application/use-cases/get-projects.use-case.ts` — Lista projetos por organizationId
- `src/modules/projects/application/dto/get-projects.dto.ts` — DTO de saída (lista)
- Atualizar `src/modules/projects/presentation/controllers/projects.controller.ts` — adicionar GET /projects

**Validações:**
- Use case recebe TenantScope com organizationId
- Query retorna apenas projetos da organização
- Controller retorna lista formatada
- Teste unitário cobre fluxo

#### 1.4 Projects List Page Frontend

**Arquivos a criar/modificar:**
- `src/modules/projects/pages/ProjectsListPage.vue` — Página que lista projetos
- `src/modules/projects/composables/use-projects.ts` — Composable que chama API
- Atualizar `src/router/index.ts` com rota /projects
- Adicionar link no dashboard ou sidebar para Projects

**Validações:**
- Componente faz GET /projects ao montar
- Renderiza tabela/cards com projetos
- Tratamento de loading e erro
- Token enviado no header Authorization

#### 1.5 Integração: Create Project Form Conectado

**Modificações:**
- Form de "novo projeto" no dashboard ou Projects page
- POST para backend com project data
- Feedback visual (loading, sucesso, erro)
- Lista atualizada após sucesso

#### 1.6 Seed do Banco de Dados

**Arquivos a criar:**
- `src/database/seeds/seed-organization.ts` — Cria organização de teste
- `src/database/seeds/seed-user.ts` — Cria usuário vinculado à organização
- Script npm para rodar seeds

**Validações:**
- User pode fazer login
- Projetos criados aparecem para a organização correta
- Isolamento: projetos de org A não aparecem para user de org B

#### 1.7 Validações End-to-End

**Testes:**
- Rodar `npm run start:dev` no backend
- Rodar `npm run dev` no frontend (Node 22)
- Login com credenciais de seed
- Criar projeto
- Verificar na lista
- Logout
- Tentar acessar /dashboard → redireciona para /login

**Entregável ao final da Fase 1:**
✅ Login funcional  
✅ Dashboard após login  
✅ Listar projetos criados  
✅ Criar novo projeto via formulário  
✅ Fluxo end-to-end testável (pode ser demonstrado)

---

### Fase 2: MVP +1 (Adicionar Fluxo Completo) 🟡

**Duração estimada:** 3-5 dias  
**Objetivo:** Validar linguagem de domínio com caso real: Projeto → Entregável → Documento

#### 2.1 Modulo Deliverables

Criar estrutura DDD completa em `src/modules/deliverables/`:
- Entity `Deliverable` com status, responsável, prazo
- Use cases: `CreateDeliverable`, `GetProjectDeliverables`
- DTOs, mapper, repository, controller
- Relação com Project (Project 1:N Deliverable)

#### 2.2 Frontend: Project Detail Page

- Rota `/projects/:id`
- Exibir detalhes do projeto
- Listar entregáveis
- Botão "Adicionar Entregável"
- Form inline ou modal

#### 2.3 Documentos Básicos

- Entity `Document` vinculada a `Deliverable`
- Versioning simples (v1, v2, etc)
- Status (draft, submitted, approved)

#### 2.4 Revisões Simplificadas

- Marcar documento como "enviado para revisão"
- Listar revisões pendentes
- Aprovar/rejeitar básico
- Registrar no activity log

**Entregável ao final da Fase 2:**
✅ Fluxo completo: Projeto → Entregável → Documento → Revisão  
✅ Linguagem de domínio refletida nas telas  
✅ Pronto para validação com engenheiros reais

---

### Fase 3: Polimento & UX 🟢

**Duração estimada:** 2-3 dias  
**Objetivo:** Melhorar apresentação e experiência do usuário

#### 3.1 Vuetify 3 Integration

- Instalar Vuetify 3
- Substituir componentes customizados por componentes Vuetify
- Temas e variações
- Layout responsivo

#### 3.2 Validação em Produção

- Mensagens de erro claras
- Estados vazios bem desenhados
- Loading states
- Confirmações antes de ações destrutivas

#### 3.3 Responsividade

- Layouts adaptáveis para mobile
- Drawer/sidebar colapsível
- Touch-friendly

#### 3.4 Activity Log Real

- Registrar eventos reais do projeto
- Exibir no dashboard
- Timeline de eventos

**Entregável ao final da Fase 3:**
✅ App profissional e pronto para apresentação  
✅ Pronto para validação com múltiplos usuários

---

## 📋 CHECKLIST DETALHADO: Fase 1

Para não esquecer nada, use este checklist durante a implementação:

### Backend

- [ ] User entity criada em identity/domain
- [ ] Login use case implementado
- [ ] JWT strategy e guard criados
- [ ] User repository e ORM entity
- [ ] Auth controller com POST /auth/login
- [ ] GetProjects use case implementado
- [ ] GET /projects adicionado ao controller
- [ ] Testes unitários do login
- [ ] Testes do get-projects
- [ ] Database seed com organização e user
- [ ] `npm run build` passa
- [ ] `npm run test` passa
- [ ] `npm run start:dev` levanta sem erros

### Frontend

- [ ] Axios instalado
- [ ] Http client com interceptor
- [ ] Auth store (Pinia) criada
- [ ] LoginPage.vue criada
- [ ] Auth guard no router
- [ ] Rota /login adicionada
- [ ] Rota /projects adicionada
- [ ] ProjectsList.vue criada
- [ ] Composable use-projects
- [ ] Dashboard com link para projects
- [ ] Form de criar projeto no frontend
- [ ] Integração POST /projects
- [ ] Feedback visual (loading, erro, sucesso)
- [ ] localStorage persiste token
- [ ] `npm run build` passa
- [ ] `npm run type-check` passa
- [ ] `npm run dev` levanta sem erros

### End-to-End

- [ ] Login com seed user funciona
- [ ] Token salvo em localStorage
- [ ] Dashboard carrega
- [ ] GET /projects retorna dados
- [ ] Lista de projetos renderiza
- [ ] Form de novo projeto funciona
- [ ] Novo projeto aparece na lista
- [ ] Logout limpa token
- [ ] Acesso sem token redireciona para /login
- [ ] Organização isolada (multi-tenancy funciona)

---

## 🗣️ LINGUAGEM DE DOMÍNIO NA TELA

Ao criar as telas, sempre usar termos da engenharia civil:

✅ **Correto:**
- "Projeto Técnico"
- "Entregável"
- "Documento Oficial"
- "Revisão Pendente"
- "Responsável Técnico"
- "Versão Aprovada"
- "Projeto de Referência"

❌ **Evitar:**
- "Task"
- "Item"
- "File"
- "Pending Action"
- "Owner"
- "Release"

---

## 📚 DOCUMENTAÇÃO PARA REFERÊNCIA

Você tem 3 documentos principais:

1. **[master.md](../master.md)** — Guia estável do projeto (leia sempre antes de decidir)
   - Princípios de arquitetura
   - Stack definida
   - Protocolo de trabalho com IA
   - Estratégia de commits
   - Validações padrão

2. **[backend/codex.md](e-engineer-backend/codex.md)** — Auditoria e histórico de decisões
   - O que foi decidido e por quê
   - Contexto de implementações anteriores
   - Fundação técnica + primeiro corte modular

3. **[frontend/codex.md](e-engineer-frontend/codex.md)** — Histórico frontend
   - Layout autenticado + dashboard mockado
   - Notas de continuidade
   - NVM + Node 22 requerido

4. **[frontend/frontend-agent.md](e-engineer-frontend/frontend-agent.md)** — Guia operacional do agente frontend
   - Stack esperada
   - Objetivo visual
   - Princípios de UX
   - Estrutura de módulos

---

## ⚠️ RISCOS E DEPENDÊNCIAS

| Risco | Impacto | Mitigação |
|-------|---------|-----------|
| Autenticação adiada | Sem isolamento tenant real testado | **ALTA PRIORIDADE** — Implementar em Fase 1 |
| Sem integração real | Frontend com mocks não valida API | Integração Fase 1 |
| Node 18 vs Node 22 | Build/testes falham com Node 18 | Usar NVM para rodar Vite/Vitest |
| Sem Vuetify | UI fica cru, difícil de vender | Pode ficar para Fase 3 |
| Sem validação de form | Entregáveis precários | Zod ou Yup quando formulários forem reais |
| Database schema não finalizado | Migrations problemáticas | Seed simples + evoluir gradualmente |

---

## 🎯 PRÓXIMOS PASSOS IMEDIATOS

**Antes de começar a implementar:**

1. ✅ Revisar este documento com o usuário
2. ✅ Confirmar prioridades (Fase 1 → 2 → 3)
3. ✅ Decidir: Zod ou Yup para validação?
4. ✅ Decidir: Adicionar Vuetify já em Fase 1 ou deixar para Fase 3?
5. ✅ Revisar seeds do banco (que user/org criar?)

**Depois:**

1. Começar com Backend: Autenticação (Identity module)
2. Depois Frontend: Login page + auth store
3. Depois: Integração (GetProjects)
4. Depois: Projects list
5. E2E testing do fluxo

---

**Documentado e pronto para implementação! 🚀**

