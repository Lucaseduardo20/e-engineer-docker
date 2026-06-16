# Prompt para Implementação da Task 8 — Aplicar KnowledgeItem em Entregáveis

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
Permitir que o conhecimento (`KnowledgeItem`) seja aplicado não apenas ao projeto como um todo, mas também a entregáveis específicos.

## Contexto
Algumas knowledges fazem mais sentido quando ligadas diretamente a um entregável.
Por exemplo:
- checklist de orçamento aplicado ao entregável “Orçamento”;
- documento modelo de memorial aplicado ao entregável “Memorial descritivo”.

## O que deve ser feito
Usar a estrutura existente de `KnowledgeRelation` com:
```txt
targetType = deliverable
```

### Escopo esperado
- Estender ou reutilizar o fluxo de aplicação de knowledge para suportar entregáveis.
- Garantir que a relação entre `KnowledgeItem` e entregável seja criada com `targetType: deliverable`.
- Respeitar regras de tenancy e contexto do projeto/entregável.
- Preservar permissões e visibilidade existentes.

## Orientações para o Codex
1. Leia os documentos indicados antes de gerar código.
2. Explique a abordagem e liste os arquivos exatos que serão criados ou alterados.
3. Não gere código antes de validar o plano com base na arquitetura do projeto.
4. Siga a arquitetura do projeto como uma bíblia: separação entre domínio, aplicação, infraestrutura e apresentação.
5. No backend, aplique a menor mudança possível para suportar `KnowledgeRelation.targetType = deliverable`.
6. No frontend, preserve padrões existentes e use componentes/fluxos já adotados.
7. Priorize clareza e coerência com o modelo de dados e regras de negócio.
8. Não altere áreas não relacionadas da aplicação.

## Regras importantes
- A aplicação do conhecimento em entregáveis deve ser consistente com o modelo de `KnowledgeRelation` já existente.
- Não crie uma estrutura paralela se o relacionamento atual puder ser estendido corretamente.
- Valide se entregáveis são acessíveis apenas dentro do mesmo projeto/tenant.
- Evite mudanças de API desnecessárias se os dados já podem ser representados com `targetType = deliverable`.

## Entrega esperada
Ao finalizar, o Codex deve:
1. apresentar a proposta de implementação e os arquivos envolvidos;
2. implementar a alteração com foco em usar `KnowledgeRelation.targetType = deliverable`;
3. validar a solução com os cenários relevantes;
4. citar explicitamente os casos de teste executados ou considerados ao fim, para confirmar a conclusão da tarefa.
