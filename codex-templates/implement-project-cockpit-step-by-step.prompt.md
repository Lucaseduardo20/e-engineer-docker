# Prompt para Implementação — Novo Projeto com Passo a Passo e Inteligência por Tags

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
Refatorar o fluxo de criação de projeto para um cadastro guiado em passos, com recomendação inteligente de projetos base a partir das tags selecionadas.

## Contexto
O cockpit de projetos deve começar no momento em que o usuário cria um projeto.
A experiência ideal é que o usuário não comece com um formulário cheio, mas com um passo a passo que traz inteligência desde a primeira tag.

O fluxo ideal descrito é:
1. clicar em "Novo projeto"
2. informar nome do projeto
3. começar a selecionar tags
4. a inteligência passa a recomendar projetos com as tags escolhidas
5. o usuário pode selecionar um projeto para usar como base
6. o projeto base é importado sem responsabilidades, apenas com entregáveis e conteúdo de entidades alinhadas à taxonomia
7. o usuário personaliza o projeto à sua maneira, mas já ganha tempo porque a base traz documentos, entregáveis e estrutura comuns

## O que deve ser feito
### Frontend
- Implementar o fluxo guiado de criação de projeto em passos.
- Criar ou adaptar um componente de criação de projeto com as etapas: nome, tags, recomendações e base.
- Fazer a seleção de tags via taxonomia governada, não via texto livre.
- Exibir recomendações de projetos base conforme as tags escolhidas.
- Permitir visualizar e selecionar um projeto base antes de seguir.
- Garantir que o projeto base importado venha sem responsabilidade atribuída.
- Preservar apenas entregáveis, documentos, revisões e estrutura técnica do projeto base.
- Deixar claro para o usuário que ele está criando um novo projeto a partir de um template/estrutura.

### Backend
- Se não existir, criar endpoint de recomendação de projetos por tags.
- O endpoint deve retornar projetos candidatos publicados/ativos com relação às tags selecionadas.
- O endpoint deve respeitar `organizationId` e usar tags governadas.
- O backend deve expor dados suficientes para exibir: título do projeto base, tags, entregáveis e principais documentos/entidades associados.

### Regras de negócio
- A recomendação deve ser acionada assim que houver tags selecionadas.
- Projetos base sugeridos devem ser do mesmo tenant/organização.
- O projeto base sugerido não deve levar responsabilidades de pessoas ou equipes para o novo projeto.
- O projeto base deve trazer apenas estrutura, entregáveis, documentos e conteúdo padronizado, como ponto de partida.
- Não crie dependências fora do fluxo de criação de projeto.

## Orientações para o Codex
1. Leia os documentos indicados antes de gerar código.
2. Explique a abordagem e liste os arquivos exatos que serão criados ou alterados.
3. Não gere código antes de validar o plano com base na arquitetura do projeto.
4. Siga a arquitetura do projeto: domínio, aplicação, infraestrutura e apresentação.
5. No frontend, preserve padrões e componentes existentes e mantenha a usabilidade.
6. No backend, use APIs e contratos atuais; crie novos endpoints apenas se estritamente necessário.
7. Priorize um fluxo incremental e seguro, evitando mudanças grandes demais de uma vez.
8. Não altere áreas não relacionadas da aplicação.

## Regras importantes
- O objetivo é não transformar o fluxo em uma lista de campos, mas em um passo a passo guiado.
- A inteligência deve ser realizada por recomendação de projetos base com tags, não por IA generativa.
- As tags devem ser governadas pela taxonomia técnica já existente.
- A experiência deve explicar o valor do projeto base e o fato de que ele não carrega responsabilidades.
- O MVP deve entregar ganho de tempo real: seleção de base + estrutura reutilizável.

## Entrega esperada
Ao finalizar, o Codex deve:
1. apresentar a proposta de implementação e os arquivos envolvidos;
2. indicar se será necessário criar novo endpoint de recomendação e qual será seu contrato;
3. implementar o fluxo guiado de criação de projeto com seleção de tags e escolha de projeto base;
4. garantir que o projeto base seja trazido sem responsáveis atribuídos;
5. sugerir casos de teste ou validações mínimas para o fluxo.
