# ProjectTechnicalProfile

## Objetivo

Consolidar sinais tecnicos do projeto em um perfil unico de tags para alimentar recomendacoes.

## Fontes consideradas

- Tags diretas do projeto (`project_tags`).
- Tags de entregaveis (`deliverable_tags`).
- Tags de documentos (`document_tags`).
- Documentos aprovados/oficiais.

## Pesos implementados

- Tag direta no projeto: `+3`.
- Tag em entregavel: `+2` por ocorrencia.
- Tag em documento: `+1`.
- Tag em documento oficial/aprovado: `+3`.
- Tag arquivada: excluida.

No frontend, o score bruto do perfil nao e exposto como formula. Em recomendacoes ele aparece como `Forca` ou `Aderencia`, para justificar a escolha.

## Backend

Use case:

- `GetProjectTechnicalProfileUseCase`

Servico:

- `ProjectTechnicalProfileScoreService`

Repositorio:

- `ProjectRepository.listTechnicalProfileTagSources`
- `TypeOrmProjectRepository.listTechnicalProfileTagSources`

Endpoint:

- `GET /projects/:id/technical-profile`

## Resposta

```json
{
  "projectId": "...",
  "organizationId": "...",
  "scoreExplanation": "Tag direta no projeto: +3...",
  "tags": [
    {
      "id": "...",
      "name": "UBS",
      "slug": "ubs",
      "category": "project_type",
      "status": "active",
      "score": 6,
      "sources": [
        { "type": "project_tag", "score": 3 },
        { "type": "official_document", "score": 3 }
      ]
    }
  ]
}
```

## Regras

- Sempre filtrado por `organizationId`.
- Nao usa IA/embeddings.
- Recalculavel sob demanda.
- Ordenacao deterministica por score desc e nome.

## Limites conhecidos

- Ainda nao ha cache materializado.
- Deprecated permanece visivel quando vier do contrato de tags, mas archived e excluida.
