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
status: 'draft' | 'active' | 'paused' | 'completed' | 'archived';
organizationId: string;
startDate?: string; // ISO date
endDate?: string; // ISO date
progress: number; // 0-100
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
- `GET /projects/:id` retorna detalhe do projeto.
- `GET /deliverables?projectId=<uuid>` retorna entregaveis.
- `GET /deliverables/:id` retorna detalhe do entregavel.
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
- `POST /projects/:projectId/promote-to-knowledge` promove projeto para referencia da base.
- `GET /audit` retorna eventos auditaveis.

Todos os endpoints, exceto login, exigem `Authorization: Bearer <token>`.
