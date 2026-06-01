# 03 — Fluxos de Negócio

## 1. Objetivo deste documento

Este documento descreve os fluxos ideais da plataforma. Ele deve orientar implementação, criação de tarefas, desenho de telas, endpoints, casos de uso e validação de UX.

O foco não é apenas documentar o que existe hoje, mas representar o fluxo dos sonhos: a jornada ideal para que uma empresa de engenharia consiga sair da desorganização e operar com padronização, rastreabilidade e reutilização de conhecimento.

## 2. Macrofluxo ideal da plataforma

O fluxo macro ideal é:

```text
Organização configura seu ambiente
→ cadastra colaboradores
→ cria ou importa padrões técnicos
→ cria base de conhecimento
→ inicia estudo de viabilidade ou projeto técnico
→ aplica template/padrões
→ gera entregáveis
→ produz documentos
→ controla versões
→ solicita revisões
→ aprova/reprova tecnicamente
→ marca versões oficiais
→ conclui entregáveis
→ registra aprendizado
→ promove projeto/documento para conhecimento reutilizável
```

Esse macrofluxo deve guiar todas as decisões de produto.

## 3. Fluxo 1 — Onboarding da organização

### Objetivo

Permitir que uma empresa comece a usar a plataforma com uma estrutura mínima de operação.

### Atores

- owner;
- admin;
- coordenador técnico.

### Fluxo ideal

```text
1. Usuário cria conta ou recebe convite.
2. Usuário cria organização.
3. Informa nome fantasia, razão social e dados básicos.
4. Define área de atuação principal.
5. Convida colaboradores.
6. Define papéis.
7. Sistema sugere templates iniciais.
8. Sistema sugere tipos de entregáveis padrão.
9. Organização entra no dashboard inicial.
```

### Dados importantes

- nome da organização;
- slug;
- colaboradores;
- papéis;
- tipos de projeto mais comuns;
- preferências operacionais.

### Resultado esperado

A organização está pronta para criar projetos técnicos e começar a registrar conhecimento.

## 4. Fluxo 2 — Criação de projeto técnico

### Objetivo

Criar um projeto técnico de engenharia de forma estruturada, evitando que ele nasça como apenas um registro vazio.

### Atores

- owner;
- admin;
- coordenador;
- engenheiro.

### Fluxo ideal

```text
1. Usuário clica em Novo projeto.
2. Informa nome do projeto.
3. Informa cliente/prefeitura.
4. Seleciona tipo do projeto.
5. Informa responsável técnico.
6. Informa prazo geral.
7. Adiciona tags.
8. Sistema sugere templates compatíveis.
9. Sistema sugere projetos de referência da Base de Conhecimento.
10. Usuário escolhe se deseja aplicar template.
11. Sistema gera entregáveis padrão.
12. Sistema cria projeto e registra evento.
13. Usuário é direcionado para o cockpit do projeto.
```

### Variação futura com Estudo de Viabilidade

```text
1. Usuário cria estudo de viabilidade.
2. Sistema retorna análise urbanística.
3. Usuário clica em Criar projeto a partir deste estudo.
4. Projeto herda endereço, zona, parâmetros, tags e documentos gerados.
5. Sistema sugere template conforme tipo e contexto.
```

### Resultado esperado

O projeto nasce com estrutura mínima:

- status;
- responsável;
- entregáveis;
- documentos esperados;
- referências sugeridas;
- histórico inicial.

## 5. Fluxo 3 — Aplicação de template ao projeto

### Objetivo

Padronizar projetos com base em modelos técnicos reutilizáveis.

### Atores

- coordenador;
- admin;
- owner.

### Fluxo ideal

```text
1. Usuário acessa projeto.
2. Clica em Aplicar template.
3. Sistema mostra templates compatíveis.
4. Usuário visualiza entregáveis que serão criados.
5. Usuário visualiza documentos esperados.
6. Usuário visualiza checklist/revisões sugeridas.
7. Usuário confirma aplicação.
8. Sistema cria entregáveis e checklists.
9. Sistema registra evento Template aplicado.
```

### Regras

- template deve pertencer à organização;
- template publicado é preferencial;
- projeto pode ter apenas um template principal, mas pode usar itens adicionais da Base de Conhecimento;
- entregáveis duplicados devem ser tratados com cuidado.

### Resultado esperado

O projeto deixa de depender da memória do coordenador para saber “o que precisa ser feito”.

## 6. Fluxo 4 — Gestão de entregáveis

### Objetivo

Controlar o pacote técnico de produção do projeto.

### Atores

- coordenador;
- engenheiro;
- projetista;
- responsável técnico.

### Fluxo ideal

```text
1. Usuário acessa projeto.
2. Visualiza entregáveis em quadro ou tabela.
3. Cada entregável possui status, responsável, prazo e tipo.
4. Usuário altera status conforme avanço.
5. Usuário adiciona descrição, bloqueio ou observação.
6. Usuário cria documentos vinculados ao entregável.
7. Sistema calcula progresso do projeto.
8. Sistema alerta entregáveis atrasados ou bloqueados.
```

