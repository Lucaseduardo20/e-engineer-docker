# Master Guide - E-Engineer

Este arquivo e o guia principal para qualquer sessao de Codex neste projeto.
Antes de implementar, revisar ou decidir qualquer coisa relevante, a sessao deve ler este arquivo e respeitar seus principios.

## Papel do Produto

E-Engineer e um SaaS B2B vertical para empresas de engenharia civil.

O produto existe para ajudar empresas de engenharia a:

- padronizar projetos tecnicos;
- controlar versoes e revisoes;
- organizar documentos tecnicos;
- gerenciar entregaveis;
- reutilizar projetos antigos como referencia;
- reduzir retrabalho e inconsistencias tecnicas.

O sistema nao deve ser conduzido como um clone generico de ClickUp, Trello ou gestor de tarefas.

A linguagem do produto deve ser a linguagem do dominio:

- projeto tecnico;
- entregavel;
- documento oficial;
- revisao;
- versao;
- template;
- padrao tecnico;
- referencia;
- historico;
- responsavel tecnico;
- reutilizacao de projetos anteriores.

## Stack

Backend:

- NestJS;
- TypeScript;
- TypeORM;
- PostgreSQL;
- Docker;
- Clean Architecture;
- DDD;
- testes automatizados.

Frontend:

- Vue 3;
- Vite;
- TypeScript;
- Pinia;
- Vue Router;
- arquitetura modular;
- integracao via API REST.

## Principios Arquiteturais

- O backend segue Clean Architecture + DDD.
- Separar claramente Domain, Application, Infrastructure e Presentation.
- Controllers devem ser finos.
- Controllers nao contem regra de negocio.
- Use cases orquestram fluxos de aplicacao.
- Entidades de dominio concentram comportamento e invariantes.
- Entidades TypeORM nao sao entidades de dominio.
- TypeORM fica isolado em Infrastructure.
- Repositorios de dominio devem falar a linguagem do modulo, nao CRUD generico.
- Abstracoes genericas, quando existirem, devem ficar em infraestrutura ou shared kernel com uso claro.
- DTOs de entrada e saida ficam em Application ou Presentation.
- A API nao retorna entidades de dominio diretamente.
- Evitar overengineering sem uso concreto.

## Multi-tenancy

O sistema e multi-tenant desde o inicio.

Decisao atual:

- single database;
- single schema;
- isolamento por `organizationId`.

Regras obrigatorias:

- toda entidade de negocio relevante deve estar vinculada a uma organizacao;
- nenhuma consulta de negocio pode ignorar `organizationId`;
- repositorios devem receber escopo de tenant explicitamente;
- nunca assumir tenant global implicito sem uma decisao arquitetural registrada;
- testes devem cobrir isolamento quando houver persistencia ou queries relevantes.

## Modulos Planejados

- identity;
- organizations;
- projects;
- templates;
- deliverables;
- documents;
- reviews;
- knowledge-base;
- audit.

Cada modulo deve ter seu proprio dominio e suas proprias regras.

Estrutura esperada por modulo:

```txt
src/modules/{module-name}/
  domain/
    entities/
    value-objects/
    repositories/
    events/
    services/
  application/
    use-cases/
    dto/
    ports/
  infrastructure/
    persistence/
      typeorm/
    mappers/
  presentation/
    controllers/
    dto/
```

## Shared Kernel

O shared kernel deve conter apenas blocos realmente transversais.

Permitido:

- Entity base;
- AggregateRoot;
- ValueObject;
- DomainEvent;
- DomainError;
- Result;
- identificadores;
- contratos transversais;
- infraestrutura compartilhada de eventos;
- helpers de persistencia tenant-aware.

Evitar:

- regras de negocio especificas;
- servicos genericos sem caso real;
- repositorio CRUD generico no dominio;
- objetos que pertencem claramente a um modulo especifico.

## Fluxo de Trabalho com Codex

Toda sessao deve seguir este fluxo:

1. Ler `master.md`.
2. Ler `codex.md` quando a tarefa envolver contexto historico, decisoes anteriores ou auditoria.
3. Entender o pedido do usuario.
4. Identificar o modulo correto.
5. Explicar rapidamente a abordagem antes de alterar codigo.
6. Listar arquivos que pretende criar ou alterar quando a mudanca for relevante.
7. Implementar de forma incremental.
8. Rodar validacoes proporcionais ao risco.
9. Atualizar `codex.md` para decisoes relevantes.
10. Sugerir commit quando o corte estiver coeso.

