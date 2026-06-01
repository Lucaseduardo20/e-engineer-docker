# 🎯 ROADMAP GLOBAL E-ENGINEER

**Data:** 26 de maio de 2026  
**Status Geral:** MVP 60% Pronto | Pronto para integração frontend-backend  
**Timeline MVP:** 7-10 dias de desenvolvimento focado

---

## 📊 RESUMO EXECUTIVO - PANORAMA COMPLETO

### ✅ Fundação (SÓLIDA)
- ✅ Clean Architecture + DDD implementado
- ✅ NestJS 11 + TypeScript strict mode
- ✅ PostgreSQL + TypeORM migrations
- ✅ JWT authentication infrastructure
- ✅ Vue 3 + Pinia + Vue Router setup
- ✅ Shared Kernel (Entity, ValueObject, DomainEvent)
- ✅ Multi-tenancy explícita via OrganizationId
- ✅ Documentação estratégica 100% completa

### ⏳ Em Progresso (60%)
- ⏳ **Backend:** Identity (95%), Projects (60%)
- ⏳ **Frontend:** Auth (70%), Dashboard (90%), Projects (40%)
- ⏳ **Integração:** Frontend services → Backend APIs (10%)

### ❌ Não Iniciado (0%)
- ❌ Deliverables module
- ❌ Documents module
- ❌ Reviews module
- ❌ Knowledge-base module
- ❌ E2E testing suite

### 📈 Métricas Atuais
| Métrica | Status |
|---------|--------|
| Backend linha de código | ~1,350 |
| Frontend linhas de código | ~800 |
| Funcionalidades implementadas | 25% do escopo total |
| API integrada end-to-end | 10% |
| Testes coverage | 20% |
| Documentação | 100% |

---

## 🚨 IMPEDIMENTOS CRÍTICOS PARA MVP

### 🔴 CRÍTICOS (Bloqueadores - Resolver em 24-48h)

#### 1. **Frontend Services Layer não existe**
- **Problema:** Frontend store chama `apiClient.projects.list()` mas método não existe
- **Impacto:** Projects page não funciona, dashboard usa apenas dados mockados
- **Severidade:** 🔴 CRÍTICO
- **Fix:** 
  - Criar `src/shared/http/api/` com módulos de serviço
  - Implementar `ProjectsService`, `AuthService`, etc.
  - Testar integração com backend real
- **Estimativa:** 4-6 horas
- **Prioridade:** **#1 - FAZER HOJE**

#### 2. **Frontend-Backend desconexão não testada**
- **Problema:** Integração API não foi validada end-to-end
- **Impacto:** Login → Dashboard → Listar Projetos pode quebrar
- **Severidade:** 🔴 CRÍTICO
- **Fix:**
  - Setup docker-compose
  - Rodar backend + frontend juntos
  - Test login com credenciais reais
  - Test criar projeto via frontend
  - Test listar projetos no dashboard
- **Estimativa:** 2-3 horas
- **Prioridade:** **#2 - FAZER APÓS #1**

#### 3. **CORS não configurado no backend**
- **Problema:** Frontend (localhost:5173) vs Backend (localhost:3000)
- **Impacto:** Requisições CORS falham
- **Severidade:** 🔴 CRÍTICO
- **Fix:**
  ```typescript
  // main.ts
  app.enableCors({
    origin: ['http://localhost:5173', 'http://localhost:3000'],
    credentials: true
  });
  ```
- **Estimativa:** 15 minutos
- **Prioridade:** **#2 - FAZER JUNTO COM #1**

#### 4. **Seed database + usuários de teste não validados**
- **Problema:** Banco vazio, não há usuários para testar login
- **Impacto:** Não consegue fazer login para testar fluxo
- **Severidade:** 🔴 CRÍTICO
- **Fix:**
  - Rodar `npm run db:seed` no backend
  - Validar usuários foram criados
  - Testar login com seed user
- **Estimativa:** 1 hora
- **Prioridade:** **#2 - FAZER JUNTO COM #2**

