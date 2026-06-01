# Prompt para Implementação do Módulo Knowledge-Base — E-Engineer Sprint 2.5

## Leitura Obrigatória (faça isso ANTES de escrever qualquer código)

Você PRECISA ler atentamente nesta ordem:
1. [`knowledge-base-module.md`](../knowledge-base-module.md) — documentação estratégica completa do módulo
2. [`master.md`](../master.md) — princípios e arquitetura do projeto
3. [`e-engineer-backend/docs/codex.md`](../e-engineer-backend/docs/codex.md) — histórico de decisões e padrões
4. [`e-engineer-frontend/codex.md`](../e-engineer-frontend/codex.md) — continuidade frontend
5. [`docs/API-CONTRACTS.md`](../docs/API-CONTRACTS.md) — contratos de API
6. [`codex-templates/implement-task.prompt.md`](./implement-task.prompt.md) — protocolo de implementação

Depois de ler, resuma em 5–7 pontos os limites arquiteturais, regras de negócio e decisões que impactam essa tarefa.

---

## Contexto do Projeto

**O que é Knowledge-Base:**
- Cérebro operacional do tenant: acervo estruturado de conhecimento técnico, padrões, modelos e referências.
- Conectado ao fluxo Projeto → Entregável → Documento → Revisão.
- Combate dispersão de conhecimento que normalmente fica em Google Drive, cabeça de pessoas, e-mails, etc.
- **Não é** wiki genérica, não é pasta de arquivos, não é clone de Notion.

**Estado atual:**
- Backend tem um módulo `knowledge-base` muito stub com apenas busca de projetos.
- Frontend tem apenas um componente `KBSearch.vue` com mock.
- Nenhuma entidade de domínio, ValueObjects ou casos de uso reais.
- Precisa ser completamente reimplementado seguindo Clean Architecture + DDD.

**Escopo desta tarefa (Sprint 2.5 — Knowledge-Base Module, 20h):**

| Task | O Que |
|------|-------|
| **KB-001** | Domain: KnowledgeItem entity + ValueObjects (type, status, tags) |
| **KB-002** | Application: Use cases (Create, List, Get, Update, Archive, Search) |
| **KB-003** | Infrastructure: TypeORM mapper + repository + relations + attachments |
| **KB-004** | Presentation: Controllers + DTOs |
| **KB-005** | Frontend: KnowledgeItemsList component (remover mock) |
| **KB-006** | Frontend: KnowledgeItemForm component (criar/editar item) |
| **KB-007** | Frontend: KnowledgeDetailsPanel component |
| **KB-008** | Tests: Unit + E2E |

---

## Decisões Arquiteturais a Validar COM O USUÁRIO

Antes de implementar, você PRECISA questionar e obter confirmação sobre:

1. **Tipos iniciais do MVP:** A documentação lista 8 tipos (`technical_standard`, `document_model`, `project_reference`, `lesson_learned`, `review_checklist`, `delivery_standard`, `zoning_rule_reference`, `project_template`). Confirmamos que iniciamos com todos esses ou reducimos para um subset?

2. **Campos "content" JSONB vs estruturado:** O campo `content` será um JSONB flexível por tipo ou criamos DTOs específicos? Qual a preferência arquitetural?

3. **Relacionamentos KnowledgeRelation:** Usar a tabela genérica `knowledge_relations` com `targetType`/`targetId`/`relationType` conforme documentação, ou criar tabelas específicas por módulo?

4. **Arquivos/Attachments:** Usar o módulo de `documents` existente ou criar sistema de attachments separado via `knowledge_attachments`?

5. **Permissões iniciais:** Usar um simples `canCreate`, `canPublish`, `canArchive` ou integrar com sistema de roles/permissions mais complexo?

6. **Status MVP:** Começamos com `draft`, `published`, `archived`, `deprecated` ou apenas `draft` e `published`?

---

## Backend — Escopo Detalhado

### 1. Domain

Criar as seguintes entidades e value objects:

