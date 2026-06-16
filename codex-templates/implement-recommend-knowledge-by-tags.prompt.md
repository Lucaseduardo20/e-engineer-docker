# Prompt para Implementação da Task 9 — Recomendações Simples por Tags

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
Sugerir `KnowledgeItems` relevantes para um projeto com base em tags governadas pela taxonomia técnica.

## Contexto
Antes de IA, a plataforma pode gerar valor com recomendações simples baseadas em taxonomia, usando relacionamentos de tags para trazer knowledge relevante ao projeto.

## O que deve ser feito
Criar o use case:
```txt
RecommendKnowledgeForProjectUseCase
```

### Escopo esperado
- Implementar lógica de recomendação simples baseada em tags do projeto e tags governadas de `KnowledgeItems`.
- Garantir que a recomendação seja restrita ao tenant/organization certo.
- Considerar apenas `KnowledgeItems` ativos e relevantes para o status do projeto.
- Reusar a taxonomia existente e os controles de permissão sempre que possível.

## Orientações para o Codex
1. Leia os documentos indicados antes de gerar código.
2. Explique a abordagem e liste os arquivos exatos que serão criados ou alterados.
3. Não gere código antes de validar o plano com base na arquitetura do projeto.
4. Siga a arquitetura do projeto como uma bíblia: separação entre domínio, aplicação, infraestrutura e apresentação.
5. No backend, crie o use case no domínio/aplicação; mantenha a implementação simples e previsível.
6. No frontend, apenas consuma o use case se já houver fluxo claro; caso contrário, proponha o menor ponto de exposição possível.
7. Priorize clareza, consistência e uso correto de taxonomia.
8. Não altere áreas não relacionadas da aplicação.

## Regras importantes
- A recomendação deve ser simples e baseada em tags, não em modelos de IA.
- Use a taxonomia governada como fonte de confiança para filtrar e priorizar itens.
- Evite introduzir regras de negócio complexas desnecessárias no MVP.
- Assegure que o use case respeite `organizationId` e contexto do projeto.

## Entrega esperada
Ao finalizar, o Codex deve:
1. apresentar a proposta de implementação e os arquivos envolvidos;
2. implementar `RecommendKnowledgeForProjectUseCase` com lógica de recomendação por tags;
3. validar a solução com os cenários relevantes;
4. citar explicitamente os casos de teste executados ou considerados ao fim, para confirmar a conclusão da tarefa.