#### 5. **Token refresh flow não existe**
- **Problema:** JWT expira e usuário perde acesso sem forma de renovar
- **Impacto:** Sessão expira durante uso
- **Severidade:** 🔴 CRÍTICO (para produção, médio para MVP)
- **Fix:**
  - Implementar refresh token no Identity module
  - Axios interceptor captura 401 e tenta renovar
  - Testar fluxo de expiração
- **Estimativa:** 3-4 horas
- **Prioridade:** **#4 - ANTES DE IR PARA PRODUÇÃO**

---

### 🟡 ALTOS (Necessários para MVP funcional - 48-72h)

#### 6. **Logout não testado**
- **Problema:** LogoutPage existe mas não foi testado
- **Impacto:** Usuário pode ficar em estado inconsistente
- **Fix:** Testar logout → limpa localStorage → redireciona → login
- **Estimativa:** 2 horas
- **Prioridade:** #5

#### 7. **Testes E2E não existem**
- **Problema:** Sem testes automatizados do fluxo completo
- **Impacto:** Regressões não detectadas
- **Fix:** Criar suite E2E com Playwright/Cypress
  - Login → Dashboard → Criar Projeto → Verificar lista
  - Login → Listar Projetos → Abrir detalhe
  - Logout
- **Estimativa:** 4-6 horas
- **Prioridade:** #5 (paralelo com testes unitários)

#### 8. **Tipos API não 100% sincroniados**
- **Problema:** Frontend tipos podem não bater com backend DTOs
- **Impacto:** Runtime errors, inconsistência de dados
- **Fix:** 
  - Validar interfaces de Projects, Users, Organizations
  - Sincronizar com backend DTOs
  - Documentar contrato API
- **Estimativa:** 2 horas
- **Prioridade:** #6

#### 9. **Error handling inconsistente**
- **Problema:** Backend retorna 500, frontend não trata adequadamente
- **Impacto:** Usuário vê erro genérico, não sabe o que fazer
- **Fix:**
  - Implementar error interceptor no frontend
  - Backend mapear erros para status codes corretos (400, 401, 403, 404, 409)
  - Frontend mostrar mensagens amigáveis
- **Estimativa:** 3 horas
- **Prioridade:** #6

#### 10. **Vuetify parcialmente integrado**
- **Problema:** Vuetify instalado mas componentes ainda usam CSS custom
- **Impacto:** Inconsistência visual, dificuldade de manutenção
- **Fix:** Escolher: A) Remover Vuetify e usar só CSS, ou B) Integrar completamente
  - Recomendação: Integrar Vuetify (mais escalável)
  - Converter componentes principais (DashboardMetricTile, etc)
- **Estimativa:** 6-8 horas
- **Prioridade:** #7 (pode ficar para após MVP)

---

### 🟢 MÉDIOS (Nice-to-have para MVP, pode ficar para Sprint 2)

#### 11. **Organização não tem module backend completo**
- **Problema:** Organizations é apenas stub com query service
- **Impacto:** Não é possível gerenciar organizações (criar, listar, atualizar)
- **Fix:** Implementar Organizations module (Domain → Presentation)
- **Estimativa:** 8-12 horas
- **Prioridade:** #8 (Sprint 2)

#### 12. **Frontend não tem service layer estruturado**
- **Problema:** API calls espalhadas em componentes/stores
- **Impacto:** Difícil de testar, refatorar, evoluir
- **Fix:** Criar serviços em `src/modules/{module}/services/`
  - ProjectsService
  - OrganizationsService
  - etc.
- **Estimativa:** 4-6 horas
- **Prioridade:** #8 (Sprint 2)

#### 13. **Tests coverage muito baixa**
- **Problema:** ~20% cobertura, regressions podem passar
- **Impacto:** Qualidade de código reduz over time
- **Fix:** 
  - Add testes para Projects module (80% coverage)
  - Add testes para Identity module (80% coverage)
  - Add testes para componentes críticos frontend
- **Estimativa:** 8-10 horas
- **Prioridade:** #8 (Sprint 2)

#### 14. **Responsividade não implementada**
- **Problema:** Layout é desktop-first, mobile quebra
- **Impacto:** Sem MVP mobile
- **Fix:** Implementar breakpoints Tailwind/Vuetify
  - Dashboard responsivo
  - Projects table responsivo
