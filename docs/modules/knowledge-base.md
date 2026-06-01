# Modulo Knowledge Base

## 1. Visao geral
A Knowledge Base e o acervo tecnico reutilizavel por tenant. Regra central: `Projetos geram conhecimento. Conhecimento melhora novos projetos.`

## 2. Papel do modulo na plataforma
Conecta projetos, documentos e revisoes ao conhecimento reutilizavel, fechando o ciclo de aprendizado operacional.

## 3. Conceitos principais
- KnowledgeItem: unidade de conhecimento.
- KnowledgeRelation: vinculo polimorfico entre item e contexto.
- ActivityLog: rastreabilidade das operacoes.

## 4. Entidades implementadas
Backend dominio/infra:
- `knowledge-item.ts`, `knowledge-relation.ts`, `knowledge-attachment.ts`
- `knowledge-item.orm-entity.ts`, `knowledge-relation.orm-entity.ts`, `knowledge-attachment.orm-entity.ts`
- mapper: `knowledge-item.mapper.ts`
- repositorio: contrato + implementacao TypeORM
Campos centrais: `organizationId`, `title`, `description`, `type`, `status`, `content`, `tags`, `createdBy`, `updatedBy`, `publishedAt`, `archivedAt`, `deprecatedAt`.

## 5. Tipos de KnowledgeItem
Implementados:
- `technical_standard`
- `document_model`
- `project_reference`
- `lesson_learned`
- `review_checklist`
- `delivery_standard`
- `zoning_rule_reference` (preparado para futuro)
- `project_template` (preparado para futuro)

## 6. Status de KnowledgeItem
- `draft`: rascunho editavel.
- `published`: oficial.
- `archived`: historico, fora do padrao de listagem.
- `deprecated`: obsoleto, ainda consultavel.

## 7. Relacoes de conhecimento
`KnowledgeRelation` com:
- relationType: `reference_for`, `based_on`, `model_for`, `lesson_from`, `standard_for`, `checklist_for`
- targetType: `project`, `deliverable`, `document`, `document_version`, `review`, `template`
No uso atual, foco principal em projeto/documento/revisao.

## 8. Fluxos implementados
1. Criacao manual.
2. Listagem/busca/filtros.
3. Detalhe.
4. Edicao.
5. Publicacao.
6. Arquivamento.
7. Depreciacao.
8. Vinculo com projeto.
9. Remocao de vinculo.
10. Promocao de projeto para referencia.
11. Documento como modelo.
12. Revisao reprovada como licao.
13. Activity log.
14. Permissoes RBAC minimas.

## 9. Regras de negocio
- Isolamento por `organizationId` em consultas/escritas.
- Estados governados por acoes especificas (nao CRUD livre de status).
- Regras de validacao em use-cases (titulo, tipo, transicao, ownership).

## 10. Multi-tenancy
`organizationId` vem do usuario autenticado (`AuthenticatedRequest`) e e aplicado em todos os use-cases do modulo.

## 11. Activity log/auditoria
Eventos relevantes sao registrados e expostos no modulo de auditoria. A UI carrega logs no detalhe de item/documento/revisao quando aplicavel.

## 12. Permissoes
Permissoes chave: `knowledge.create/read/update/publish/archive/deprecate/link/unlink/promote_project/save_document_model/register_lesson`.
Backend com `PermissionsGuard` + `@RequirePermissions`; frontend com `auth.can(...)` para esconder/bloquear acoes.

## 13. Seeds e demo flow
Ha seed e roteiro em `docs/demo/knowledge-base-demo-flow.md` com narrativa de 5-8 minutos.

## 14. Decisoes tecnicas
- Separacao dominio x ORM.
- Relacoes polimorficas por `targetType/targetId`.
- Fluxos orientados a negocio (promote/save-as-model/register-lesson).
- RBAC backend + enforcement visual no frontend.

## 15. Limitacoes conhecidas
- Sem busca semantica/embeddings.
- Sem versionamento de KnowledgeItem publicado.
- Sem workflow formal de aprovacao multi-etapa.
- Algumas relacoes futuras existem no modelo, mas nao estao totalmente exploradas na UI.

## 16. Proximos passos
- Recomendacao por tags/contexto.
- Health score tecnico do projeto.
- Busca semantica por tenant.
- Versionamento de itens publicados.
- Workflow de aprovacao e governanca avancada.
