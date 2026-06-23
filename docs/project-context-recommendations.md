# Project Context Recommendations

## Objetivo

Usar o `ProjectTechnicalProfile` para recomendar conhecimento aplicavel ao projeto no cockpit.

## Backend

Use case:

- `RecommendKnowledgeForProjectUseCase`

Endpoint:

- `GET /projects/:id/knowledge/recommendations`

Repositorios usados:

- `ProjectRepository`
- `DeliverableRepository`
- `KnowledgeItemRepository`

## Entradas do calculo

1. Projeto do tenant autenticado.
2. Entregaveis do projeto para identificar contexto aplicado.
3. `ProjectTechnicalProfile` para obter tags e score tecnico.
4. KnowledgeItems com tags governadas.
5. KnowledgeRelations para calcular `alreadyApplied`.

## Regras

- Apenas itens do mesmo tenant.
- `archived` e excluido.
- `published` e priorizado.
- `deprecated` pode aparecer, mas com penalizacao e motivo avisando.
- `alreadyApplied` e retornado para a UI sinalizar que o conhecimento ja esta aplicado.
- `reason` e obrigatorio.

## Retorno

```json
{
  "items": [
    {
      "type": "review_checklist",
      "knowledgeItem": {
        "id": "...",
        "title": "Revisao de orcamento antes de envio ao cliente",
        "type": "review_checklist",
        "status": "published"
      },
      "score": 12,
      "matchedTags": [
        { "id": "...", "name": "Orcamento", "slug": "orcamento" }
      ],
      "reason": "Sugestao baseada no contexto tecnico: Orcamento.",
      "alreadyApplied": false
    }
  ]
}
```

## Frontend

Componente:

- `ProjectDetail.vue`

Secao:

- `Recomendacoes contextuais`

Microcopy:

- `Sugestoes baseadas no contexto tecnico deste projeto.`

Acoes:

- `Aplicar ao projeto`
- `Abrir detalhe`
- `Ja aplicado`

Score na UI:

- exibido como `Forca N`.

## Limites conhecidos

- Documentos modelo e checklists sao representados como `KnowledgeItems`.
- Projetos semelhantes aparecem no wizard de criacao, nao nesta secao do cockpit.
- Nao ha explicacao expandida da formula no frontend.
