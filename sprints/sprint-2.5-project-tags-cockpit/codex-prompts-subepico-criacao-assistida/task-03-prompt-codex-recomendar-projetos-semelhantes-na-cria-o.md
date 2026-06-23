# Task 3 — Recomendar projetos semelhantes na criação

# Contexto global obrigatório

Você está trabalhando no projeto **e-engineer**, um SaaS B2B vertical para empresas de engenharia, arquitetura e operação técnica.

A plataforma não deve ser um gerenciador genérico de tarefas, nem uma cópia de Trello, ClickUp, Monday ou Notion.

A tese central do produto é:

> Projetos geram conhecimento. Conhecimento melhora novos projetos.

A e-engineer conecta organizações, colaboradores, projetos, entregáveis técnicos, documentos, versões, revisões, Base de Conhecimento, Taxonomia Técnica, conhecimento aplicado e recomendações.

O objetivo deste subépico é lançar uma inteligência vendável no produto: a criação de projetos não deve ser apenas um formulário com nome e descrição. Ela deve ser assistida por contexto técnico. O usuário seleciona tags governadas, a plataforma recomenda projetos semelhantes, documentos, entregáveis e conhecimentos, e o novo projeto nasce já conectado ao conhecimento acumulado da empresa.

Frase-guia:

> A e-engineer não começa um projeto do zero. Ela começa com a inteligência acumulada da sua empresa.
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

Criar mecanismo simples de recomendação de projetos semelhantes com base nas tags selecionadas na criação de projeto.

---

# Contexto específico

Ao selecionar UBS, Prefeitura SP e Orçamento, a plataforma deve mostrar projetos antigos parecidos com motivo da recomendação. Esse é o primeiro momento vendável de inteligência do produto.

---

# Escopo funcional

Criar use case `RecommendSimilarProjectsUseCase` e endpoint `GET /projects/similar?tagIds=...` ou `POST /projects/similar`. Retornar project summary, score, matchedTags, reason, contadores úteis.

---

# Backend — O que deve ser feito

Validar tagIds, buscar apenas projetos do tenant, calcular score por interseção, excluir statuses inadequados, ordenar por score desc e limitar resultados. Reason precisa ser claro.

---

# Frontend — O que deve ser feito

Na tela/wizard de novo projeto, ao selecionar tags, buscar recomendações com debounce. Exibir bloco “Projetos semelhantes encontrados” com cards e ação “Usar como base”.

---

# Regras de negócio

Só recomendar projetos do mesmo tenant, com tag em comum. Toda recomendação precisa de motivo. Não vender como IA. Limitar resultados.

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

- Use case existe
- Endpoint retorna score/matchedTags/reason
- Frontend mostra recomendações
- Reason claro
- Respeita tenant
- Ordena por score

---

# QA — Cenários mínimos

- Projeto antigo com UBS+Orçamento aparece ao selecionar essas tags.
- Reason menciona tags em comum.
- Sem tags mostra empty state.
- Outro tenant não aparece.
- Maior match aparece primeiro.

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
