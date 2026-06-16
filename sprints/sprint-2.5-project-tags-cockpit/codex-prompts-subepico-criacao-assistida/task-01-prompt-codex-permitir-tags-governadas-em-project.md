# Task 1 — Permitir tags governadas em Project

# Contexto global obrigatório

Você está trabalhando no projeto **e-engineer**, um SaaS B2B vertical para empresas de engenharia, arquitetura e operação técnica.

A plataforma não deve ser um gerenciador genérico de tarefas, nem uma cópia de Trello, ClickUp, Monday ou Notion.

A tese central do produto é:

> Projetos geram conhecimento. Conhecimento melhora novos projetos.

A e-engineer conecta organizações, colaboradores, projetos, entregáveis técnicos, documentos, versões, revisões, Base de Conhecimento, Taxonomia Técnica, conhecimento aplicado e recomendações.

O objetivo deste subépico é lançar uma inteligência vendável no produto: a criação de projetos não deve ser apenas um formulário com nome e descrição. Ela deve ser assistida por contexto técnico. O usuário seleciona tags governadas, a plataforma recomenda projetos semelhantes, documentos, entregáveis e conhecimentos, e o novo projeto nasce já conectado ao conhecimento acumulado da empresa.

Frase-guia:

> A e-engineer não começa um projeto do zero. Ela começa com a inteligência acumulada da sua empresa.

## Documentações obrigatórias para leitura

Antes de implementar qualquer coisa, leia profundamente:

- `docs/master.md`
- `docs/business/01-product-vision.md`
- `docs/business/02-domain-map.md`
- `docs/business/03-business-flows.md`
- `docs/business/04-business-rules.md`
- `docs/business/05-knowledge-base.md`
- `docs/business/06-intelligence-roadmap.md`
- `docs/epics/01-epic-knowledge-base-operacional.md`
- `docs/epics/01-epic-knowledge-base-backlog.md`
- `docs/epics/02-epic-cockpit-tecnico.md`
- `docs/epics/02-epic-cockpit-tecnico-backlog.md`
- `docs/epics/subepico-criacao-assistida-projetos-contexto-tecnico.md`, se existir
- `docs/modules/knowledge-base.md`
- `docs/modules/knowledge-base-api.md`
- `docs/modules/knowledge-base-permissions.md`
- `docs/modules/technical-taxonomy.md`, se existir
- `docs/modules/project-cockpit.md`, se existir
- `docs/demo/knowledge-base-demo-flow.md`
- `docs/demo/project-cockpit-demo-flow.md`, se existir

Se algum arquivo não existir exatamente nesses caminhos, procure o equivalente dentro de `docs/`.

## Código obrigatório para análise

Antes de alterar código, leia a estrutura real do projeto e entenda:

- backend NestJS, TypeScript, TypeORM e PostgreSQL;
- arquitetura DDD/Clean Architecture;
- entidades de domínio separadas de ORM;
- use cases na camada de aplicação;
- controllers finos;
- repositórios por contrato;
- migrations e seeds;
- multi-tenancy por `organizationId`;
- frontend Vue 3, Composition API, services/composables e componentes existentes;
- módulos Organizations, Projects, Deliverables, Documents, DocumentVersions, Reviews, Knowledge Base, KnowledgeRelation e TechnicalTags.

Não invente uma arquitetura paralela. Siga os padrões já existentes.

## Regra de ouro

Qualquer implementação deve preservar:

- isolamento por tenant;
- segurança de organizationId;
- linguagem de produto simples para o usuário;
- complexidade técnica escondida da UI;
- DDD/Clean Architecture;
- compatibilidade incremental com o que já existe;
- clareza para futura recomendação por tags;
- não usar IA/embeddings agora;
- não transformar a plataforma em gerenciador genérico.

## Antes de codar

Antes de implementar, responda primeiro com um plano curto contendo:

1. Arquivos que você vai ler.
2. Arquivos que pretende criar.
3. Arquivos que pretende alterar.
4. Estratégia técnica.
5. Riscos de compatibilidade.
6. Como vai preservar multi-tenancy.
7. Como vai validar.
8. Comandos que eu devo rodar.

