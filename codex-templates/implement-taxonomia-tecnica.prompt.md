# Prompt para Implementação da Tela de Taxonomia Técnica — E-Engineer

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
Criar a tela de **Taxonomia técnica** na seção de **Organização**, permitindo que administradores e coordenadores gerenciem as tags técnicas do tenant.

## O que deve ser feito
- Criar seção em Organização com título `Taxonomia técnica`.
- Implementar listagem de tags técnicas.
- Implementar busca de tags.
- Implementar filtragem por categoria.
- Implementar filtragem por status.
- Implementar criação de tag.
- Implementar edição de tag.
- Implementar arquivamento de tag.
- Implementar depreciação de tag.
- Exibir contagem de uso quando disponível.

## UI / UX
- A tela deve ser simples e administrativa.
- Apresentar colunas/cards com: nome, slug, categoria, status, descrição, uso, ações.
- Não deve parecer uma tela técnica demais.
- Deve explicar que tags ajudam recomendações e organização do conhecimento.
- Deve exibir alerta de confirmação antes de arquivar ou depreciar.
- Não permitir exclusão destrutiva no MVP.
- UI deve ser consistente com a plataforma existente.

## Regras de Acesso e Permissões
- Admin acessa a tela e usa as ações de gerenciamento.
- Coordinator acessa a tela e usa as ações de gerenciamento.
- Engineer não deve gerenciar tags, salvo regra já adotada no projeto.
- Viewer não gerencia e não deve ver ações de gerenciamento.
- Usuário sem permissão não acessa ações e não pode executar criação/edição/arquivamento/depreciação.

## Critérios de Aceite
- Admin acessa tela.
- Coordinator acessa tela.
- Engineer não gerencia, salvo regra adotada.
- Viewer não gerencia.
- Tags podem ser criadas e editadas.
- Tags podem ser arquivadas e depreciadas.
- Uso da tag aparece se implementado.
- UI é consistente com a plataforma.

## QA — Cenários mínimos
- Listar tags.
- Criar tag.
- Editar tag.
- Arquivar tag.
- Depreciar tag.
- Filtrar por categoria.
- Filtrar por status.
- Usuário sem permissão não acessa ações.

---

## Orientações para o Codex
1. Leia os documentos indicados antes de gerar código.
2. Explique a abordagem e liste os arquivos exatos que serão criados ou alterados.
3. Não gere código antes de validar o plano com base na arquitetura do projeto.
4. Siga a arquitetura do projeto como uma bíblia: Clean Architecture, separação entre domínio, aplicação, infraestrutura e apresentação.
5. No frontend, preserve padrões e componentes existentes do projeto.
6. No backend, use APIs e contratos existentes; se precisar de nova rota ou recurso, proponha a menor mudança possível.
7. Priorize a consistência de UI/UX e regras de negócio sobre forma livre.
8. Não altere áreas não relacionadas da aplicação.

## Padrões Importantes
- Multi-tenant: confirme `organizationId` em todos os fluxos de dados.
- Roles e permissões: respeite as regras de acesso para Admin, Coordinator, Engineer, Viewer.
- Não use exclusão física: apenas arquivar ou depreciar.
- Confirme se há endpoints existentes para tags técnicas ou se será necessário estender o backend.

---

## Resultado Esperado do Prompt
O Codex deve responder com:
1. Resumo de leitura e limites arquiteturais.
2. Plano de arquivos a criar/alterar e mudanças de dados necessárias.
3. Lista de perguntas abertas, se houver.
4. Implementação incremental em pequenos cortes.
5. Testes sugeridos e validação mínima.
6. Relatório de entrega com comandos, resultados e arquivos alterados.