- **Estimativa:** 6-8 horas
- **Prioridade:** #9 (Sprint 2 ou 3)

---

## 📋 O QUE FALTA CONSTRUIR (Por Sprint)

### Sprint 0: Integração Imediata (HOJE - 48h) 🔥

**Objetivo:** Validar que MVP funciona end-to-end

| Task | Descrição | Estimativa | Depen. | Status |
|------|-----------|-----------|--------|--------|
| **FIX-001** | Implementar Frontend Services Layer | 4-6h | - | 🔴 |
| **FIX-002** | Habilitar CORS no backend | 15min | - | 🔴 |
| **FIX-003** | Testar integração Login → Dashboard | 2h | FIX-001, FIX-002 | 🔴 |
| **FIX-004** | Validar e rodar db:seed | 1h | - | 🔴 |
| **FIX-005** | Testar criar/listar projetos end-to-end | 2h | FIX-001, FIX-004 | 🔴 |
| **FIX-006** | Testar logout flow | 1-2h | FIX-005 | 🟡 |
| **FIX-007** | Sincronizar tipos API frontend-backend | 2h | FIX-001 | 🟡 |
| **FIX-008** | Criar teste E2E básico (login → list) | 3-4h | FIX-005 | 🟡 |
| **TOTAL** | | **18-24 horas** | | |

**Entregáveis:**
- ✅ Frontend consegue fazer login
- ✅ Dashboard mostra projetos do banco real
- ✅ Pode criar projeto via frontend e vê em lista
- ✅ Logout funciona
- ✅ Teste E2E baseline

---

### Sprint 1: MVP Mínimo Validado (72h-96h)

**Objetivo:** MVP funcional pronto para primeiros usuários internos

| Task | Módulo | O Que | Estimativa | Status |
|------|--------|-------|-----------|--------|
| **MVP-001** | Projects | Refinar UI de projetos (Vuetify integration) | 6h | ⏳ |
| **MVP-002** | Projects | Add filter/search em projects list | 3h | ⏳ |
| **MVP-003** | Projects | Validar error handling completo | 3h | ⏳ |
| **MVP-004** | Identity | Refresh token flow | 4h | ⏳ |
| **MVP-005** | Backend | Add validação global (class-validator) | 2h | ⏳ |
| **MVP-006** | Frontend | Add loading states em todas as requisições | 3h | ⏳ |
| **MVP-007** | Tests | Coverage mínima 60% backend | 6h | ⏳ |
| **MVP-008** | Tests | Coverage mínima 40% frontend | 4h | ⏳ |
| **MVP-009** | Docs | Guia QA para testar fluxo MVP | 2h | ⏳ |
| **TOTAL** | | | **33-40 horas** | |

**Entregáveis:**
- ✅ MVP funcional para testes internos
- ✅ Refresh token funcionando
- ✅ Error handling consistente
- ✅ Testes cobrindo happy path
- ✅ Guia de QA

---

### Sprint 2: Módulos de Negócio Essenciais (120h)

**Objetivo:** Adicionar next layer de funcionalidades

#### 2.1: Deliverables Module (30h)

| Task | O Que |
|------|-------|
| **DEL-001** | Domain: Deliverable entity + ValueObjects (tipo, status) |
| **DEL-002** | Application: Use cases (Create, List, Get, Update) |
| **DEL-003** | Infrastructure: TypeORM mapper + repository |
| **DEL-004** | Presentation: Controller + DTOs |
| **DEL-005** | Frontend: DeliverablesList component |
| **DEL-006** | Frontend: DeliverableForm component |
| **DEL-007** | Tests: Unit + E2E básico |

#### 2.2: Documents Module (25h)

| Task | O Que |
|------|-------|
| **DOC-001** | Domain: Document entity + ValueObjects (tipo, status) |
| **DOC-002** | Application: Use cases (Create, List, Get, Update, Delete) |
| **DOC-003** | Infrastructure: TypeORM mapper + S3 integration (storage) |
| **DOC-004** | Presentation: Controller + file upload |
| **DOC-005** | Frontend: DocumentsList component |
| **DOC-006** | Frontend: DocumentUpload component |
| **DOC-007** | Tests: Unit + E2E |