Só depois implemente.


---

# Objetivo da task

Adicionar suporte a TechnicalTags diretamente em projetos, permitindo que um projeto tenha contexto técnico governado desde sua criação.

---

# Contexto específico

Hoje a taxonomia já existe para KnowledgeItems ou está em implantação, mas a criação assistida exige que Project também seja classificado com tags governadas. Quando o usuário cria um projeto, ele informa contexto técnico como UBS, Prefeitura SP, Orçamento, Projeto Executivo, Reforma Escolar, Drenagem etc. Essas tags serão o primeiro sinal semântico do projeto.

---

# Escopo funcional

Criar vínculo entre Project e TechnicalTag. Tabela recomendada: `project_tags`.

Campos mínimos: `id`, `organization_id`, `project_id`, `tag_id`, `source`, `created_by`, `created_at`.

`source`: `manual`, `inherited`, `suggested`, `system`. Nesta task, implementar `manual` e preparar os demais.

---

# Backend — O que deve ser feito

Criar migration, ORM entity, repositório/métodos de sync, DTOs de Create/UpdateProject com `tagIds`, validação via TechnicalTagRepository, retorno de Project com tags resolvidas e seeds de projetos com tags.

---

# Frontend — O que deve ser feito

Ajustar formulário de criação/edição de projeto para trabalhar com `tagIds`. Se `TechnicalTagSelector` já existir, usar. Caso contrário, preparar tipagem e manter UI compatível. Exibir tags em cards/detalhe do projeto usando `tag.name`.

---

# Regras de negócio

Project só usa tags da mesma organizationId. Não permitir archived/deprecated em novo vínculo, salvo decisão explícita. Não duplicar tag no projeto. Se `tagIds` não vier no update, não alterar tags. Se vier `[]`, remover vínculos. Todas as consultas devem respeitar tenant.

---

# O que NÃO fazer nesta task

- Não sair do escopo desta task.
- Não implementar IA/embeddings.
- Não criar arquitetura paralela.
- Não quebrar o fluxo existente sem fallback/compatibilidade.
- Não ignorar multi-tenancy.
- Não expor conceitos técnicos internos para o usuário final sem necessidade.

---

# Critérios de aceite

- Persistência de ProjectTag existe
- CreateProject aceita tagIds
- UpdateProject sincroniza tags
- Detail/List retornam tags resolvidas
- Bloqueia tag de outro tenant
- Bloqueia archived
- Não duplica tags
- Seeds criam projetos tagueados

---

# QA — Cenários mínimos

- Criar projeto com tags e ver no detalhe.
- Editar tags A+B para B+C e validar sync.
- Tentar tag de outro tenant e esperar erro.
- Tentar tag archived e esperar erro.
- Validar cards/listagem sem quebrar.

---

# Testes automatizados recomendados

Se o projeto possui setup de testes, crie ou ajuste testes para cobrir os comportamentos principais desta task.

Priorize testes de:

- domínio/use cases;
- repositórios;
- endpoints;
- componentes/composables frontend, quando aplicável;
- casos multi-tenant;
- casos de permissão;
- cenários de regressão.

---

# Comandos

Não assuma que pode instalar dependências.

Se precisar de dependência nova, avise antes e peça confirmação.

Comandos possíveis, adaptar ao projeto real:

```bash
npm run test
npm run lint
npm run typecheck
npm run start:dev
npm run db:migration:run
npm run db:seed
npm run dev
```

Informe exatamente em qual diretório cada comando deve ser executado.

---

# Resultado esperado na resposta final

Ao final da implementação, responda com:

1. Resumo do que foi implementado.
2. Arquivos criados.
3. Arquivos alterados.
4. Decisões técnicas tomadas.
5. Como a regra de negócio foi garantida.
6. Como multi-tenancy foi protegido.
7. Como testar manualmente.
8. Comandos que devo rodar.
9. Pendências ou limitações conhecidas.
10. Próxima task recomendada.