**Entities:**
- `src/modules/knowledge-base/domain/entities/knowledge-item.ts`
- `src/modules/knowledge-base/domain/entities/knowledge-relation.ts`
- `src/modules/knowledge-base/domain/entities/knowledge-attachment.ts`

**Value Objects:**
- `src/modules/knowledge-base/domain/value-objects/knowledge-item-type.vo.ts` (tipos válidos: technical_standard, document_model, project_reference, lesson_learned, review_checklist, delivery_standard, zoning_rule_reference, project_template)
- `src/modules/knowledge-base/domain/value-objects/knowledge-item-status.vo.ts` (draft, published, archived, deprecated)
- `src/modules/knowledge-base/domain/value-objects/knowledge-tag.vo.ts` (normalização: lowercase, sem espaços extras, não-vazio)

**Repositories (interfaces):**
- `src/modules/knowledge-base/domain/repositories/knowledge-item.repository.ts`

**Domain Events:**
- `src/modules/knowledge-base/domain/events/knowledge-item-created.event.ts`
- `src/modules/knowledge-base/domain/events/knowledge-item-published.event.ts`
- `src/modules/knowledge-base/domain/events/knowledge-item-archived.event.ts`
- `src/modules/knowledge-base/domain/events/project-promoted-to-knowledge.event.ts`

**Invariantes e regras de negócio a validar no domínio:**
- `organizationId` é obrigatório e nunca NULL.
- `title` é obrigatório, não-vazio, máximo 180 caracteres.
- `type` deve ser um `KnowledgeItemType` válido.
- `status` deve ser um `KnowledgeItemStatus` válido.
- Novo item começa com status `draft` automaticamente.
- Tags devem ser normalizadas (lowercase, sem espaços duplos).
- Item não pode passar de `archived` para `published` sem passar por `draft` primeiro (se necessário, questione).
- `publishedAt` deve ser preenchido apenas quando status mudar para `published`.
- `archivedAt` deve ser preenchido apenas quando status mudar para `archived`.

### 2. Application (Use Cases)

Criar os seguintes use cases em `src/modules/knowledge-base/application/use-cases/`:

1. **CreateKnowledgeItemUseCase**
   - Input: `organizationId`, `createdBy`, `title`, `description`, `type`, `tags`, `content?`
   - Valida regras de domínio.
   - Cria entidade `KnowledgeItem` em `draft`.
   - Persiste e emite evento `KnowledgeItemCreated`.
   - Retorna item criado.

2. **UpdateKnowledgeItemUseCase**
   - Input: `organizationId`, `itemId`, `updatedBy`, `title`, `description`, `tags`, `content?`
   - Valida permissões e estado.
   - Atualiza campos e emite evento genérico de auditoria.

3. **PublishKnowledgeItemUseCase**
   - Input: `organizationId`, `itemId`, `publishedBy`
   - Valida que item está em `draft`.
   - Muda status para `published` e preenche `publishedAt`.
   - Emite evento `KnowledgeItemPublished`.

4. **ArchiveKnowledgeItemUseCase**
   - Input: `organizationId`, `itemId`, `archivedBy`
   - Muda status para `archived` e preenche `archivedAt`.
   - Emite evento `KnowledgeItemArchived`.

5. **ListKnowledgeItemsUseCase**
   - Input: `organizationId`, `type?`, `status?`, `tags?`, `page`, `pageSize`
   - Filtros principais: tipo, status, tags.
   - Por padrão, retorna apenas itens `published` para usuários normais (drafts apenas para owner/admin).
   - Ordenação: `updatedAt DESC`, `title ASC`.

6. **SearchKnowledgeItemsUseCase**
   - Input: `organizationId`, `query` (texto livre), `type?`, `status?`, `page`, `pageSize`
   - Busca em: `title`, `description`, `tags`, `content`.
   - Retorna itens `published` por padrão.

7. **GetKnowledgeItemDetailsUseCase**
   - Input: `organizationId`, `itemId`
   - Retorna: dados completos + relacionamentos + anexos + projetos relacionados.