## Decisoes Arquiteturais

Decisoes importantes devem ser revisadas com o usuario antes da implementacao.

Exemplos de decisoes importantes:

- estrategia de tenancy;
- autenticacao e autorizacao;
- fronteiras entre modulos;
- mudanca de stack;
- padrao de eventos;
- estrategia de persistencia;
- padrao de migrations;
- padrao de testes;
- contratos publicos de API;
- alteracoes no modelo central do dominio.

Quando uma decisao for aprovada, registrar em `codex.md`.

## Relacao entre master.md e codex.md

`master.md` e o guia estavel do projeto.

Ele contem:

- principios;
- arquitetura esperada;
- protocolo de trabalho;
- estrategia de versionamento;
- regras permanentes para sessoes de IA.

`codex.md` e o historico/auditoria.

Ele contem:

- decisoes tomadas;
- contexto de cortes implementados;
- justificativas relevantes;
- observacoes para continuidade entre sessoes.

Se houver conflito entre os dois:

1. seguir a decisao mais recente registrada em `codex.md`;
2. propor atualizar `master.md` se a decisao virar principio permanente.

## Estrategia de Commits

O projeto deve evitar commits gigantes.

Commits devem representar cortes coesos e revisaveis.

Tamanho ideal:

- uma decisao arquitetural pequena;
- uma fundacao tecnica isolada;
- uma entidade/use case completo;
- um ajuste de teste;
- uma refatoracao sem mudanca funcional;
- uma correcao de bug especifica.

Evitar:

- misturar feature, refatoracao e formatacao no mesmo commit;
- alterar muitos modulos sem uma justificativa clara;
- commitar codigo quebrado;
- commitar decisoes arquiteturais sem registro em `codex.md`;
- commitar arquivos gerados desnecessarios.

Antes de sugerir commit, verificar:

- `git status --short`;
- diff dos arquivos alterados;
- lint, build e testes relevantes;
- se `codex.md` precisa ser atualizado.

Codex deve sugerir o commit quando o corte estiver pronto, mas so deve executar `git add` e `git commit` quando o usuario pedir ou confirmar explicitamente.

Se existirem mudancas pre-existentes do usuario no working tree:

- nao reverter;
- nao misturar no commit sem necessidade;
- separar o corte quando possivel;
- perguntar antes se a separacao nao estiver clara.

Formato recomendado de mensagem:

```txt
type(scope): summary
```

Tipos recomendados:

- `feat`: nova capacidade de produto;
- `fix`: correcao de bug;
- `chore`: setup, tooling, dependencias ou manutencao;
- `refactor`: mudanca interna sem alterar comportamento;
- `test`: testes;
- `docs`: documentacao;
- `arch`: decisao ou estrutura arquitetural relevante.

Exemplos:

```txt
docs(project): add master guide for codex sessions
arch(backend): establish tenant-aware shared kernel
feat(projects): create technical project use case
test(projects): cover create project use case
```

## Quando Commitar

Sugerir commit quando:

- uma fundacao arquitetural estiver validada;
- um modulo ou use case minimo estiver completo;
- uma decisao documentada estiver registrada;
- testes e build passarem para o corte;
- o diff estiver pequeno o bastante para revisao humana.

Nao sugerir commit quando:

- a implementacao estiver incompleta;
- houver falhas de lint/build/test nao explicadas;
- houver decisao arquitetural pendente;
- o usuario estiver apenas explorando ideias;
- existirem mudancas misturadas que deveriam ser separadas primeiro.

## Validacoes Padrao

Backend:

```txt
npm run lint
npm test -- --runInBand
npm run build
```

E2E/integracao:

- rodar quando houver Postgres ativo;
- preferir teste de integracao para persistencia e HTTP;
- cobrir isolamento por `organizationId` quando houver consulta tenant-aware.

## Regra de Ouro

Antes de implementar, perguntar:

Este codigo fortalece um SaaS vertical de engenharia civil ou empurra o produto para um gestor generico?

Se a resposta pender para generico, repensar a modelagem.
