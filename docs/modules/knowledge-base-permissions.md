# Permissoes da Knowledge Base

## 1. Papeis reais do projeto
`owner`, `admin`, `manager`, `project_manager`, `estimator`, `member`, `finance`.

## 2. Permissoes disponiveis
- `knowledge.create`
- `knowledge.read`
- `knowledge.update`
- `knowledge.publish`
- `knowledge.archive`
- `knowledge.deprecate`
- `knowledge.link`
- `knowledge.unlink`
- `knowledge.promote_project`
- `knowledge.save_document_model`
- `knowledge.register_lesson`

## 3. Matriz (estado atual)
- owner/admin/manager: conjunto completo acima.
- project_manager/estimator/member: create/read/update/link/promote/save/register (sem publish/archive/deprecate/unlink por padrao).
- finance: sem escrita de Knowledge Base por padrao.

## 4. UI
Acoes sensiveis sao ocultadas quando `auth.can(...)` falha (criar/publicar/arquivar/depreciar/link/unlink/promover/salvar modelo/registrar licao).

## 5. Backend
Endpoints protegidos com `PermissionsGuard` + `@RequirePermissions(...)`.

## 6. Divergencias do plano ideal
O plano menciona papeis como `coordinator/engineer/viewer`; implementacao real usa papeis acima e mapeamento equivalente de capacidade.