#### 2.3: Reviews Module (25h)

| Task | O Que |
|------|-------|
| **REV-001** | Domain: Review entity + ValueObjects (status, reviewer) |
| **REV-002** | Application: Use cases (Create, List, Approve/Reject) |
| **REV-003** | Infrastructure: TypeORM mapper + repository |
| **REV-004** | Presentation: Controller + DTOs |
| **REV-005** | Frontend: ReviewsList component |
| **REV-006** | Frontend: ReviewForm component |
| **REV-007** | Frontend: ReviewsPanel integration (remove mock) |
| **REV-008** | Tests: Unit + E2E |

#### 2.4: Organizations Module (20h)

| Task | O Що |
|------|-------|
| **ORG-001** | Completar Domain layer (estava stub) |
| **ORG-002** | Implementar Use cases |
| **ORG-003** | Frontend: Organizations management page |
| **ORG-004** | Tests: Unit + E2E |

#### 2.5: Knowledge-Base Module (20h)

| Task | O Que |
|------|-------|
| **KB-001** | Domain: KnowledgeBase entity + search index |
| **KB-002** | Application: Create, List, Search use cases |
| **KB-003** | Frontend: KBSearch component (remover mock) |
| **KB-004** | Integração com search (ElasticSearch ou similar) |
| **KB-005** | Tests |

**Entregáveis Sprint 2:**
- ✅ Deliverables CRUD completo
- ✅ Documents CRUD com upload
- ✅ Reviews workflow (criar → revisar → aprovar)
- ✅ Organizations gerenciável
- ✅ Knowledge-Base com busca

---

### Sprint 3: Polimento + Escalabilidade (80h)

#### 3.1: Frontend Polish (30h)
- [ ] Vuetify full integration (design system)
- [ ] Responsividade completa (mobile/tablet)
- [ ] Temas escuro/claro
- [ ] Notificações em tempo real (WebSocket)
- [ ] Offline mode (service worker)

#### 3.2: Backend Robustez (25h)
- [ ] Logging structured (Winston)
- [ ] Monitoring (Prometheus metrics)
- [ ] Rate limiting
- [ ] Request validation schema
- [ ] Audit trail completo (DomainEvents → AuditLog)

#### 3.3: Testing Coverage (15h)
- [ ] 80%+ coverage backend
- [ ] 60%+ coverage frontend
- [ ] Performance tests
- [ ] Load tests

#### 3.4: DevOps + Production (10h)
- [ ] Docker Compose com volumes corretos
- [ ] Environment configuration
- [ ] CI/CD pipeline (GitHub Actions)
- [ ] Database backups automation

---

## 🎯 PRIORIDADES DE IMPLEMENTAÇÃO

### Hierarquia de Necessidade para MVP Real

```
┌─────────────────────────────────────────────────────────┐
│  CRÍTICO - Bloqueador MVP (FAZER AGORA)                │
├─────────────────────────────────────────────────────────┤
│ 1. Frontend Services Layer (apiClient integrado)        │
│ 2. CORS habilitado                                      │
│ 3. Seed database com usuários reais                     │
│ 4. Teste E2E: login → list projects → criar projeto    │
│ 5. Token refresh                                        │
│                                                          │
├─────────────────────────────────────────────────────────┤
│  ALTO - Sprint 1 (Próximas 72h)                        │
├─────────────────────────────────────────────────────────┤
│ 6. Error handling consistente                           │
│ 7. Logout completo                                      │
│ 8. Loading states UI                                    │
│ 9. Refresh token flow testado                           │
│ 10. Testes 60%+ coverage                                │
│                                                          │
├─────────────────────────────────────────────────────────┤
│  MÉDIO - Sprint 2 (Próximas semanas)                   │
├─────────────────────────────────────────────────────────┤
│ 11. Deliverables module                                 │
│ 12. Documents module                                    │
│ 13. Reviews module                                      │
│ 14. Organizations completo                              │
│ 15. Knowledge-base                                      │
│                                                          │
├─────────────────────────────────────────────────────────┤
│  BAIXO - Sprint 3 (Polimento)                          │
├─────────────────────────────────────────────────────────┤
│ 16. Vuetify integration                                 │
│ 17. Responsividade                                      │
│ 18. Temas                                               │
│ 19. Notificações RT                                     │
│ 20. Monitoring prod                                     │
└─────────────────────────────────────────────────────────┘
```

