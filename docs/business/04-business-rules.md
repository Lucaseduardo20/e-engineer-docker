# 04 — Regras de Negócio

## 1. Objetivo deste documento

Este documento descreve regras de negócio que devem orientar backend, frontend, validações, casos de uso, permissões e UX.

As regras aqui descritas representam o comportamento ideal da plataforma. Nem todas precisam ser implementadas imediatamente, mas devem servir como norte para criação de tarefas e evolução do produto.

## 2. Regras gerais de multi-tenancy

### REG-001 — Todo dado de negócio pertence a uma organização

Toda entidade operacional deve possuir `organizationId` ou relação direta com uma entidade que possua `organizationId`.

Entidades afetadas:

- Project;
- Deliverable;
- Document;
- DocumentVersion;
- Review;
- KnowledgeItem;
- ActivityLog;
- Template;
- FeasibilityStudy.

### REG-002 — Usuário só acessa dados da organização ativa

Toda consulta deve filtrar por organização ativa. Nenhum endpoint deve retornar dados de outra organização.

### REG-003 — Trocar tenant muda o contexto de todos os módulos

Ao trocar o tenant ativo, dashboard, projetos, documentos, revisões, base de conhecimento e colaboradores devem refletir apenas o tenant selecionado.

### REG-004 — Operações críticas devem registrar ator

Ações relevantes devem registrar quem executou:

- criação de projeto;
- envio de documento;
- marcação de versão oficial;
- solicitação de revisão;
- aprovação/reprovação;
- publicação de conhecimento;
- promoção de projeto como referência.

## 3. Regras de usuários e permissões

### REG-010 — Usuário precisa ser membro ativo para acessar organização

Um usuário autenticado só pode acessar uma organização se possuir Membership ativa.

### REG-011 — Papéis iniciais

Papéis recomendados:

- owner;
- admin;
- coordinator;
- engineer;
- designer;
- viewer.

### REG-012 — Owner possui controle total

Owner pode:

- gerenciar organização;
- gerenciar colaboradores;
- criar/editar/excluir projetos;
- publicar conhecimento;
- arquivar itens;
- aprovar revisões, se estiver no fluxo.

### REG-013 — Viewer não altera dados

Viewer pode apenas visualizar dados permitidos.

### REG-014 — Publicação de conhecimento deve exigir permissão

Publicar item de conhecimento deve ser permitido apenas para papéis com responsabilidade técnica/administrativa:

- owner;
- admin;
- coordinator.

Engineers podem criar rascunhos, mas publicação pode depender de aprovação.

## 4. Regras de projeto

### REG-100 — Projeto deve pertencer a uma organização

Nenhum projeto pode existir sem organizationId.

### REG-101 — Projeto deve ter nome

Nome é obrigatório.

### REG-102 — Projeto deve ter status

Todo projeto deve possuir status operacional.

### REG-103 — Projeto pode ter responsável técnico

Responsável técnico é recomendado, mas pode ser opcional no rascunho.

### REG-104 — Projeto pode ter cliente/prefeitura

Cliente ajuda contexto, busca, relatório e filtros.

### REG-105 — Progresso do projeto pode ser calculado pelos entregáveis

Progresso ideal:

```text
entregáveis concluídos / total de entregáveis
```

Mas pode considerar pesos futuros.

### REG-106 — Projeto concluído deve possuir entregáveis fechados

Para marcar projeto como concluído, idealmente:

- entregáveis principais concluídos;
- documentos oficiais presentes;
- revisões pendentes resolvidas.

No MVP, isso pode ser alerta, não bloqueio.

### REG-107 — Projeto pode ser promovido para Base de Conhecimento

Projeto finalizado ou maduro pode virar `KnowledgeItem` do tipo `project_reference`.

### REG-108 — Projeto pode usar itens de conhecimento

Projeto pode se vincular a padrões, documentos modelo, projetos de referência, lições aprendidas e checklists.

### REG-109 — Projeto sem template aplicado deve gerar alerta opcional

Sistema pode alertar:

> Este projeto ainda não possui template ou padrão aplicado.

## 5. Regras de entregáveis

### REG-200 — Entregável pertence a um projeto

Nenhum entregável deve existir sem projectId.