8. **LinkKnowledgeItemUseCase** (criar relação genérica)
   - Input: `organizationId`, `itemId`, `targetType`, `targetId`, `relationType`, `linkedBy`
   - Cria entrada em `KnowledgeRelation`.
   - Valida que target pertence à mesma organização.

9. **PromoteProjectToKnowledgeUseCase** (caso de uso nobre)
   - Input: `organizationId`, `projectId`, `createdBy`, `title`, `description`, `tags`, `selectedDeliverableIds?`, `lessonsLearned?`, `warnings?`
   - Cria novo `KnowledgeItem` com tipo `project_reference`.
   - Cria relação com projeto de origem.
   - Pode copiar metadados de documentos/entregáveis.
   - Emite evento `ProjectPromotedToKnowledge`.

10. **UseKnowledgeItemInProjectUseCase** (registra uso)
    - Input: `organizationId`, `itemId`, `projectId`, `usedBy`
    - Cria relação `knowledge_relations` com `relationType: used_in`.

### 3. Infrastructure

**TypeORM Entities:**
- `src/modules/knowledge-base/infrastructure/persistence/typeorm/knowledge-item.orm-entity.ts`
- `src/modules/knowledge-base/infrastructure/persistence/typeorm/knowledge-relation.orm-entity.ts`
- `src/modules/knowledge-base/infrastructure/persistence/typeorm/knowledge-attachment.orm-entity.ts`

Campos sugeridos para `knowledge_items` tabela:
```sql
id (uuid, PK)
organization_id (uuid, FK to organizations, NOT NULL, indexed)
title (varchar 180, NOT NULL)
description (text)
type (varchar 40, NOT NULL, indexed)
status (varchar 40, NOT NULL, default 'draft', indexed)
tags (jsonb, array de tags normalizados)
content (jsonb, conteúdo flexível por tipo)
created_by (varchar 120)
updated_by (varchar 120)
published_at (timestamptz, nullable)
archived_at (timestamptz, nullable)
created_at (timestamptz, NOT NULL)
updated_at (timestamptz, NOT NULL)
```

Campos para `knowledge_relations` tabela:
```sql
id (uuid, PK)
organization_id (uuid, FK)
knowledge_item_id (uuid, FK to knowledge_items, indexed)
target_type (varchar 40, ex: 'project', 'deliverable', etc)
target_id (uuid, indexed)
relation_type (varchar 40, ex: 'reference_from', 'used_in', etc)
created_by (varchar 120)
created_at (timestamptz)
```

Campos para `knowledge_attachments` tabela (futura, mas criar estrutura):
```sql
id (uuid)
organization_id (uuid)
knowledge_item_id (uuid, FK)
file_id (uuid, referência a documento/arquivo)
label (varchar 120)
created_by (varchar 120)
created_at (timestamptz)
```

**Mappers:**
- `src/modules/knowledge-base/infrastructure/mappers/knowledge-item.mapper.ts`
  - Converte entre `KnowledgeItem` (domínio) e `KnowledgeItemOrmEntity` (DB).

**Repository Implementation:**
- `src/modules/knowledge-base/infrastructure/repositories/knowledge-item.repository.ts`
  - Implementa interface de repositório.
  - Métodos: `save()`, `findById()`, `findByIdWithRelations()`, `search()`, `list()`, `archive()`, `publish()`.
  - Sempre filtrar por `organizationId`.

**Migrations:**
- Criar migration para as 3 tabelas (`knowledge_items`, `knowledge_relations`, `knowledge_attachments`).
- Adicionar índices em: `organization_id`, `type`, `status`, `tags` (para JSONB search), `knowledge_item_id`.

### 4. Presentation (Controllers & DTOs)

**Controller:**
- `src/modules/knowledge-base/presentation/controllers/knowledge-base.controller.ts`