---

## 🚀 ROTEIRO EXECUTIVO (Timeline MVP)

### Dia 1 - Quarta (26/05)
- [ ] Implementar Frontend Services Layer (4-6h)
- [ ] Enable CORS (15min)
- [ ] Rodar db:seed e validar usuários (1h)
- [ ] Testar login → dashboard manual (1h)
- **Checkpoint:** Backend + Frontend conseguem se falar

### Dia 2 - Quinta (27/05)
- [ ] Testar criar/listar projetos end-to-end (2h)
- [ ] Sincronizar tipos (2h)
- [ ] Implementar error handling (2h)
- [ ] Logout completo (1h)
- **Checkpoint:** MVP básico funciona

### Dia 3 - Sexta (28/05)
- [ ] Implementar refresh token (4h)
- [ ] Criar teste E2E (3-4h)
- [ ] Validar testes (2h)
- **Checkpoint:** Testes automatizados passam

### Dias 4-5 - Fim de semana (29-30/05)
- [ ] Polish: loading states, error messages (4h)
- [ ] Tests coverage mínima 60% backend, 40% frontend (8h)
- [ ] QA checklist (2h)
- **Checkpoint:** MVP pronto para stakeholders

### Semana 2 (31/05 - 06/06)
- Sprint 1: Iterar em feedback, robustez
- Sprint 2 (paralelo): Começar Deliverables + Documents

---

## 📊 DEPENDENCY MAP

```
Frontend Services Layer
    ↓
    ├→ CORS ✅
    ├→ DB Seed ✅
    ├→ Login integration
    │   ├→ Error handling
    │   └→ Logout
    │
    ├→ Projects CRUD
    │   ├→ List projects
    │   ├→ Create project
    │   └→ Detail project
    │
    └→ E2E Tests
        └→ Refresh token

Modules Backend (Sprint 2)
    ├→ Deliverables (independent)
    ├→ Documents (independent)
    ├→ Reviews (depends on Projects)
    ├→ Organizations (independent)
    └→ Knowledge-Base (independent)
```

---

## ✅ CHECKLIST IMPLEMENTAÇÃO MVP

### Fase 0: Setup (✅ DONE)
- [x] NestJS + TypeScript setup
- [x] Vue 3 + Pinia setup
- [x] Database + TypeORM
- [x] Authentication (JWT)
- [x] Routers e layouts

### Fase 1: Integração (🔄 IN PROGRESS)
- [ ] Frontend Services implementado
- [ ] CORS ativado
- [ ] Login end-to-end funciona
- [ ] Projects CRUD funciona
- [ ] Refresh token implementado
- [ ] Testes E2E básico
- [ ] Error handling padronizado
- [ ] Tests 60%+ coverage

### Fase 2: Negócio (⏳ PRÓXIMA)
- [ ] Deliverables module
- [ ] Documents module
- [ ] Reviews module
- [ ] Organizations completo
- [ ] Knowledge-base

### Fase 3: Polimento (⏳ DEPOIS)
- [ ] Vuetify integration
- [ ] Responsividade
- [ ] Performance
- [ ] Monitoring

---

## 📂 ARQUIVOS-CHAVE A MODIFICAR (Sprint 0)

### Backend

| Arquivo | O Que Fazer | Linhas |
|---------|-----------|--------|
| [e-engineer-backend/src/main.ts](e-engineer-backend/src/main.ts) | Add app.enableCors() | 1 adição |
| [e-engineer-backend/src/modules/identity/presentation/auth.controller.ts](e-engineer-backend/src/modules/identity/presentation/auth.controller.ts) | Adicionar @UseGuards(JwtAuthGuard) no endpoint protegido | 1 adição |
| [e-engineer-backend/scripts/db-reset.sh](e-engineer-backend/scripts/db-reset.sh) | Assegurar que seed roda | Validar |

### Frontend

