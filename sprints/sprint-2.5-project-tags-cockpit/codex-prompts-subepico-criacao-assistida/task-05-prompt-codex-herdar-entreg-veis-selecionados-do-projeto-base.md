# Task 5 — Herdar entregáveis selecionados do projeto base

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

Permitir selecionar quais entregáveis do projeto base serão herdados ao criar novo projeto.

---

# Contexto específico

Copiar tudo cegamente gera sujeira. O usuário deve revisar a estrutura do projeto base e escolher quais entregáveis fazem sentido.

---

# Escopo funcional

Adicionar `deliverablesToInherit` ao fluxo de criação baseada em projeto. Criar novos entregáveis no novo projeto com origem rastreável.

---

# Backend — O que deve ser feito

Ajustar `CreateProjectFromBaseProjectUseCase` para criar entregáveis selecionados, preservar nome/tipo/descrição, resetar status para inicial adequado, não copiar documentos/revisões, opcionalmente criar `deliverable_base_relations`.

---

# Frontend — O que deve ser feito

No wizard, mostrar entregáveis do projeto base com checkbox, tags/tipo/status, permitir selecionar/desselecionar e continuar sem herdar nenhum.

---

# Regras de negócio

Só herdar entregáveis do projeto base validado. Não copiar documentos/revisões. Não copiar status finalizado como pronto. Tags herdadas devem usar source inherited, se aplicável.

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

- Usuário escolhe entregáveis
- Apenas selecionados são criados
- Novos pertencem ao novo projeto
- Origem rastreável
- Não copia documentos/revisões
- Pode criar sem herdar

---

# QA — Cenários mínimos

- Selecionar 2 de 5 entregáveis e validar que só 2 foram criados.
- Criar sem selecionar nenhum.
- Validar que documentos não foram copiados.
- Validar tags herdadas, se implementado.
- Bloquear entregável de outro tenant.

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
