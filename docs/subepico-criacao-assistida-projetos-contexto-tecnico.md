# Subepico: Criacao assistida de projetos por contexto tecnico

## Tese

A e-engineer nao comeca um projeto do zero. Ela comeca com a inteligencia acumulada da empresa.

Este subepico conecta tags governadas, projetos base, entregaveis, documentos, KnowledgeItems, perfil tecnico e recomendacoes para transformar a criacao de projeto em uma experiencia assistida por contexto tecnico.

## O que esta implementado

- Wizard de novo projeto com dados basicos, tags governadas, sugestoes, ponto de partida, revisao de entregaveis e confirmacao.
- Tags governadas em Project, Deliverable e Document.
- Recomendacao de projetos base por tags tecnicas.
- Criacao a partir de projeto base.
- Heranca seletiva de entregaveis.
- Banner de revisao de entregaveis herdados no cockpit.
- Fluxo auditavel para solicitar/remover entregavel herdado com motivo e aprovacao.
- ProjectTechnicalProfile consolidando tags de projeto, entregaveis e documentos.
- Recomendacoes contextuais de KnowledgeItems no cockpit com score, tags combinadas, motivo e estado `alreadyApplied`.
- Seeds de demo para UBS, reforma escolar, documentos, revisoes, KnowledgeItems e tags tecnicas.

## Entidades e tabelas envolvidas

- `projects`
- `project_tags`
- `project_base_relations`
- `deliverables`
- `deliverable_tags`
- `deliverable_base_relations`
- `deliverable_removal_requests`
- `documents`
- `document_versions`
- `document_tags`
- `reviews`
- `knowledge_items`
- `knowledge_item_tags`
- `knowledge_relations`
- `technical_tags`
- `activity_logs`

## Endpoints principais

- `POST /projects`
- `POST /projects/from-base`
- `POST /projects/recommend-bases`
- `POST /projects/similar`
- `GET /projects/:id/technical-profile`
- `GET /projects/:id/knowledge/recommendations`
- `GET /projects/:id/knowledge`
- `POST /projects/:id/knowledge`
- `DELETE /projects/:id/knowledge/:relationId`
- `PATCH /deliverables/:id/inheritance-review`
- `POST /deliverables/:id/removal-requests`
- `POST /deliverables/removal-requests/:id/approve`
- `POST /deliverables/removal-requests/:id/reject`

## Fluxo funcional

1. Usuario abre `Novo projeto`.
2. Informa nome e tipo tecnico.
3. Seleciona tags governadas no `TechnicalTagSelector`.
4. Plataforma busca projetos semelhantes do mesmo tenant.
5. Usuario escolhe:
   - comecar do zero; ou
   - usar projeto existente como base.
6. Se usar base, revisa entregaveis a herdar.
7. Confirma criacao.
8. Plataforma redireciona ao cockpit.
9. Cockpit mostra:
   - contexto tecnico;
   - entregaveis herdados pendentes de revisao;
   - recomendacoes de knowledge por score tecnico;
   - historico/auditoria.

## Regras de negocio

- Sugestoes nao bloqueiam a criacao.
- Usuario sempre pode comecar do zero.
- Tags precisam pertencer ao tenant e nao podem estar arquivadas.
- Entregavel removido do novo projeto nao altera o projeto base.
- Entregaveis herdados entram no fluxo de revisao pos-criacao.
- Score e recomendacoes sao explicaveis, sem IA/embeddings.
- Complexidade tecnica deve ficar no backend e em textos simples na UI.

## Multi-tenancy

O `organizationId` vem do usuario autenticado e e aplicado em todos os use cases e repositorios. Seeds usam o tenant demo `Engenharia Horizonte Ltda`. Nenhum endpoint confia em `organizationId` vindo do body.

## Decisoes tecnicas

- Nao foi criada arquitetura paralela.
- O wizard reaproveita endpoints existentes.
- O perfil tecnico e recalculavel e nao usa cache complexo.
- O score e exibido como `Aderencia` ou `Forca`, nao como formula tecnica.
- Knowledge recomendado usa `ProjectTechnicalProfile` como fonte de contexto.

## Limitacoes conhecidas

- Nao ha IA, embeddings ou busca semantica.
- Nao ha preview separado de documentos modelo no wizard de criacao; eles aparecem como KnowledgeItems no cockpit.
- Recomendacao de projeto base ainda usa score tecnico deterministico por tags e sinais estruturais.
- Nao ha versionamento formal de KnowledgeItem publicado.
- Fluxo de aprovacao de remocao de entregavel esta focado em entregaveis herdados.

## Documentos relacionados

- `docs/project-assisted-creation.md`
- `docs/project-technical-profile.md`
- `docs/project-context-recommendations.md`
- `docs/demo/assisted-project-creation-demo-flow.md`
- `docs/qa-assisted-project-creation.md`