| Arquivo | O Que Fazer | Linhas |
|---------|-----------|--------|
| [e-engineer-frontend/src/shared/http/api/](e-engineer-frontend/src/shared/http/api/) | **CRIAR** este diretório | - |
| [e-engineer-frontend/src/shared/http/api/projects.ts](e-engineer-frontend/src/shared/http/api/projects.ts) | **CRIAR** ProjectsService com métodos reais | 30-50 linhas |
| [e-engineer-frontend/src/shared/http/api/auth.ts](e-engineer-frontend/src/shared/http/api/auth.ts) | **CRIAR** AuthService | 20-30 linhas |
| [e-engineer-frontend/src/shared/http/http-client.ts](e-engineer-frontend/src/shared/http/http-client.ts) | Adicionar interceptor para 401 (refresh token) | 20 linhas adição |
| [e-engineer-frontend/src/modules/projects/stores/projects.store.ts](e-engineer-frontend/src/modules/projects/stores/projects.store.ts) | Integrar com ProjectsService real | 10-15 linhas |
| [e-engineer-frontend/src/modules/dashboard/pages/DashboardPage.vue](e-engineer-frontend/src/modules/dashboard/pages/DashboardPage.vue) | Usar dados reais em vez de mock | 5-10 linhas |

---

## 🔍 MÉTRICAS DE SUCESSO

### Sprint 0 (Integração)
- ✅ Teste E2E verde: login → list projects
- ✅ 0 CORS errors em console do browser
- ✅ API integrada sem mock data
- ✅ Tests cobrindo happy path

### Sprint 1 (MVP Validado)
- ✅ Backend 60%+ code coverage
- ✅ Frontend 40%+ code coverage
- ✅ 0 console.error em fluxo principal
- ✅ Refresh token não expira durante sessão normal

### Sprint 2 (Negócio)
- ✅ 5 módulos principais implementados
- ✅ 80%+ backend coverage
- ✅ 60%+ frontend coverage

### Sprint 3 (Produção)
- ✅ Responsivo em mobile
- ✅ < 3s carregamento principal
- ✅ 0 critical issues

---

## 📚 DOCUMENTAÇÃO DE SUPORTE

### Ler Primeiro (Ordem)
1. **[master.md](master.md)** (Arquitetura + Princípios)
2. **[ANALISE-MVP-2026-05-25.md](ANALISE-MVP-2026-05-25.md)** (Análise técnica profunda)
3. **Este arquivo** (ROADMAP-GLOBAL.md)
4. **[QUICK-START-FASE1.md](QUICK-START-FASE1.md)** (Checklist tático)

### Referência Técnica
- **Backend:** [e-engineer-backend/docs/AUTH.md](e-engineer-backend/docs/AUTH.md)
- **Frontend:** [e-engineer-frontend/docs/AUTH-FRONTEND.md](e-engineer-frontend/docs/AUTH-FRONTEND.md)
- **Database:** [e-engineer-backend/docs/database-setup.md](e-engineer-backend/docs/database-setup.md)
- **Setup:** [e-engineer-backend/README.md](e-engineer-backend/README.md)

### QA & Validação
- Será criado documento separado com passos de teste manual
- Será criado documento separado com suite E2E

---

## 🤝 DIVISÃO DE TRABALHO

### Recomendado: 2 Devs em Paralelo

**Dev 1 - Backend Focus**
- Sprint 0: Validar CORS + db:seed + error handling
- Sprint 1: Refresh token + testes 60%+
- Sprint 2: Deliverables + Documents + Reviews
- Sprint 3: Monitoring + Performance

**Dev 2 - Frontend Focus**
- Sprint 0: Frontend Services Layer + E2E tests
- Sprint 1: Loading states + error messages + testes 40%+
- Sprint 2: UI para novos módulos + componentes reutilizáveis
- Sprint 3: Vuetify integration + responsividade

**Ambos:**
- Daily standup (15min)
- Code review (pair programming em críticos)
- QA testing de features prontas

---

## 💡 PRÓXIMOS PASSOS IMEDIATOS

