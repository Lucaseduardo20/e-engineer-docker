# Historico de Desenvolvimento

## 2026-05-26 - Dashboard integrado

- Adicionados contratos TypeScript compartilhados para dashboard.
- Backend exposto com endpoints REST para auth, organizations, projects, deliverables, documents, reviews, knowledge-base e audit.
- Respostas novas padronizadas em envelope `{ data }`.
- Erros HTTP normalizados em `{ code, message, details? }`.
- Swagger habilitado em `/docs/api`.
- Frontend migrado para AppShell Vuetify com dashboard integrado ao backend.
- Criados client API tipado, stores Pinia de projects/ui e componentes ProjectsList, ProjectDetail, DeliverablesBoard, OrgSwitcher, KBSearch, ReviewsPanel, NotificationsFeed e AdminUsers.
- Adicionados testes mínimos para listagem de projetos no backend e renderizacao de ProjectsList no frontend.
