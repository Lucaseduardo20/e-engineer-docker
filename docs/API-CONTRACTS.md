# API Contracts - Dashboard

Todas as respostas REST novas seguem envelope:

```json
{ "data": {}, "meta": {} }
```

Erros seguem:

```json
{ "code": "BadRequestException", "message": "Mensagem legivel", "details": {} }
```

## Modelos TypeScript

```ts
interface User {
id: string;
fullName: string;
email: string;
avatarUrl?: string | null;
roles: string[]; // e.g. ['admin','manager']
isPlatformAdmin?: boolean;
impersonatedBy?: string | null;
organizationId?: string;
}

interface Organization {
id: string;
name: string;
slug: string;
logoUrl?: string | null;
parentId?: string | null;
}

interface Project {
id: string;
name: string;
description?: string;
client?: string | null;
projectType?: string | null;
responsibleName?: string | null;
status: 'draft' | 'active' | 'paused' | 'completed' | 'archived';
organizationId: string;
startDate?: string; // ISO date
endDate?: string; // ISO date
progress: number; // 0-100
tags?: string[];
metrics?: Record<string, number>;
}

interface Deliverable {
id: string;
projectId: string;
title: string;
description?: string;
dueDate?: string;
status: 'todo'|'in_progress'|'done'|'blocked';
type: 'technical_survey'|'architectural_project'|'structural_project'|'electrical_project'|'hydraulic_project'|'drainage_project'|'paving_project'|'landscaping_project'|'lighting_project'|'descriptive_memorial'|'budget'|'schedule'|'art_rrt'|'photographic_report'|'technical_report'|'other';
assignees: string[]; // user ids
tagIds?: string[];
tags?: { id: string; name: string; slug: string; category: string; status: string }[];
attachments?: { url: string; name: string }[];
}

interface Paginated<T> {
items: T[];
total: number;
page: number;
pageSize: number;
}

type PriorityTargetType = 'project' | 'deliverable' | 'review' | 'document';
type PriorityLevel = 'normal' | 'high' | 'urgent';
type PriorityRequestStatus = 'requested' | 'applied' | 'rejected';

interface PriorityRequest {
id: string;
organizationId: string;
targetType: PriorityTargetType;
targetId: string;
requestedBy: string;
requestedForUserId?: string | null;
priority: PriorityLevel;
reason?: string | null;
status: PriorityRequestStatus;
decidedBy?: string | null;
decidedAt?: string | null;
createdAt: string;
updatedAt: string;
}

type TechnicalTagCategory = 'project_type' | 'technical_discipline' | 'document_type' | 'operational_pain' | 'client_context' | 'project_stage' | 'knowledge_purpose';
type TechnicalTagStatus = 'active' | 'pending_review' | 'deprecated' | 'archived';

interface TechnicalTag {
id: string;
organizationId: string;
name: string;
slug: string;
category: TechnicalTagCategory;
description?: string | null;
status: TechnicalTagStatus;
usageCount: number;
createdBy: string;
updatedBy?: string | null;
createdAt: string;
updatedAt: string;
archivedAt?: string | null;
deprecatedAt?: string | null;
}
```

## Exemplo JSON

```json
{
"items": [{ "id":"p1","name":"Projeto X","status":"active","organizationId":"o1","progress":42 }],
"total": 1,
"page": 1,
"pageSize": 20
}
```

Envelope real do endpoint:

```json
{
  "data": {
    "items": [{ "id": "p1", "name": "Projeto X", "status": "active", "organizationId": "o1", "progress": 42 }],
    "total": 1,
    "page": 1,
    "pageSize": 20
  }
}
```

## Endpoints