**Endpoints a expor:**
- `POST /knowledge-base` — criar item (CreateKnowledgeItemDto)
- `GET /knowledge-base?type=&status=&tags=&page=&pageSize=` — listar itens
- `GET /knowledge-base/search?q=&type=&page=` — buscar (texto livre + filtros)
- `GET /knowledge-base/:id` — detalhe do item
- `PATCH /knowledge-base/:id` — atualizar item (UpdateKnowledgeItemDto)
- `POST /knowledge-base/:id/publish` — publicar
- `POST /knowledge-base/:id/archive` — arquivar
- `POST /knowledge-base/:id/relations` — vincular relação (LinkKnowledgeItemDto)
- `POST /projects/:projectId/promote-to-knowledge` — promover projeto (PromoteProjectToKnowledgeDto)

**DTOs a criar:**
- `src/modules/knowledge-base/presentation/dto/create-knowledge-item.dto.ts`
- `src/modules/knowledge-base/presentation/dto/update-knowledge-item.dto.ts`
- `src/modules/knowledge-base/presentation/dto/link-knowledge-item.dto.ts`
- `src/modules/knowledge-base/presentation/dto/promote-project-to-knowledge.dto.ts`
- `src/modules/knowledge-base/presentation/dto/knowledge-item-response.dto.ts`
- `src/modules/knowledge-base/presentation/dto/knowledge-item-detail-response.dto.ts`

**Padrões a seguir:**
- Usar `JwtAuthGuard` em todas as rotas.
- Usar `ok()` envelope para respostas bem-sucedidas.
- Validar `organizationId` do usuário versus item/request.
- Retornar 404 se item não pertence à organização.
- Usar `ValidationPipe` global existente.

---

## Frontend — Escopo Detalhado

### 1. Estrutura de Módulo

Criar `src/modules/knowledge-base/` com:
```
knowledge-base/
  pages/
    KnowledgeBaseListPage.vue
    KnowledgeBaseDetailPage.vue
  components/
    KnowledgeItemsList.vue
    KnowledgeItemForm.vue
    KnowledgeItemCard.vue
    KnowledgeDetailsPanel.vue
  stores/
    knowledge-items.store.ts
  types/
    knowledge.types.ts
```

### 2. Rotas

Adicionar a `src/router/index.ts`:
```javascript
{
  path: '/knowledge-base',
  name: 'knowledge-base',
  component: () => import('@/modules/knowledge-base/pages/KnowledgeBaseListPage.vue'),
  meta: { title: 'Base de Conhecimento', requiresAuth: true }
},
{
  path: '/knowledge-base/:id',
  name: 'knowledge-base-detail',
  component: () => import('@/modules/knowledge-base/pages/KnowledgeBaseDetailPage.vue'),
  meta: { title: 'Detalhe do Item', requiresAuth: true }
}
```

Atualizar o link de navegação em `AuthenticatedLayout.vue` para apontar para `/knowledge-base` em vez de mock.

### 3. API Client

Estender `src/shared/http/api-client.ts` com:
```javascript
knowledgeBase: {
  list(params?: PageParams & { type?: string; status?: string; tags?: string[] }) { ... },
  search(params?: PageParams & { q?: string; type?: string }) { ... },
  get(id: string) { ... },
  create(payload: CreateKnowledgeItemDto) { ... },
  update(id: string, payload: UpdateKnowledgeItemDto) { ... },
  publish(id: string) { ... },
  archive(id: string) { ... },
  link(id: string, payload: LinkKnowledgeItemDto) { ... },
  promoteProject(projectId: string, payload: PromoteProjectToKnowledgeDto) { ... }
}
```

### 4. Componentes

**KnowledgeItemsList.vue:**
- Listagem de itens com filtros por tipo, status, tags.
- Cards ou table view.
- Cada card mostra: título, tipo (com ícone/cor), status badge, tags, última atualização.
- Ação de "Novo item" e ação de "Ver detalhes".
- Paginação.

**KnowledgeItemForm.vue:**
- Formulário reativo que muda com base no tipo selecionado.
- Campos comuns: title, description, type, tags.
- Campos específicos: conforme tipo (project_reference, lesson_learned, etc).
- Validação por Zod.
- Estados: criando, salvando, sucesso, erro.

