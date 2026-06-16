# Prompt para Implementação da Task 7 — Visão Rica de Entregáveis Técnicos

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
Fazer os entregáveis técnicos se tornarem o eixo operacional principal dentro do projeto, com uma visão rica e útil que mostre claramente suas relações com documentos, revisões, prazos, responsáveis e knowledges aplicados.

## Contexto
A dor de engenharia gira em torno de entregáveis. Cada entregável pode ter documentos, revisões, responsáveis, prazos, status e conhecimentos aplicados, e essa visão deve ser centralizada e clara.

## O que deve ser feito
Criar o componente:
```txt
ProjectDeliverableTechnicalCard
```

### Escopo esperado
O componente deve ser capaz de exibir:
- nome do entregável;
- status atual;
- responsável;
- prazo/entrega;
- documentos oficiais relacionados;
- revisões pendentes e reprovadas;
- conhecimentos aplicados;
- indicadores de risco ou necessidades técnicas importantes.

### Objetivo de UX
- Transformar entregáveis em pontos de ação operacional claros.
- Dar ao usuário uma visão rápida e rica do que está acontecendo em cada entregável.
- Facilitar a navegação entre entregáveis, documentos e knowledges.
- Mostrar valor imediato para a equipe de engenharia.

## Orientações para o Codex
1. Leia os documentos indicados antes de gerar código.
2. Explique a abordagem e liste os arquivos exatos que serão criados ou alterados.
3. Não gere código antes de validar o plano com base na arquitetura do projeto.
4. Siga a arquitetura do projeto como uma bíblia: separación entre domínio, aplicação, infraestrutura e apresentação.
5. No frontend, preserve padrões e componentes existentes e a identidade visual da plataforma.
6. No backend, use APIs e contratos existentes; se for necessário criar ou estender endpoints, proponha a menor mudança possível.
7. Priorizne clareza, consistência visual e usabilidade.
8. Não altere áreas não relacionadas da aplicação.

## Regras importantes
- O componente deve ser rico, mas também legível e enxuto.
- Deve ser orientado para ação e para visão operacional.
- O usuário deve imediatamente entender o estado do entregável e seus pontos de atenção.
- Respeite os limites de permissão e contexto do projeto.
- Se houver necessidade de dados agregados, verifique se há endpoint existente ou proponha um endpoint novo mínimo.

## Entrega esperada
Ao finalizar, o Codex deve:
1. apresentar a proposta de implementação e os arquivos envolvidos;
2. implementar o componente com foco em experiência operacional;
3. validar a solução com os cenários relevantes;
4. citar explicitamente os casos de teste executados ou considerados ao fim, para confirmar a conclusão da tarefa.
