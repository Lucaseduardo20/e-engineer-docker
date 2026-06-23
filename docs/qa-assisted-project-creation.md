# QA — Criacao assistida por contexto tecnico

## Objetivo

Validar o subepico de criacao assistida de projetos, incluindo seeds, recomendacoes, heranca e cockpit.

## Preparacao

```bash
cd /home/lkt/work/e_engineer/e-engineer-backend
npm run db:migration:run
npm run db:seed
npm run db:seed
```

Rodar duas vezes confirma idempotencia.

## Cenarios minimos

### 1. Criar projeto do zero com tags

1. Abrir `/projects`.
2. Clicar `Novo projeto`.
3. Informar nome.
4. Selecionar tags governadas.
5. Escolher `Comecar do zero`.
6. Confirmar.

Esperado:

- Projeto criado.
- Redireciona ao cockpit.
- Tags aparecem no contexto tecnico.
- Nao ha entregaveis herdados pendentes.

### 2. Ver semelhantes ao selecionar tags

Tags:

- `UBS`
- `Prefeitura SP`
- `Orgao publico`
- `Obra publica`
- `Projeto basico`

Esperado:

- `Construcao da UBS Vila Esperanca` aparece.
- Card mostra `Aderencia N`.
- Tags combinadas aparecem.

### 3. Usar projeto como base

1. Escolher `Construcao da UBS Vila Esperanca`.
2. Revisar entregaveis.
3. Confirmar criacao.

Esperado:

- Projeto criado com relacao de base.
- Entregaveis selecionados sao copiados.
- Base original nao e alterada.
- Cockpit mostra banner de revisao de entregaveis herdados.

### 4. Revisao pos-criacao

1. Abrir cockpit do novo projeto.
2. Ver banner `Revise os entregaveis herdados`.
3. Marcar entregavel como revisado.

Esperado:

- Contador diminui.
- Actor/time registrados.
- Banner some quando todos revisados.

### 5. Remocao governada de herdado

1. Solicitar remocao de entregavel herdado.
2. Informar motivo tecnico.
3. Aprovar/rejeitar conforme RBAC.

Esperado:

- Motivo obrigatorio.
- Base original nao e afetada.
- Historico/auditoria registra movimento.

### 6. Recomendacoes contextuais

1. Abrir cockpit de projeto com perfil tecnico.
2. Ver `Recomendacoes contextuais`.

Esperado:

- Itens mostram `Forca N`.
- `reason` cita tags.
- `alreadyApplied` mostra `Ja aplicado`.
- Archived nao aparece.
- Deprecated, se aparecer, deve ser sinalizado no motivo.

### 7. Tenant protegido

1. Trocar tenant quando possivel.
2. Repetir buscas/recomendacoes.

Esperado:

- Nenhum dado de outro tenant aparece.
- Tags de outro tenant sao recusadas pelo backend.

## Testes automatizados recomendados

Backend:

```bash
cd /home/lkt/work/e_engineer/e-engineer-backend
npm test -- recommend-project-bases-by-tags.use-case.spec.ts recommend-knowledge-for-project.use-case.spec.ts get-project-technical-profile.use-case.spec.ts create-project-from-base-project.use-case.spec.ts
npm run type-check
```

Frontend:

```bash
cd /home/lkt/work/e_engineer/e-engineer-frontend
npm run type-check
```

## Limitacoes conhecidas

- Testes unitarios frontend podem falhar no startup do Vitest em ambientes Node que nao expoem `node:util.styleText`.
- Nao ha IA/embeddings.
- Nao ha recomendacao semantica por texto livre.