**KnowledgeDetailsPanel.vue:**
- Exibe detalhes completos de um item.
- Seções: dados principais, conteúdo, anexos, relacionamentos, projetos usadores.
- Ações: editar, publicar, arquivar, duplicar, vincular.

### 5. Store (Pinia)

Criar `src/modules/knowledge-base/stores/knowledge-items.store.ts`:
```javascript
export const useKnowledgeItemsStore = defineStore('knowledgeItems', () => {
  const items = ref<KnowledgeItem[]>([])
  const selectedItem = ref<KnowledgeItemDetail | null>(null)
  const isLoading = ref(false)
  const error = ref<string | null>(null)
  const filters = reactive({
    type: null,
    status: 'published',
    tags: [],
    searchQuery: ''
  })

  // Actions
  async function listItems(page: number, pageSize: number) { ... }
  async function searchItems(query: string) { ... }
  async function getItemDetail(id: string) { ... }
  async function createItem(data: CreateKnowledgeItemDto) { ... }
  async function updateItem(id: string, data: UpdateKnowledgeItemDto) { ... }
  async function publishItem(id: string) { ... }
  async function archiveItem(id: string) { ... }
  // etc...

  return {
    items,
    selectedItem,
    isLoading,
    error,
    filters,
    // ...actions
  }
})
```

### 6. Tipos TypeScript

Criar `src/modules/knowledge-base/types/knowledge.types.ts`:
```typescript
export type KnowledgeItemType = 
  | 'technical_standard'
  | 'document_model'
  | 'project_reference'
  | 'lesson_learned'
  | 'review_checklist'
  | 'delivery_standard'
  | 'zoning_rule_reference'
  | 'project_template'

export type KnowledgeItemStatus = 'draft' | 'published' | 'archived' | 'deprecated'

export interface KnowledgeItem {
  id: string
  title: string
  description?: string
  type: KnowledgeItemType
  status: KnowledgeItemStatus
  tags: string[]
  createdAt: string
  updatedAt: string
  publishedAt?: string
}

export interface KnowledgeItemDetail extends KnowledgeItem {
  content?: Record<string, any>
  createdBy: string
  updatedBy: string
  relations?: KnowledgeRelation[]
  attachments?: KnowledgeAttachment[]
}

// ... outros tipos
```

---

## Testes — Obrigatórios

### Backend Testes

**Unit Tests:**
- `src/modules/knowledge-base/domain/entities/knowledge-item.spec.ts`
  - Criação válida, invariantes (título vazio, type inválido, etc).
  - Transições de estado (draft → published → archived).
  - Normalização de tags.

- `src/modules/knowledge-base/application/use-cases/create-knowledge-item.use-case.spec.ts`
  - Criar item válido.
  - Payload inválido → erro.
  - Isolamento tenant → erro se `organizationId` diferente.

- `src/modules/knowledge-base/application/use-cases/search-knowledge-items.use-case.spec.ts`
  - Busca por texto livre.
  - Busca com filtros (type, status, tags).
  - Isolamento tenant.

- `src/modules/knowledge-base/infrastructure/mappers/knowledge-item.mapper.spec.ts`
  - Conversão domínio ↔ ORM.

**Integration Tests:**
- `src/modules/knowledge-base/presentation/controllers/knowledge-base.controller.spec.ts`
  - POST `/knowledge-base` → 201 + item criado.
  - GET `/knowledge-base` → 200 + lista paginada.
  - GET `/knowledge-base/search?q=teste` → 200 + resultados.
  - POST `/knowledge-base/:id/publish` → 200 + status updated.
  - POST `/knowledge-base/:id/archive` → 200 + archived.

**E2E Básico:**
- Criar um item do tipo `technical_standard`.
- Buscar por título.
- Publicar item.
- Arquivar item.
- Promover um projeto para referência.

### Frontend Testes

