# Knowledge Base API (Estado Implementado)

## POST /knowledge-base
Permissao: `knowledge.create`.
Objetivo: criar item. Erros: 400, 404.

## GET /knowledge-base
Permissao: `knowledge.read`.
Objetivo: listar com filtros (`type/status/tags/page/pageSize/includeArchived`).

## GET /knowledge-base/search
Permissao: `knowledge.read`.
Objetivo: busca textual (`q`) com filtros.

## GET /knowledge-base/:id
Permissao: `knowledge.read`.
Objetivo: detalhe do item.

## PATCH /knowledge-base/:id
Permissao: `knowledge.update`.
Objetivo: editar item.

## POST /knowledge-base/:id/publish
Permissao: `knowledge.publish`.
Objetivo: publicar item draft.

## POST /knowledge-base/:id/archive
Permissao: `knowledge.archive`.
Objetivo: arquivar item.

## POST /knowledge-base/:id/deprecate
Permissao: `knowledge.deprecate`.
Objetivo: marcar obsoleto.

## POST /knowledge-base/:id/relations
Permissao: `knowledge.link`.
Objetivo: criar relacao.

## POST /knowledge-base/:id/relations/:relationId/remove
Permissao: `knowledge.unlink`.
Objetivo: remover relacao.

## GET /projects/:id/knowledge
Permissao: `knowledge.read`.
Objetivo: listar conhecimento aplicado ao projeto.

## POST /projects/:id/knowledge
Permissao: `knowledge.link`.
Objetivo: vincular item ao projeto.

## POST /projects/:id/knowledge/:relationId/remove
Permissao: `knowledge.unlink`.
Objetivo: remover vinculo do projeto.

## POST /projects/:projectId/promote-to-knowledge
Permissao: `knowledge.promote_project`.
Objetivo: criar `project_reference` a partir de projeto.

## POST /documents/:id/save-as-model
Permissao: `knowledge.save_document_model`.
Objetivo: salvar documento como `document_model`.

## POST /documents/:id/versions/:versionId/save-as-model
Permissao: `knowledge.save_document_model`.
Objetivo: salvar versao oficial como `document_model`.

## POST /reviews/:id/register-lesson-learned
Permissao: `knowledge.register_lesson`.
Objetivo: registrar `lesson_learned`.

## Autenticacao e erros
- Auth: JWT bearer.
- Autorizacao: `PermissionsGuard` + `@RequirePermissions`.
- Erros comuns: `400` (regra de negocio), `403` (sem permissao), `404` (nao encontrado no tenant).
