# Prompt para Implementação da Task 6 — Redesenhar Detalhe do Projeto como Cockpit Técnico

## Leitura Obrigatória (faça isso ANTES de tocar no código)
Você PRECISA ler atentamente nesta ordem:
1. `master.md` — princípios do projeto e arquitetura geral
2. `e-engineer-backend/docs/codex.md` — padrões backend e histórico de decisões
3. `e-engineer-frontend/codex.md` — padrões frontend e continuidade do projeto
4. `docs/API-CONTRACTS.md` — contratos de API e padrões de comunicação
5. `README-CODEX-PROMPT.md` — protocolo de prompt do projeto
6. `e-engineer-backend/README.md` e `e-engineer-frontend/README.md` — para entender scripts, build e execução

Após a leitura, resuma em 3–6 pontos os limites arquiteturais, regras de negócio e decisões que impactam esta tarefa.

---

## Objetivo da Tarefa
Reorganizar a tela de detalhe do projeto para que ela comunique a situação operacional e técnica do projeto de forma clara, transformando a página em um cockpit técnico da plataforma.

## Contexto
Hoje o detalhe do projeto já exibe informações importantes, mas a seção de conhecimento aplicado ainda parece uma lista técnica simples. O projeto precisa virar o cockpit principal da plataforma.

## O que deve ser feito
Redesenhar a estrutura da tela com as seguintes seções:
1. Header executivo
2. Indicadores rápidos
3. Resumo operacional
4. Entregáveis
5. Documentos
6. Revisões
7. Conhecimento aplicado
8. Recomendações
9. Riscos e aprendizados
10. Histórico

### Header executivo
Exibir:
- nome
- cliente
- status
- progresso
- responsável
- prazo
- ações principais

### Indicadores rápidos
Exibir cards pequenos com:
- entregáveis totais
- entregáveis atrasados
- documentos oficiais
- revisões pendentes
- revisões reprovadas
- conhecimentos aplicados
- recomendações disponíveis

## Backend
Pode ser necessário criar endpoint de resumo:
GET /projects/:projectId/technical-summary

---

## Orientações para o Codex
1. Leia os documentos indicados antes de gerar código.
2. Explique a abordagem e liste os arquivos exatos que serão criados ou alterados.
3. Não gere código antes de validar o plano com base na arquitetura do projeto.
4. Siga a arquitetura do projeto como uma bíblia: Clean Architecture, separação entre domínio, aplicação, infraestrutura e apresentação.
5. No frontend, preserve padrões e componentes existentes e a identidade visual da plataforma.
6. No backend, use APIs e contratos existentes; se for necessário criar um endpoint novo, justifique a necessidade e proponha a menor mudança possível.
7. Priorize clareza de leitura, usabilidade e consistência da interface.
8. Não altere áreas não relacionadas da aplicação.

## Regras Importantes
- O redesign deve melhorar a leitura operacional e técnica do projeto, sem perder os dados já existentes.
- Se a tela depender de dados agregados, verifique se há endpoint adequado ou se será necessário estender o backend com um resumo técnico.
- Respeite os limites arquiteturais do projeto e mantenha o padrão de módulos já adotado.
- O MVP não precisa reinventar o modelo de dados; deve melhorar a experiência e a organização da informação.

---

## Resultado Esperado do Prompt
O Codex deve responder com:
1. Resumo de leitura e limites arquiteturais.
2. Plano de arquivos a criar/alterar e mudanças de dados necessárias.
3. Lista de perguntas abertas, se houver.
4. Implementação incremental em pequenos cortes.
5. Testes sugeridos e validação mínima.
6. Ao final do desenvolvimento, o Codex deve citar explicitamente os casos de teste executados/considerados para confirmar que a tarefa foi concluída.
7. Relatório de entrega com comandos, resultados e arquivos alterados.