**Unit Tests:**
- `src/modules/knowledge-base/components/KnowledgeItemsList.spec.ts`
  - Renderiza lista de itens.
  - Filtra por tipo.
  - Abre detalhe ao clicar em item.

- `src/modules/knowledge-base/components/KnowledgeItemForm.spec.ts`
  - Form renderiza campos comuns.
  - Ao selecionar tipo `lesson_learned`, mostra campos específicos.
  - Validação: título vazio.
  - Submit válido → cria item.

- `src/modules/knowledge-base/stores/knowledge-items.store.spec.ts`
  - `listItems()` → popula store.
  - `searchItems(query)` → filtra.
  - `createItem()` → adiciona e retorna.

**E2E:**
- Acessar `/knowledge-base` → vê listagem (ou empty state).
- Criar novo item → form aparece → preenche → submit → item criado e aparece na lista.
- Clicar em item → detalhe abre.
- Publicar item → status muda.
- Arquivar item → desaparece da listagem padrão (published).

---

## Processo de Implementação (Obrigatório)

1. **Resumo de Leitura (FAÇA PRIMEIRO):**
   - Leia `knowledge-base-module.md` completamente.
   - Leia `master.md` + `codex.md` backend + frontend.
   - Resuma em 5–7 pontos.

2. **Questões Abertas:**
   - Liste 3–5 dúvidas que você tem.
   - **PARE aqui e questione o usuário. Não prossiga sem respostas.**

3. **Proposta Arquitetural:**
   - Descreva a abordagem.
   - Liste todos os arquivos a criar/editar.
   - Explique decisões para cada ponto de questão anterior.

4. **Implementação Incremental:**
   - Implemente domain → application → infrastructure → presentation → frontend.
   - Pequenos cortes coesos (1–2 arquivos por commit).
   - Valide type-check após cada bloco.

5. **Validações Locais (OBRIGATÓRIO):**
   - `npm run type-check` — deve passar.
   - `npm run test` (backend) — deve passar.
   - `npm run test:unit` (frontend) — deve passar.
   - Cole as saídas completas.

6. **Cenários Testados Manualmente:**
   - Resuma pelo menos 5 cenários:
     1. Criar item de tipo `technical_standard` com tags.
     2. Buscar item por título (texto livre).
     3. Publicar item (muda de `draft` para `published`).
     4. Arquivar item.
     5. Promover projeto para referência (cria relação).
   - Descreva o resultado esperado versus observado.

7. **Auditoria (entry em codex.md):**
   - Data, tarefa, mudanças, decisão tomada, testes, observações.
   - Copie e cole em `e-engineer-backend/codex.md`.

8. **Relatório de Entrega:**
   - Comando de type-check, test, logs resumidos.
   - Diff de arquivos criados/alterados.
   - Sugestão de mensagem de commit.
   - Comandos para rodar localmente.

---

## Regras Críticas

- **NUNCA** use entidades TypeORM como entidades de domínio.
- **SEMPRE** filtre por `organizationId` em queries.
- **SEMPRE** valide permissões/ownership antes de atualizar/arquivar.
- Se uma decisão impactar modelo de dados, tenancy, ou contratos públicos, **QUESTIONE o usuário primeiro**.
- Se estiver em dúvida sobre escolha entre duas alternativas, escolha a mais simples e questione o usuário.
- **NUNCA** commit secrets ou credenciais.
- Commits pequenos e coerentes: um propósito por commit.

---

## Sucesso = Entrega Completa

A tarefa só fica "pronta" quando:
- ✅ Todos os arquivos domain/application/infrastructure/presentation estão implementados.
- ✅ Type-check, test, e2e passam 100%.
- ✅ Pelo menos 5 cenários foram testados manualmente e documentados.
- ✅ Frontend lista, cria, edita, publica, arquiva itens.
- ✅ KBSearch mock foi substituído por componente real.
- ✅ Entrada em `codex.md` foi adicionada.
- ✅ Mensagem de commit foi sugerida.

Use este prompt como sua bíblia. Qualquer dúvida, volte para cá e questione o usuário.
