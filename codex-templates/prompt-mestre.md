Prompt mestre (Português) — Implementação de tarefas E-Engineer
=============================================================

Objetivo: Este prompt orienta o Codex/IA a executar implementações no projeto E‑Engineer respeitando arquitetura, regras de negócio, testes mínimos, auditoria e boas práticas.

Instruções obrigatórias (antes de qualquer código)
- Leia atentamente os READMEs e docs relevantes do repositório: `master.md`, `e-engineer-backend/docs/codex.md`, `e-engineer-frontend/codex.md`, `docs/API-CONTRACTS.md`, `README-CODEX-PROMPT.md`, além de `e-engineer-backend/README.md` e `e-engineer-frontend/README.md`. Confirme que leu e resuma em 3–6 pontos os limites arquiteturais e regras de negócio que impactam a tarefa.
- Não gere código antes de explicar a abordagem e listar os arquivos exatos (criados/alterados) que pretende tocar.
- Se houver qualquer dúvida arquitetural, de negócio, ou necessidade de alteração de modelo/dados/infra, pergunte ao usuário; NÃO ADVINHE nem decida sozinho.

Princípios e limites arquiteturais
- Siga Clean Architecture + DDD do projeto: separar `domain`, `application`, `infrastructure`, `presentation`.
- Não use entidades TypeORM como entidades de domínio. Use ValueObjects, Entities e Repositories no domínio; TypeORM apenas na infraestrutura.
- Multi‑tenant: `organizationId` é obrigatório em entidades de negócio e nunca deve ser assumido do body sem validação a partir do token do usuário.
- Controllers: finos — validação superficial e delegação a use cases.
- Repositórios: interfaces no domínio/aplicação; implementações em infraestrutura.
- Reaproveite padrões existentes (`TenantScopedOrmEntity`, `UniqueEntityId`, `OrganizationId`, `ok()` envelope, `JwtAuthGuard`, event bus in‑process).

Processo de implementação (passos mínimos)
1. Leitura & resumo: indique 3–6 pontos chave do que foi lido que influenciam a tarefa.
2. Proposta: descreva a abordagem, lista de arquivos a criar/editar e razões arquiteturais (2–6 linhas).
3. Especificação de mudanças de dados: indique se precisa migration e explique por quê.
4. Implementação incremental: implemente em pequenos cortes coesos (por arquivo/submódulo).
5. Testes: escreva testes unitários para domain/use-cases e testes de integração/E2E quando envolver persistência/HTTP/arquivos. Prioridade: saúde do projeto sobre quantidade de testes.
6. Execução de validações: rode `npm run type-check`, `npm run test` e `npm run test:e2e` (ou scripts análogos) e cole os resultados/resumo do que passou/ falhou.
7. Entrega: antes de declarar pronta a tarefa, forneça:
   - Comandos executados e saída relevante.
   - Lista de cenários testados manualmente/automatizados (pelo menos 3 cenários relevantes).
   - Dif com arquivos criados/alterados.
   - Sugestão de mensagem de commit coesa.
8. Auditoria: adicione uma entrada datada em `e-engineer-backend/codex.md` ou `e-engineer-frontend/codex.md` (conforme escopo) descrevendo decisões arquiteturais, trade‑offs e links para os arquivos alterados.

Regras sobre decisões e perguntas
- Se uma decisão impacta modelo de dados, tenancy, segurança, autenticação ou contratos públicos, pare e questione o usuário antes de aplicar.
- Se for necessário integrar serviços externos (S3, AWS, email, etc.), peça credenciais ou proponha um mock/local emulator; nunca comite credenciais.
- Se houver incerteza sobre o impacto em outras áreas, proponha uma alternativa de menor risco (feature flag, endpoint experimental, migration reversível).

Testes e validação (obrigatórios antes de "pronto")
- Sempre inclua testes unitários para domínio/use cases. Para alterações com persistência/HTTP, inclua testes de integração ou mock do DB.
- Execute os scripts de teste e linters disponíveis; inclua os comandos e o resumo dos resultados no relatório de entrega.
- Liste os cenários testados (ex.: criação válida, payload inválido, isolamento tenant, aprovação/negação, upload de arquivo com falha/êxito).

Boas práticas de código e revisão
- Faça commits pequenos e coerentes; um único propósito por commit.
- Não altere estilos e formatação em arquivos não relacionados.
- Documente brevemente as decisões técnicas no `codex.md` com data, autor e justificativa.
- Mantenha a legibilidade e evite complexidade desnecessária; prefira soluções simples que respeitem limites arquiteturais.

Template de entrada de auditoria a ser adicionada ao `codex.md`
- Data: YYYY-MM-DD
- Tarefa: [ID/Título da task]
- Mudanças: lista de arquivos alterados (paths)
- Decisão tomada: curta descrição e motivo
- Alternativas consideradas
- Tests executados: lista de cenários e resultado
- Observações / Próximos passos

Segurança e infra
- Não commit secrets. Se precisar de variáveis, documente-as em `.env.example` e instruções de setup no README.
- Para S3 ou serviços externos, oferecer opção de usar emulator local (MinIO) para desenvolvimento.

Formato de resposta esperado do Codex quando chamado com uma tarefa
1. Resumo de leitura (3–6 pontos).
2. Lista de perguntas abertas (se houver).
3. Plano curto (arquivos a criar/editar, migrations, testes).
4. Implementação — cortes pequenos com explicação por corte.
5. Testes executados e logs/resumos.
6. Registro de auditoria pronto para colar em `codex.md`.
7. Sugestão de mensagem de commit e comandos para rodar localmente.