# Cenarios de Teste - Knowledge Base

## Como usar
Executar por task, validando UI + API + banco + tenant.

## Pre-requisitos
- Seed executada.
- Usuarios com perfis diferentes.
- Backend/frontend em execucao.

## Task 1-17 (resumo objetivo)

## Task 1 - Dominio base
1.1 Validar tipos/status no dominio. 1.2 Item nasce `draft`. 1.3 Exige `organizationId`, titulo e tipo valido.

## Task 2 - Persistencia/seeds
2.1 Migration cria estruturas KB. 2.2 Seed popula itens realistas sem duplicar criticamente por tenant.

## Task 3 - Criacao manual
3.1 Criar item pela UI. 3.2 Validar obrigatorios. 3.3 Item aparece em listagem como `draft`.

## Task 4 - Listagem/filtros
4.1 Busca por texto/tags. 4.2 Filtro por tipo/status. 4.3 `archived` oculto por padrao.

## Task 5 - Detalhe
5.1 Abrir item e conferir campos completos. 5.2 Bloqueio cross-tenant.

## Task 6 - Edicao
6.1 Atualizar campos. 6.2 Item arquivado nao editavel.

## Task 7 - Publicar/arquivar/depreciar
7.1 Publicar draft. 7.2 Arquivar oculta da listagem padrao. 7.3 Depreciar published.

## Task 8 - Relacoes
8.1 Vincular item-projeto. 8.2 Nao duplicar relacao identica. 8.3 Remover vinculo.

## Task 9 - KB no projeto
9.1 Secao de conhecimento aplicado aparece. 9.2 Empty state. 9.3 Link para detalhe funciona.

## Task 10 - Promover projeto
10.1 Modal e validacoes. 10.2 Cria `project_reference` draft. 10.3 Relacao de origem criada.

## Task 11 - Documento como modelo
11.1 Acao no card/menu. 11.2 Fluxo cria `document_model`. 11.3 Relacao com documento/versao.

## Task 12 - Revisao como licao
12.1 Acao em revisao rejeitada. 12.2 Cria `lesson_learned`. 12.3 Contexto de origem preservado.

## Task 13 - Cards ricos
13.1 Card exibe tipo/status/metadados. 13.2 Estados vazios e loading.

## Task 14 - Detalhe contextual
14.1 Conteudo contextual por tipo (referencia/modelo/licao/checklist/padrao).

## Task 15 - Seeds/demo
15.1 Roteiro de demo coerente. 15.2 Itens-chave visiveis.

## Task 16 - Activity log
16.1 Eventos de create/publish/archive/deprecate/link/promote/save/register aparecem em auditoria.

## Task 17 - Permissoes
17.1 Backend retorna 403 sem permissao. 17.2 UI oculta acoes sem permissao. 17.3 Tenant isolado.

## Teste E2E manual - Demo
1. Login admin.
2. Abrir projeto UBS.
3. Ver conhecimento aplicado.
4. Abrir licao aprendida e origem.
5. Ir para Base de Conhecimento e filtrar `document_model`.
6. Abrir modelo e conferir relacoes.

## Checklist final
- Fluxos 1-12 funcionando.
- Auditoria visivel.
- RBAC coerente front/back.
- Sem vazamento entre tenants.