### Status recomendados

- A produzir;
- Em produção;
- Bloqueado;
- Em revisão;
- Concluído;
- Atrasado.

### Resultado esperado

O projeto passa a ter uma visão clara do que precisa ser produzido e do que está travado.

## 7. Fluxo 5 — Criação de documento técnico

### Objetivo

Registrar documento técnico vinculado a projeto e entregável, com controle de tipo, status e versão.

### Atores

- engenheiro;
- projetista;
- coordenador;
- administrativo técnico.

### Fluxo ideal

```text
1. Usuário acessa Documentos ou detalhe do Projeto.
2. Clica em Novo documento.
3. Seleciona projeto.
4. Seleciona entregável vinculado.
5. Informa título técnico.
6. Informa descrição.
7. Seleciona tipo de documento.
8. Define status inicial.
9. Envia arquivo da primeira versão.
10. Informa código de revisão.
11. Informa notas da versão.
12. Define se é versão oficial.
13. Opcionalmente indica responsável pela revisão.
14. Sistema salva documento e versão.
15. Sistema registra evento Documento enviado.
```

### Resultado esperado

O documento já nasce rastreável e conectado ao projeto, não como anexo solto.

## 8. Fluxo 6 — Nova versão de documento

### Objetivo

Controlar evolução documental sem perder histórico.

### Atores

- engenheiro;
- projetista;
- coordenador.

### Fluxo ideal

```text
1. Usuário acessa documento.
2. Clica em Nova versão.
3. Envia novo arquivo.
4. Informa código de revisão.
5. Informa notas da versão.
6. Define se deseja solicitar revisão.
7. Sistema registra nova versão.
8. Se marcada como oficial, sistema remove oficialidade da versão anterior.
9. Sistema registra evento Nova versão enviada.
```

### Regras

- uma versão deve ter autor;
- uma versão deve ter data de upload;
- idealmente uma versão deve ter código de revisão;
- apenas uma versão oficial por documento;
- marcar oficial deve ser evento auditável.

### Resultado esperado

A equipe sabe exatamente qual versão é a atual/oficial e quais versões anteriores existiram.

## 9. Fluxo 7 — Marcar versão oficial

### Objetivo

Definir qual versão de documento representa a entrega válida ou referência atual.

### Atores

- coordenador;
- responsável técnico;
- admin;
- owner.

### Fluxo ideal

```text
1. Usuário acessa histórico de versões.
2. Seleciona uma versão.
3. Clica em Marcar como oficial.
4. Sistema pede confirmação.
5. Sistema remove oficialidade de versões anteriores.
6. Sistema marca nova versão como oficial.
7. Sistema registra ator, data e motivo opcional.
8. Sistema registra evento no projeto.
```

### Resultado esperado

Não existe ambiguidade sobre qual arquivo deve ser usado.

## 10. Fluxo 8 — Solicitação de revisão técnica

### Objetivo

Formalizar revisão de documento, versão, entregável ou projeto.

### Atores

- solicitante;
- revisor;
- coordenador.

### Fluxo ideal

```text
1. Usuário seleciona documento, versão ou entregável.
2. Clica em Solicitar revisão.
3. Informa título da revisão.
4. Informa descrição/contexto.
5. Escolhe revisor.
6. Define prazo.
7. Sistema cria revisão pendente.
8. Revisor recebe notificação ou visualiza na tela de Revisões.
9. Sistema registra evento Revisão solicitada.
```

### Resultado esperado

Revisão deixa de ser conversa informal e passa a ter dono, prazo, alvo e histórico.

## 11. Fluxo 9 — Aprovação ou reprovação de revisão

### Objetivo

Registrar decisão técnica.

### Atores

- revisor;
- coordenador;
- responsável técnico.

### Fluxo de aprovação

```text
1. Revisor abre revisão.
2. Analisa contexto e documento.
3. Clica em Aprovar.
4. Informa comentário opcional.
5. Sistema marca revisão como aprovada.
6. Opcionalmente marca versão como oficial.
7. Sistema registra evento Revisão aprovada.
```

### Fluxo de reprovação

```text
1. Revisor abre revisão.
2. Analisa contexto e documento.
3. Clica em Reprovar.
4. Informa motivo obrigatório.
5. Sistema marca revisão como reprovada.
6. Sistema pode alterar status do entregável/documento.
7. Sistema sugere registrar lição aprendida.
8. Sistema registra evento Revisão reprovada.
```

### Resultado esperado

Toda decisão técnica fica rastreável e pode virar aprendizado.

## 12. Fluxo 10 — Promover projeto para Base de Conhecimento

### Objetivo

Transformar um projeto finalizado ou relevante em referência reutilizável.

### Atores

- coordenador;
- admin;
- owner;
- responsável técnico.

### Fluxo ideal