### Hoje (Dentro de 24h)
```bash
# 1. Criar branch de trabalho
git checkout -b feat/sprint0-integration

# 2. Começar pelo #1: Frontend Services
# → Criar src/shared/http/api/projects.ts
# → Implementar ProjectsService

# 3. Seguir para #2: CORS
# → main.ts enableCors()

# 4. Testar integração
# → docker-compose up
# → Login com seed user
# → Listar projetos

# 5. Criar teste E2E básico
# → Validar fluxo completo
```

### Semana
- Completar Sprint 0 (18-24h de trabalho)
- Iniciar Sprint 1 (em paralelo, iterativo)
- Feedback de stakeholders

### Próximas Semanas
- Sprint 1 completado (MVP validado)
- Sprint 2 iniciado (módulos negócio)
- Preparar beta para usuários piloto

---

## 🎯 VISÃO DE SUCESSO

Uma plataforma SaaS para Engenharia Civil que:

1. **MVP Funcional (Fim de maio)**
   - ✅ Usuários conseguem fazer login
   - ✅ Listar, criar, ver detalhes de projetos
   - ✅ Sessão persiste durante trabalho normal
   - ✅ Erros tratados elegantemente

2. **Primeiro Release (Meados de junho)**
   - ✅ Gerenciar entregáveis
   - ✅ Upload de documentos
   - ✅ Workflow de revisões
   - ✅ Conhecimento compartilhado
   - ✅ Auditoria completa

3. **Production-Ready (Fim de junho)**
   - ✅ Responsivo em mobile
   - ✅ Performance otimizada
   - ✅ Monitored + Alertado
   - ✅ Backup automático
   - ✅ Pronto para escalar

---

**Mantido por:** Tim de Desenvolvimento  
**Última atualização:** 26 de maio de 2026  
**Próxima revisão:** 30 de maio de 2026 (após Sprint 0)

---

## Apêndice A: Checklist Teste Manual MVP

### Login Flow
- [ ] Abrir localhost:5173
- [ ] Página redireciona para /login
- [ ] Submeter credenciais seed user
- [ ] Token salvo em localStorage
- [ ] Redirecionado para /dashboard
- [ ] Dashboard mostra projetos do banco

### Projects Flow
- [ ] Dashboard lista projetos reais
- [ ] Clicar em projeto abre detalhe
- [ ] Botão "Create Project" abre form
- [ ] Submeter novo projeto
- [ ] Projeto aparece na lista
- [ ] Atualizar página, projeto ainda lá

### Logout Flow
- [ ] Logout button limpa localStorage
- [ ] Redirecionado para /login
- [ ] Token removido
- [ ] Dashboard inacessível

### Error Handling
- [ ] Login com senha errada → erro legível
- [ ] Criar projeto sem nome → erro validação
- [ ] Network offline → mensagem apropriada
- [ ] Token expirado → prompt renovar ou login

---

## Apêndice B: Stack Técnico Validado

| Layer | Tech | Versão | Status |
|-------|------|--------|--------|
| Backend | NestJS | 11.0 | ✅ Validado |
| Language | TypeScript | 5.7 | ✅ Validado |
| ORM | TypeORM | 1.0 | ✅ Validado |
| Database | PostgreSQL | 17 | ✅ Validado |
| Frontend | Vue | 3.5 | ✅ Validado |
| State | Pinia | 3.0 | ✅ Validado |
| HTTP | Axios | 1.16 | ✅ Validado |
| Testing | Jest | 30.0 | ✅ Configurado |
| Testing | Vitest | 4.1 | ✅ Configurado |
| Container | Docker | Latest | ✅ Configurado |
| Package Manager | npm | 11+ | ✅ Validado |

---

## Apêndice C: Diagrama de Domínio MVP

```
┌────────────────────────────────────────────────┐
│             E-ENGINEER DOMAIN V1                │
├────────────────────────────────────────────────┤
│                                                 │
│  User              Organization    Project      │
│  ├─ email          ├─ name         ├─ name     │
│  ├─ password       ├─ cnpj         ├─ type     │
│  └─ name           └─ address      ├─ status   │
│                                    └─ timeline │
│                                                 │
│  N:M relationship: User ↔ Organization         │
│  1:N relationship: Organization → Project      │
│                                                 │
│  Future: Deliverables, Documents, Reviews      │
│                                                 │
└────────────────────────────────────────────────┘
```