- `POST /auth/login` retorna `{ data: { token, user } }`.
- `POST /auth/refresh` retorna `{ data: { token } }`.
- `POST /auth/switch-tenant` permite super-admin trocar o tenant ativo e retorna `{ data: { token, user } }`.
- `POST /auth/impersonate` permite super-admin incorporar usuario de tenant e retorna `{ data: { token, user } }`.
- `GET /organizations` lista tenants para super-admin.
- `GET /organizations/current` retorna a organizacao autenticada.
- `PATCH /organizations/current` atualiza nome/razao social/logo URL da organizacao autenticada.
- `POST /organizations/current/logo` atualiza logo via `multipart/form-data` campo `file`.
- `GET /organizations/current/users` retorna usuarios da organizacao.
- `POST /organizations/current/users` cria colaborador no tenant autenticado.
- `PATCH /organizations/current/users/:userId` atualiza nome, email, senha, papel e avatar URL de colaborador.
- `POST /organizations/current/users/:userId/avatar` atualiza foto via `multipart/form-data` campo `file`.
- `POST /organizations/current/users/:userId/clone` clona role/avatar basicos exigindo novo nome, email e senha.
- `GET /priority-requests` lista solicitacoes/aplicacoes de prioridade do tenant.
- `POST /priority-requests` cria solicitacao de prioridade para projeto, revisao ou documento.
- `POST /priority-requests/:id/apply` aplica prioridade pendente.
- `POST /priority-requests/:id/reject` rejeita prioridade pendente.
- `GET /projects?page=1&pageSize=20` retorna projetos paginados.
- `POST /projects/recommend-bases` recebe `{ tagIds, limit? }` e retorna projetos base recomendados por tags tecnicas do projeto, entregaveis, documentos e KnowledgeItems vinculados, com tags combinadas, score de aderencia, preview de entregaveis, documentos e contagem de revisoes.
- `GET /projects/:id` retorna detalhe do projeto.
- `POST /projects/from-base` cria projeto a partir de projeto existente do mesmo tenant. Aceita `inheritTags`, `inheritDeliverables` e `deliverablesToInherit`.
- `GET /projects/:id/technical-profile` retorna contexto tecnico consolidado com tags, score e fontes.
- `GET /projects/:id/knowledge/recommendations` retorna recomendacoes contextuais de KnowledgeItems com `type`, `score`, `matchedTags`, `reason` e `alreadyApplied`.
- `GET /projects/:id/knowledge` retorna KnowledgeItems aplicados ao projeto e aos entregaveis do projeto, incluindo `targetType` e `targetId`.
- `GET /projects/:id/knowledge/recommendations` retorna KnowledgeItems publicados recomendados por tags tecnicas dos entregaveis do projeto, com `matchedTags`, `score` e `reason`.
- `GET /deliverables?projectId=<uuid>` retorna entregaveis.
- `GET /deliverables/:id` retorna detalhe do entregavel.
- `POST /projects` cria projeto usando organizationId do usuario autenticado; aceita `baseProjectId` opcional para copiar entregaveis/tags/documentos/versoes/revisoes do projeto base sem responsaveis/revisores no novo projeto.
- `POST /deliverables` cria entregavel usando organizationId do usuario autenticado.
- `PATCH /deliverables/:id` atualiza campos editaveis do entregavel.
- `GET /documents` retorna documentos e revisao oficial.
- `GET /reviews` retorna revisoes.
- `POST /knowledge-base` cria item da base de conhecimento.
- `GET /knowledge-base?type=&status=&tags=&page=&pageSize=` lista itens da base.
- `GET /knowledge-base/search?q=...` busca itens publicados da base.
- `GET /knowledge-base/:id` retorna detalhe com relacoes e anexos.
- `PATCH /knowledge-base/:id` atualiza campos editaveis.
- `POST /knowledge-base/:id/publish` publica item em rascunho.
- `POST /knowledge-base/:id/archive` arquiva item.
- `POST /knowledge-base/:id/relations` cria relacao generica com outro alvo do tenant.
- `POST /projects/:projectId/knowledge` vincula KnowledgeItem ao projeto; aceita `deliverableId` opcional para criar `KnowledgeRelation` com `targetType = deliverable`.
- `POST /projects/:projectId/promote-to-knowledge` promove projeto para referencia da base.
- `GET /technical-tags?search=&category=&status=&includeArchived=&page=&limit=` lista tags tecnicas do tenant com contagem de uso quando disponivel.
- `GET /technical-tags/:id` retorna detalhe da tag tecnica.
- `POST /technical-tags` cria tag tecnica no tenant autenticado.
- `PATCH /technical-tags/:id` atualiza campos editaveis da tag tecnica.
- `POST /technical-tags/:id/archive` arquiva tag tecnica sem exclusao fisica.
- `POST /technical-tags/:id/deprecate` marca tag tecnica como obsoleta sem exclusao fisica.
- `GET /audit` retorna eventos auditaveis.

Todos os endpoints, exceto login, exigem `Authorization: Bearer <token>`.
