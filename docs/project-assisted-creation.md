# Project Assisted Creation

## Objetivo

Criar projetos a partir de contexto tecnico governado, com sugestoes de projetos base e revisao dos entregaveis herdados.

## Frontend

Componente principal:

- `e-engineer-frontend/src/modules/projects/components/ProjectCreateWizard.vue`

Entrada pela listagem:

- `e-engineer-frontend/src/modules/projects/pages/ProjectsListPage.vue`

Fluxo atual do wizard:

1. `Dados`: nome e tipo tecnico.
2. `Contexto`: selecao de tags governadas com `TechnicalTagSelector`.
3. `Partida`: escolha entre comecar do zero ou usar base recomendada.
4. `Entregaveis`: revisao dos entregaveis da base.
5. `Confirmar`: resumo e criacao.

## Backend reaproveitado

- `CreateProjectUseCase`
- `CreateProjectFromBaseProjectUseCase`
- `RecommendProjectBasesByTagsUseCase`
- `RecommendSimilarProjectsUseCase`

Endpoints:

- `POST /projects`
- `POST /projects/from-base`
- `POST /projects/recommend-bases`
- `POST /projects/similar`

## Payloads principais

Criar do zero:

```json
{
  "name": "Nova UBS Jardim Aurora",
  "projectType": "unidade de saude",
  "tagIds": ["..."]
}
```

Criar a partir de base:

```json
{
  "baseProjectId": "...",
  "name": "Nova UBS Jardim Aurora",
  "projectType": "unidade de saude",
  "tagIds": ["..."],
  "inheritTags": true,
  "inheritDeliverables": false,
  "deliverablesToInherit": ["..."]
}
```

## UX

- Tags sao recomendadas, mas nao obrigatorias.
- Sugestoes nao bloqueiam.
- Score aparece como `Aderencia N`.
- Usuario nao ve `relationType`, ids internos ou detalhes de formula.
- Apos criar, a UI redireciona para o cockpit do projeto.

## Pos-criacao

Quando entregaveis sao herdados:

- cada entregavel nasce marcado como pendente de revisao;
- banner `Revise os entregaveis herdados` aparece no cockpit;
- usuario pode marcar revisado;
- remocao exige motivo e respeita fluxo de aprovacao.

## Compatibilidade

O fluxo antigo de criar projeto simples continua suportado pelo endpoint `POST /projects`.