### REG-201 — Entregável deve ter título

Título é obrigatório.

### REG-202 — Entregável deve ter status

Status é obrigatório.

Status recomendados:

- to_produce;
- in_production;
- blocked;
- in_review;
- completed;
- overdue.

### REG-203 — Entregável bloqueado deve ter motivo

Quando um entregável for marcado como bloqueado, o sistema deve solicitar motivo.

### REG-204 — Entregável pode ter responsável

Responsável ajuda coordenação e cobrança.

### REG-205 — Entregável concluído deve possuir evidência técnica

Idealmente, entregável concluído deve ter:

- documento oficial; ou
- revisão aprovada; ou
- justificativa.

No MVP, isso pode ser aviso.

### REG-206 — Entregáveis podem ser gerados por template

Ao aplicar template, o sistema pode gerar entregáveis padrão.

### REG-207 — Alteração de status deve registrar atividade

Mudanças relevantes de status devem gerar ActivityLog.

## 6. Regras de documentos

### REG-300 — Documento deve pertencer a uma organização

Documento precisa respeitar organizationId.

### REG-301 — Documento deve pertencer a um projeto

Documento sem projeto perde contexto técnico.

### REG-302 — Documento deve idealmente pertencer a um entregável

Documento vinculado a entregável melhora rastreabilidade.

### REG-303 — Documento deve ter título

Título é obrigatório.

### REG-304 — Documento deve ter tipo

Tipo ajuda filtros, templates e conhecimento.

Tipos recomendados:

- memorial_descritivo;
- projeto_arquitetonico;
- projeto_estrutural;
- projeto_eletrico;
- projeto_hidraulico;
- orcamento;
- cronograma;
- art_rrt;
- relatorio_tecnico;
- relatorio_fotografico;
- calculo_materiais;
- estudo_viabilidade.

### REG-305 — Documento pode ter status

Status recomendados:

- draft;
- under_review;
- official;
- rejected;
- archived.

### REG-306 — Documento oficial deve possuir versão oficial

Um documento marcado como oficial precisa ter pelo menos uma DocumentVersion oficial.

### REG-307 — Documento não deve apagar histórico facilmente

Excluir documento deve ser controlado. Preferência futura: arquivar em vez de excluir.

## 7. Regras de versões

### REG-400 — Documento pode ter múltiplas versões

Cada envio novo deve criar uma DocumentVersion.

### REG-401 — Versão deve ter arquivo ou metadado de arquivo

No MVP, pode existir metadado fake. Em produção, deve possuir arquivo armazenado.

### REG-402 — Versão deve registrar autor

uploadedBy é obrigatório.

### REG-403 — Versão deve registrar data

uploadedAt é obrigatório.

### REG-404 — Apenas uma versão oficial por documento

Quando uma versão for marcada como oficial, outras versões do mesmo documento devem deixar de ser oficiais.

### REG-405 — Marcar versão oficial deve ser auditável

Registrar:

- quem marcou;
- quando marcou;
- versão anterior;
- versão nova;
- motivo opcional.

### REG-406 — Código de revisão é recomendado

Exemplos:

- R00;
- R01;
- R02;
- V1;
- V2.

### REG-407 — Versão reprovada não deve ser oficial

Se uma versão for reprovada em revisão, ela não deve ser marcada como oficial sem nova decisão.

## 8. Regras de revisão

### REG-500 — Revisão deve possuir alvo

Uma revisão deve estar vinculada a pelo menos um destes:

- projeto;
- entregável;
- documento;
- versão de documento.

### REG-501 — Revisão deve possuir revisor

reviewerId é obrigatório para revisão formal.

### REG-502 — Revisão deve ter status

Status recomendados:

- pending;
- approved;
- rejected;
- overdue;
- canceled.

### REG-503 — Reprovação exige comentário

Toda revisão reprovada deve ter motivo.

### REG-504 — Aprovação pode ter comentário opcional

Comentário é opcional, mas recomendado.

### REG-505 — Revisão atrasada deve aparecer em alertas

Revisões vencidas devem alimentar dashboard e saúde técnica.

### REG-506 — Revisão reprovada pode sugerir lição aprendida

O sistema deve sugerir:

> Deseja registrar este problema como lição aprendida?

### REG-507 — Revisão aprovada pode permitir versão oficial

Se uma versão for aprovada, sistema pode sugerir marcá-la como oficial.

## 9. Regras da Base de Conhecimento

### REG-600 — KnowledgeItem pertence a uma organização

Todo item de conhecimento é específico do tenant.

### REG-601 — KnowledgeItem deve ter tipo

Tipos iniciais:

- technical_standard;
- document_model;
- project_reference;
- lesson_learned;
- review_checklist;
- delivery_standard.

### REG-602 — KnowledgeItem deve ter status

Status:

- draft;
- published;
- archived;
- deprecated.

### REG-603 — Apenas itens publicados devem aparecer como recomendação padrão

Rascunhos podem aparecer apenas para autores/admins.

### REG-604 — Itens arquivados não devem ser recomendados

Arquivados ficam preservados, mas fora do fluxo normal.

### REG-605 — Itens depreciados devem alertar usuário

Se item deprecated for aberto, mostrar aviso.

### REG-606 — KnowledgeItem pode se relacionar com projetos

Relações possíveis:

- reference_from;
- used_in;
- generated_from;
- recommended_for.

### REG-607 — Projeto pode gerar KnowledgeItem

Projeto finalizado pode ser promovido para item do tipo project_reference.

### REG-608 — Documento oficial pode gerar modelo

Documento oficial pode ser salvo como document_model.

### REG-609 — Revisão reprovada pode gerar lesson_learned

Reprovações recorrentes devem alimentar aprendizado.

### REG-610 — KnowledgeItem deve possuir tags

Tags são importantes para busca e recomendação.

## 10. Regras de recomendações

### REG-700 — Recomendações iniciais podem ser baseadas em tags

Não é necessário IA no início.

Exemplo:

```text
Projeto tag UBS → recomenda KnowledgeItems tag UBS.
```

### REG-701 — Tipo de projeto deve influenciar recomendação

Projeto de pavimentação recomenda itens de pavimentação.

### REG-702 — Tipo de entregável deve influenciar recomendação

Entregável orçamento recomenda padrões de orçamento.

### REG-703 — Recomendações devem ser explicáveis

Mostrar motivo:

> Recomendado porque possui a tag UBS.

## 11. Regras de Activity Log

### REG-800 — Eventos importantes devem gerar ActivityLog

Eventos mínimos:

- project.created;
- project.status_changed;
- deliverable.created;
- deliverable.status_changed;
- document.created;
- document_version.uploaded;
- document_version.marked_official;
- review.requested;
- review.approved;
- review.rejected;
- knowledge_item.published;
- project.promoted_to_knowledge.

### REG-801 — ActivityLog deve respeitar organização

Todo log precisa de organizationId.

### REG-802 — ActivityLog deve conter metadata

Metadata permite mostrar detalhes no dashboard.

## 12. Regras de saúde técnica

### REG-900 — Saúde técnica pode ser calculada por sinais

Sinais negativos:

- entregável atrasado;
- entregável bloqueado;
- revisão vencida;
- documento sem versão oficial;
- revisão reprovada;
- projeto sem responsável;
- projeto sem template;
- projeto sem conhecimento vinculado.

### REG-901 — Classificação inicial

- Boa;
- Atenção;
- Crítica.

### REG-902 — Saúde deve mostrar motivos

Não basta mostrar score. Usuário precisa saber por quê.

## 13. Regras de viabilidade urbanística futura

### REG-1000 — Estudo de viabilidade deve preservar fonte

Todo resultado deve ter:

- fonte;
- data de consulta;
- versão/base;
- observação de apoio técnico.

### REG-1001 — Estudo pode gerar projeto

FeasibilityStudy pode originar Project.

### REG-1002 — Resultado não substitui responsabilidade técnica

Interface e relatório devem informar que o resultado é apoio preliminar.

## 14. Princípio de validação

Sempre que o sistema permitir uma ação que impacta rastreabilidade, deve responder:

- quem fez?
- quando fez?
- em qual organização?
- em qual projeto?
- qual item foi afetado?
- qual era o estado anterior?
- qual é o novo estado?

Esse princípio evita que a plataforma vire um Drive com botões.