```text
1. Usuário acessa projeto concluído ou maduro.
2. Clica em Adicionar à Base de Conhecimento.
3. Seleciona tipo: Projeto de referência.
4. Sistema pré-preenche título, descrição, cliente, tipo e tags.
5. Usuário seleciona entregáveis úteis.
6. Usuário seleciona documentos que podem servir de referência.
7. Usuário adiciona observações.
8. Usuário adiciona lições aprendidas.
9. Usuário define status como rascunho ou publicado.
10. Sistema cria KnowledgeItem vinculado ao projeto.
11. Sistema registra evento Projeto promovido para conhecimento.
```

### Resultado esperado

O histórico da empresa deixa de ficar perdido e passa a alimentar projetos futuros.

## 13. Fluxo 11 — Criar item manual na Base de Conhecimento

### Objetivo

Permitir que a empresa registre conhecimento independente de um projeto específico.

### Atores

- coordenador;
- engenheiro;
- admin;
- owner.

### Fluxo ideal

```text
1. Usuário acessa Base de Conhecimento.
2. Clica em Novo item.
3. Escolhe tipo do item.
4. Preenche título e descrição.
5. Adiciona conteúdo estruturado.
6. Adiciona tags.
7. Vincula projetos, documentos ou templates, se existirem.
8. Salva como rascunho ou publica.
```

### Tipos iniciais

- Padrão técnico;
- Documento modelo;
- Projeto de referência;
- Lição aprendida;
- Checklist de revisão.

## 14. Fluxo 12 — Usar item de conhecimento em projeto

### Objetivo

Fazer a Base de Conhecimento impactar a operação real.

### Atores

- coordenador;
- engenheiro;
- projetista.

### Fluxo ideal

```text
1. Usuário acessa projeto.
2. Sistema mostra conhecimento recomendado por tags/tipo.
3. Usuário abre item recomendado.
4. Clica em Usar neste projeto.
5. Sistema registra vínculo.
6. Se for documento modelo, permite criar documento a partir dele.
7. Se for checklist, adiciona checklist ao projeto/entregável.
8. Se for projeto de referência, vincula como referência.
9. Sistema registra uso do conhecimento.
```

### Resultado esperado

A base deixa de ser arquivo morto e passa a influenciar projetos novos.

## 15. Fluxo 13 — Sugestão automática de conhecimento

### Objetivo

Dar sensação de inteligência sem necessariamente usar IA inicialmente.

### Estratégia MVP

Usar regras simples:

```text
Se projeto possui tag 'UBS'
→ recomendar itens com tag 'UBS'

Se projeto é de pavimentação
→ recomendar templates/documentos/checklists de pavimentação

Se entregável é orçamento
→ recomendar padrões e lições de orçamento

Se revisão foi reprovada por divergência de quantitativos
→ sugerir lições aprendidas sobre quantitativos
```

### Resultado esperado

Usuário percebe que o sistema ajuda ativamente.

## 16. Fluxo 14 — Saúde técnica do projeto

### Objetivo

Mostrar risco operacional e técnico de forma simples.

### Cálculo inicial possível

Critérios negativos:

- entregáveis atrasados;
- entregáveis bloqueados;
- documentos sem versão oficial;
- revisões pendentes vencidas;
- projeto sem responsável;
- projeto sem template aplicado;
- projeto sem conhecimento vinculado;
- documentos reprovados.

Classificação:

- Boa;
- Atenção;
- Crítica.

### Fluxo ideal

```text
1. Sistema calcula saúde técnica.
2. Exibe no dashboard e no projeto.
3. Mostra motivos.
4. Sugere ações.
```

Exemplo:

```text
Saúde técnica: Atenção
Motivos:
- 2 entregáveis bloqueados
- 1 documento sem versão oficial
- 1 revisão atrasada
```

## 17. Fluxo 15 — Estudo de viabilidade urbanística futuro

### Objetivo

Criar a porta de entrada inteligente do produto.

### Fluxo dos sonhos

```text
1. Usuário clica em Novo Estudo de Viabilidade.
2. Informa endereço, SQL/IPTU ou coordenada.
3. Sistema geocodifica/localiza terreno.
4. Sistema consulta base urbanística.
5. Sistema retorna zona, parâmetros, fontes e alertas.
6. Sistema gera relatório preliminar.
7. Usuário salva estudo.
8. Usuário cria projeto técnico a partir do estudo.
9. Sistema recomenda template e conhecimento.
```

### Resultado esperado

O produto passa a começar antes do projeto, apoiando a tomada de decisão inicial.

## 18. Prioridade de implementação sugerida

Ordem recomendada após documentação:

1. Base de Conhecimento funcional;
2. vínculo entre KnowledgeItem e Project;
3. promover projeto para conhecimento;
4. usar conhecimento em projeto;
5. recomendações por tags;
6. saúde técnica do projeto;
7. dashboard com alertas inteligentes;
8. estudo de viabilidade mockado;
9. estudo de viabilidade com dados reais.

## 19. Princípio final dos fluxos

O usuário não deve apenas cadastrar coisas. Ele deve ser guiado.

O produto deve sempre tentar responder:

- o que está pendente?
- qual versão é oficial?
- quem precisa revisar?
- qual padrão devo usar?
- já fizemos algo parecido?
- que erro devo evitar?
- o que pode virar conhecimento para o futuro?
