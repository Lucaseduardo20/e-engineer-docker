# Épico 2 — Backlog Estruturado

# Cockpit Técnico do Projeto, Taxonomia do Tenant e Conhecimento Aplicado

## 1. Visão geral do épico

Este documento detalha as tarefas do Épico 2 da plataforma E-Engineer.

O objetivo deste épico é transformar a tela de detalhe do projeto em um cockpit técnico operacional, conectando entregáveis, documentos, revisões, riscos e conhecimentos aplicados/recomendados.

A tese central do produto permanece:

> Projetos geram conhecimento. Conhecimento melhora novos projetos.

Após o Épico 1, a plataforma passou a possuir uma Base de Conhecimento funcional, com criação, edição, publicação, arquivamento, depreciação, relações, promoção de projeto, documento como modelo, revisão como lição aprendida, activity log, permissões e demo flow.

Porém, o valor da Knowledge Base ainda precisa aparecer de forma mais natural dentro do fluxo principal do usuário: o projeto.

O usuário não deve depender de entrar manualmente na Base de Conhecimento, procurar itens, entender tipos de relação e vincular tudo por conta própria.

A plataforma deve levar o conhecimento certo para o contexto certo.

Este épico trabalha três frentes principais:

1. Taxonomia técnica governada do tenant;
2. Cockpit técnico do projeto;
3. Conhecimento aplicado e recomendado dentro do fluxo operacional.

---

## 2. Problema que o épico resolve

Empresas de engenharia sofrem com perda de conhecimento operacional.

O conhecimento técnico normalmente fica espalhado entre:

* Drive;
* WhatsApp;
* documentos antigos;
* planilhas;
* memória de coordenadores;
* revisões reprovadas;
* arquivos duplicados;
* modelos não padronizados;
* padrões informais.

Mesmo quando a empresa já possui projetos anteriores bons, documentos úteis e aprendizados importantes, essas informações raramente aparecem no momento certo para orientar um novo projeto.

Além disso, se tags forem livres demais, a plataforma perde capacidade de recomendação e inteligência. Tags como `ubs`, `UBS`, `saude`, `saúde`, `orçamento`, `orcamento`, `obra`, `teste` e `importante` criam ruído e reduzem a utilidade da base.

Este épico resolve três dores:

1. O projeto ainda não comunica claramente o que precisa de atenção;
2. A Knowledge Base ainda exige esforço manual demais para gerar valor;
3. As tags precisam deixar de ser texto solto e virar uma taxonomia técnica confiável.

---

## 3. Resultado esperado do épico

Ao final deste épico, o usuário deve conseguir abrir um projeto e entender rapidamente:

* situação geral do projeto;
* entregáveis em produção, atrasados ou bloqueados;
* documentos oficiais, minutas e pendências;
* revisões pendentes ou reprovadas;
* conhecimentos já aplicados ao projeto;
* conhecimentos recomendados pela plataforma;
* riscos e lições aprendidas aplicáveis;
* padrões e checklists relevantes;
* próximas ações operacionais.

O projeto deve parecer menos uma tela administrativa e mais um cockpit técnico.

---

## 4. Princípios de produto

### 4.1 O projeto é o centro da operação

O usuário trabalha em projetos, não em módulos isolados.

A Base de Conhecimento deve apoiar o projeto, não competir com ele.

---

### 4.2 O entregável é o eixo técnico

A plataforma não deve virar um gerenciador genérico de tarefas.

O foco deve ser o entregável técnico:

* projeto arquitetônico;
* projeto estrutural;
* orçamento;
* memorial;
* cronograma;
* ART/RRT;
* relatório;
* pacote técnico.

---

### 4.3 O usuário não deve entender complexidade interna

Conceitos como `relationType`, `targetType`, `based_on`, `lesson_from` e `standard_for` pertencem ao domínio interno.

Na interface, o usuário deve ver ações como:

* Aplicar checklist;
* Usar como referência;
* Aplicar padrão;
* Usar documento modelo;
* Registrar lição aprendida;
* Ver recomendação;
* Aplicar ao projeto.

---

### 4.4 Tags são infraestrutura de inteligência

Tags não são detalhes visuais.

Tags serão usadas para:

* busca;
* filtros;
* recomendações;
* riscos;
* agrupamentos;
* inteligência futura;
* embeddings no futuro;
* entendimento do contexto técnico do tenant.

Por isso, precisam ser governadas.

---

## 5. Ordem estratégica recomendada

A ordem recomendada para execução é:

1. Taxonomia técnica do tenant;
2. Autocomplete e governança de tags;
3. Redesign estrutural do cockpit do projeto;
4. Visão rica dos entregáveis;
5. Aplicação de knowledge em entregáveis;
6. Recomendações simples por tags;
7. Riscos e aprendizados aplicáveis;
8. Fluxos guiados de vínculo;
9. Ajuste de demo flow;
10. Documentação e testes do épico.

A taxonomia vem antes das recomendações porque recomendação ruim nasce de contexto ruim.

---

# Task 1 — Criar domínio de Taxonomia Técnica do Tenant

## Objetivo

Transformar tags livres em entidades governadas por organização, criando a base semântica para recomendações, filtros e inteligência operacional.

## Contexto

Hoje, tags podem ser digitadas livremente em campos separados por vírgula. Isso permite duplicidade, ruído, variações de escrita e tags sem valor técnico.

Exemplos problemáticos:

* `ubs`;
* `UBS`;
* `unidade saude`;
* `unidade de saúde`;
* `orcamento`;
* `orçamento`;
* `teste`;
* `abc`;
* `importante`.

Esse modelo compromete a capacidade da plataforma de recomendar conhecimento com qualidade.

## O que deve ser feito

Criar um novo conceito de domínio para tags governadas por tenant.

Nome sugerido:

* `TechnicalTag`;
* ou `TenantTag`;
* ou `KnowledgeTag`.

Recomendação:

```txt
TechnicalTag
```

Porque a tag não será usada apenas na Knowledge Base, mas em projetos, entregáveis, documentos e revisões.

A entidade deve possuir:

* id;
* organizationId;
* name;
* slug;
* category;
* description;
* status;
* createdBy;
* updatedBy;
* createdAt;
* updatedAt;
* archivedAt, se fizer sentido;
* deprecatedAt, se fizer sentido.

## Categorias iniciais

Criar categorias controladas:

* project_type;
* technical_discipline;
* document_type;
* operational_pain;
* client_context;
* project_stage;
* knowledge_purpose.

Labels amigáveis:

* Tipo de projeto;
* Disciplina técnica;
* Tipo de documento;
* Dor operacional;
* Contexto de cliente/órgão;
* Etapa do projeto;
* Finalidade do conhecimento.

## Status iniciais

Criar status:

* active;
* pending_review;
* deprecated;
* archived.

## Regras de negócio

* Tag pertence obrigatoriamente a uma organização.
* Tag deve ter nome.
* Tag deve ter slug único por organização.
* Tag deve ter categoria.
* Não permitir duas tags equivalentes no mesmo tenant.
* Criar normalização para slug.
* Tags archived não devem aparecer para seleção.
* Tags deprecated podem aparecer como histórico, mas não devem ser recomendadas.
* Tags pending_review podem existir, mas devem ser sinalizadas.

## Backend

Criar:

* entidade de domínio;
* enum/value object de categoria;
* enum/value object de status;
* contrato de repositório;
* entidade ORM;
* migration;
* mapper;
* implementação do repositório;
* seeds iniciais por organização.

## Frontend

Nesta task, frontend pode ser mínimo ou inexistente.

No máximo, preparar tipos TypeScript se necessário.

## Critérios de aceite

* TechnicalTag existe no domínio.
* Migration cria tabela de tags.
* Tags respeitam organizationId.
* Slug é normalizado.
* Não é possível criar duplicata grosseira.
* Categorias existem.
* Status existem.
* Seeds criam tags úteis para a demo.
* Código respeita DDD/Clean Architecture.

## QA — Cenários mínimos

### Cenário 1.1 — Criar tag válida

Criar tag “UBS” na categoria “Tipo de projeto”.

Resultado esperado:

* tag criada;
* slug `ubs`;
* status active;
* organizationId preenchido.

### Cenário 1.2 — Evitar duplicidade

Tentar criar `UBS`, `ubs` e `U.B.S`.

Resultado esperado:

* sistema bloqueia ou reaproveita tag existente;
* não cria duplicatas.

### Cenário 1.3 — Isolamento por tenant

Criar tag `UBS` em duas organizações diferentes.

Resultado esperado:

* permitido;
* cada organização possui sua própria tag.

---

# Task 2 — Criar casos de uso e endpoints para gestão de tags

## Objetivo

Permitir criar, listar, editar, arquivar e depreciar tags técnicas do tenant via API.

## Contexto

A taxonomia precisa ser gerenciável para que o tenant consiga evoluir seu vocabulário técnico.

## O que deve ser feito

Criar use cases:

* CreateTechnicalTagUseCase;
* ListTechnicalTagsUseCase;
* UpdateTechnicalTagUseCase;
* ArchiveTechnicalTagUseCase;
* DeprecateTechnicalTagUseCase;
* GetTechnicalTagDetailsUseCase, se fizer sentido.

Criar endpoints:

```txt
POST /technical-tags
GET /technical-tags
GET /technical-tags/:id
PATCH /technical-tags/:id
POST /technical-tags/:id/archive
POST /technical-tags/:id/deprecate
```

Query params de listagem:

* search;
* category;
* status;
* includeArchived;
* page;
* limit.

## Regras de negócio

* Apenas membros da organização podem listar tags.
* Apenas usuários autorizados podem criar/editar/arquivar/depreciar.
* Tags usadas em itens existentes não devem ser apagadas fisicamente.
* Arquivar remove da seleção padrão.
* Depreciar mantém histórico, mas sinaliza uso não recomendado.

## Permissões sugeridas

* owner/admin/coordinator: gerenciam tags;
* engineer: pode sugerir/criar pending_review, se adotado;
* viewer: apenas consulta tags active;
* para MVP, engineer pode criar active ou pending_review conforme decisão técnica.

Recomendação para MVP:

```txt
owner/admin/coordinator criam active.
engineer cria pending_review.
viewer não cria.
```

Se isso for complexo, permitir owner/admin/coordinator apenas.

## Critérios de aceite

* Endpoints existem.
* Listagem filtra por categoria/status/busca.
* Criação normaliza slug.
* Edição mantém unicidade.
* Arquivamento funciona.
* Depreciação funciona.
* Backend protege por organizationId.
* Backend protege por permissão.

## QA — Cenários mínimos

* Criar tag.
* Editar nome e descrição.
* Filtrar por categoria.
* Filtrar por status.
* Arquivar tag.
* Depreciar tag.
* Garantir que tag arquivada não aparece por padrão.
* Usuário sem permissão não cria tag.
* Usuário de outro tenant não acessa tag.

---

# Task 3 — Migrar KnowledgeItem para usar tags governadas

## Objetivo

Substituir ou complementar o modelo atual de tags em texto por vínculos com tags governadas do tenant.

## Contexto

KnowledgeItems ainda usam tags livres. Para que recomendações sejam confiáveis, os itens precisam referenciar tags reais.

## O que deve ser feito

Definir estratégia de persistência:

Opção A:

```txt
knowledge_items.tags continua como array de strings
```

e adiciona relação nova:

```txt
knowledge_item_tags
```

Opção B:

```txt
substituir tags por relation table
```

Recomendação:

Usar tabela relacional:

```txt
knowledge_item_tags
```

Campos:

* id;
* organizationId;
* knowledgeItemId;
* tagId;
* createdAt;
* createdBy.

Manter `tags` textual temporariamente apenas se necessário para compatibilidade.

Criar use cases/ajustes:

* criação de KnowledgeItem usando tagIds;
* edição de KnowledgeItem usando tagIds;
* listagem retornando tags resolvidas;
* detalhe retornando tags resolvidas;
* seeds atualizados.

## Regras de negócio

* KnowledgeItem só pode usar tags da mesma organização.
* Não permitir tag archived em novo vínculo.
* Tag deprecated pode ser usada com alerta ou bloqueio.
* Não permitir tag duplicada no mesmo item.
* Tags devem ser retornadas com id, name, slug e category.

## Backend

Atualizar:

* DTOs;
* mappers;
* repositórios;
* use cases;
* seeds;
* endpoints de create/update/list/detail.

## Frontend

Ainda pode manter compatibilidade temporária, mas preparar para receber tags como objetos.

## Critérios de aceite

* KnowledgeItem usa tags governadas.
* Listagem exibe tags corretamente.
* Detalhe exibe tags corretamente.
* Criação não aceita tag de outro tenant.
* Edição não aceita tag archived.
* Seeds continuam funcionando.
* Busca por tag funciona com nova estrutura.

## QA — Cenários mínimos

* Criar item com tags existentes.
* Editar tags do item.
* Remover tag do item.
* Tentar usar tag de outro tenant.
* Tentar usar tag archived.
* Ver tags na listagem.
* Ver tags no detalhe.
* Buscar item por tag.

---

# Task 4 — Criar componente de seleção de tags no frontend

## Objetivo

Substituir campos de texto livre por um componente reutilizável de autocomplete e seleção de tags governadas.

## Contexto

O usuário não deve digitar tags separadas por vírgula. Ele deve selecionar tags existentes e, quando permitido, criar novas tags de forma controlada.

## O que deve ser feito

Criar componente:

```txt
TechnicalTagSelector
```

ou:

```txt
TenantTagSelector
```

Recomendação:

```txt
TechnicalTagSelector
```

Funcionalidades:

* buscar tags por texto;
* filtrar por categoria, se configurado;
* exibir categoria da tag;
* selecionar múltiplas tags;
* remover tag selecionada;
* criar nova tag, se usuário tiver permissão;
* impedir duplicidade;
* sinalizar tag deprecated;
* ocultar archived.

## Aplicar inicialmente em

* formulário de criação de KnowledgeItem;
* formulário de edição de KnowledgeItem;
* fluxo de promover projeto como referência;
* fluxo de salvar documento como modelo;
* fluxo de registrar revisão como lição aprendida.

## UX esperada

Ao digitar “orça”, sugerir:

* Orçamento;
* Revisão de orçamento;
* Quantitativos divergentes.

Se não existir:

```txt
Criar nova tag "orçamento executivo"
```

Ao criar nova tag, pedir:

* nome;
* categoria;
* descrição opcional.

## Critérios de aceite

* Campo de tags livres não é mais usado nos principais formulários.
* Usuário seleciona tags existentes.
* Usuário autorizado cria tag nova.
* Usuário sem permissão não cria tag nova.
* Categorias aparecem.
* Deprecated aparece com alerta.
* Archived não aparece.
* Formulários salvam tagIds.

## QA — Cenários mínimos

* Buscar tag existente.
* Selecionar múltiplas tags.
* Remover tag.
* Criar tag nova com categoria.
* Tentar criar tag duplicada.
* Ver tag deprecated sinalizada.
* Garantir que archived não aparece.
* Salvar KnowledgeItem com tags selecionadas.

---

# Task 5 — Criar tela de Taxonomia Técnica na Organização

## Objetivo

Permitir que administradores/coordenadores gerenciem a taxonomia técnica do tenant.

## Contexto

Para a taxonomia ser confiável, precisa existir uma área de governança simples.

## O que deve ser feito

Criar seção em Organização:

```txt
Taxonomia técnica
```

Funcionalidades:

* listar tags;
* buscar tags;
* filtrar por categoria;
* filtrar por status;
* criar tag;
* editar tag;
* arquivar tag;
* depreciar tag;
* ver contagem de uso, se disponível.

## UI

A tela deve ser simples e administrativa.

Colunas/cards:

* nome;
* slug;
* categoria;
* status;
* descrição;
* uso;
* ações.

## Regras de UX

* Não parecer tela técnica demais.
* Explicar que tags ajudam recomendações e organização do conhecimento.
* Alertar antes de arquivar/depreciar.
* Não permitir exclusão destrutiva no MVP.

## Critérios de aceite

* Admin acessa tela.
* Coordinator acessa tela.
* Engineer não gerencia, salvo regra adotada.
* Viewer não gerencia.
* Tags podem ser criadas/editadas.
* Tags podem ser arquivadas/depreciadas.
* Uso da tag aparece, se implementado.
* UI é consistente com a plataforma.

## QA — Cenários mínimos

* Listar tags.
* Criar tag.
* Editar tag.
* Arquivar tag.
* Depreciar tag.
* Filtrar por categoria.
* Filtrar por status.
* Usuário sem permissão não acessa ações.

---

# Task 6 — Redesenhar estrutura do detalhe do projeto como Cockpit Técnico

## Objetivo

Reorganizar a tela de detalhe do projeto para que ela comunique a situação operacional e técnica do projeto de forma clara.

## Contexto

Hoje o detalhe do projeto já exibe informações importantes, mas a seção de conhecimento aplicado ainda parece uma lista técnica simples. O projeto precisa virar o cockpit principal da plataforma.

## O que deve ser feito

Redesenhar a estrutura da tela com seções:

1. Header executivo;
2. Indicadores rápidos;
3. Resumo operacional;
4. Entregáveis;
5. Documentos;
6. Revisões;
7. Conhecimento aplicado;
8. Recomendações;
9. Riscos e aprendizados;
10. Histórico.

## Header executivo

Exibir:

* nome;
* cliente;
* status;
* progresso;
* responsável;
* prazo;
* ações principais.

## Indicadores rápidos

Exibir cards pequenos:

* entregáveis totais;
* entregáveis atrasados;
* documentos oficiais;
* revisões pendentes;
* revisões reprovadas;
* conhecimentos aplicados;
* recomendações disponíveis.

## Backend

Pode ser necessário criar endpoint de resumo:

```txt
GET /projects/:projectId/technical-summary
```

Ou incluir dados no detalhe do projeto.

Recomendação:

Criar use case dedicado:

```txt
GetProjectTechnicalCockpitUseCase
```

## Critérios de aceite

* Detalhe do projeto fica organizado em cockpit.
* Usuário entende situação geral em poucos segundos.
* Indicadores aparecem corretamente.
* Conhecimento aplicado não fica solto.
* Estados vazios são claros.
* UI continua responsiva para desktop/notebook.

## QA — Cenários mínimos

* Abrir projeto com dados completos.
* Abrir projeto sem documentos.
* Abrir projeto sem revisões.
* Abrir projeto com knowledge aplicado.
* Ver indicadores corretos.
* Validar loading/error/empty state.

---

# Task 7 — Criar visão rica de entregáveis técnicos

## Objetivo

Fazer entregáveis virarem o eixo operacional principal dentro do projeto.

## Contexto

A dor de engenharia gira em torno de entregáveis. Cada entregável pode ter documentos, revisões, responsáveis, prazos, status e conhecimentos aplicados.

## O que deve ser feito

Criar componente:

```txt
ProjectDeliverableTechnicalCard
```

Cada card deve exibir:

* nome;
* tipo;
* status;
* responsável;
* prazo;
* atraso, se houver;
* documentos vinculados;
* revisões vinculadas;
* knowledge aplicado;
* pendências;
* ações.

## Agrupamentos

Permitir visualizar entregáveis por:

* status;
* disciplina;
* responsável;
* prazo;
* etapa.

Para MVP, manter agrupamento simples por status.

## Critérios de aceite

* Entregáveis aparecem como cards ricos.
* Usuário vê documentos vinculados.
* Usuário vê revisões vinculadas.
* Usuário vê knowledge aplicado ao entregável, se houver.
* Entregável atrasado é sinalizado.
* Entregável bloqueado é sinalizado.
* Card permite abrir/gerenciar entregável.

## QA — Cenários mínimos

* Entregável sem documentos.
* Entregável com documentos.
* Entregável com revisão reprovada.
* Entregável com knowledge aplicado.
* Entregável atrasado.
* Entregável bloqueado.
* Responsividade.

---

# Task 8 — Permitir aplicar KnowledgeItem diretamente em entregáveis

## Objetivo

Permitir que o conhecimento seja aplicado não só ao projeto, mas também a entregáveis específicos.

## Contexto

Um checklist de orçamento faz mais sentido aplicado ao entregável “Orçamento” do que ao projeto inteiro.

Um documento modelo de memorial faz mais sentido aplicado ao entregável “Memorial descritivo”.

## O que deve ser feito

Usar a estrutura existente de KnowledgeRelation com:

```txt
targetType = deliverable
```

Criar fluxos:

* vincular knowledge ao entregável;
* remover vínculo;
* listar knowledge aplicado ao entregável;
* abrir detalhe do knowledge;
* aplicar por ações guiadas.

## Endpoints sugeridos

```txt
GET /projects/:projectId/deliverables/:deliverableId/knowledge
POST /projects/:projectId/deliverables/:deliverableId/knowledge
DELETE /projects/:projectId/deliverables/:deliverableId/knowledge/:relationId
```

Internamente, reaproveitar KnowledgeRelation.

## Regras

* KnowledgeItem e entregável devem pertencer à mesma organização.
* Entregável deve pertencer ao projeto informado.
* Não vincular archived.
* Deprecated exige alerta.
* Evitar duplicidade.

## Critérios de aceite

* Usuário vincula knowledge a entregável.
* Usuário remove vínculo.
* Entregável exibe knowledge aplicado.
* Projeto continua exibindo visão agregada.
* Backend protege organizationId.
* UI não expõe relationType cru.

## QA — Cenários mínimos

* Vincular checklist a orçamento.
* Vincular documento modelo a memorial.
* Remover vínculo.
* Tentar vincular item archived.
* Tentar vincular item de outro tenant.
* Ver vínculo no entregável.
* Ver vínculo agregado no projeto.

---

# Task 9 — Criar recomendações simples por tags

## Objetivo

Sugerir KnowledgeItems relevantes para um projeto com base em tags governadas.

## Contexto

Antes de IA, a plataforma pode gerar valor com recomendação simples usando taxonomia.

## O que deve ser feito

Criar use case:
ṕ
```txt
RecommendKnowledgeForProjectUseCase
```

Entrada:

* organizationId;
* projectId;
* filtros opcionais.

Critérios de recomendação:

* tags do projeto;
* tags dos entregáveis;
* tipos dos entregáveis;
* knowledge published;
* ignorar archived;
* sinalizar deprecated;
* calcular score simples por interseção de tags.

## Score simples

Exemplo:

* +3 para tag igual no projeto;
* +2 para tag igual em entregável;
* +2 se tipo do knowledge combina com entregável;
* -5 se deprecated;
* excluir archived.

## Output esperado

Cada recomendação deve retornar:

* knowledgeItem;
* score;
* matchedTags;
* reason;
* recommendedFor;
* alreadyApplied.

Exemplo de reason:

```txt
Recomendado porque este projeto possui as tags UBS e orçamento.
```

## Endpoint

```txt
GET /projects/:projectId/knowledge-recommendations
```

## Critérios de aceite

* Endpoint retorna recomendações.
* Recomendações usam tags governadas.
* Archived não aparece.
* Deprecated aparece com alerta ou score reduzido.
* Item já aplicado é sinalizado.
* UI mostra motivo da recomendação.
* Usuário pode aplicar recomendação.

## QA — Cenários mínimos

* Projeto com tag UBS recomenda knowledge de UBS.
* Projeto sem tags não recomenda ou mostra empty state.
* Knowledge archived não aparece.
* Knowledge deprecated aparece com alerta.
* Item já aplicado aparece como aplicado ou não aparece.
* Score ordena resultados.

---

# Task 10 — Criar seção “Sugestões da Base Técnica” no projeto

## Objetivo

Exibir recomendações de KnowledgeItems diretamente no cockpit do projeto.

## Contexto

O usuário não deve precisar entrar na Base de Conhecimento para descobrir padrões úteis.

## O que deve ser feito

Criar seção no cockpit:

```txt
Sugestões da Base Técnica
```

Cada recomendação deve exibir:

* título;
* tipo;
* status;
* tags;
* motivo;
* score visual simples, se fizer sentido;
* ação “Aplicar ao projeto”;
* ação “Abrir detalhe”.

## UX

A seção deve explicar:

```txt
Sugestões baseadas nas tags e no contexto técnico deste projeto.
```

Não vender como IA.

Usar linguagem transparente.

## Estados

* loading;
* erro;
* sem recomendações;
* recomendações disponíveis;
* todos já aplicados.

## Critérios de aceite

* Cockpit mostra recomendações.
* Motivo da recomendação é claro.
* Usuário aplica recomendação.
* Usuário abre detalhe.
* Sugestões não poluem a tela.
* Recomendações desaparecem ou mudam estado após aplicação.

## QA — Cenários mínimos

* Ver recomendações.
* Aplicar uma recomendação.
* Confirmar que vira knowledge aplicado.
* Abrir detalhe.
* Empty state sem recomendações.
* Deprecated sinalizado.

---

# Task 11 — Criar seção “Riscos e aprendizados aplicáveis”

## Objetivo

Destacar riscos técnicos e lições aprendidas relacionadas ao projeto.

## Contexto

Lições aprendidas são mais valiosas quando aparecem antes do erro se repetir.

## O que deve ser feito

Criar seção no cockpit:

```txt
Riscos e aprendizados aplicáveis
```

Fonte de dados:

* KnowledgeItems do tipo lesson_learned;
* revisões reprovadas do próprio projeto;
* knowledge recomendado por tags;
* knowledge deprecated aplicado;
* entregáveis sem checklist, se simples.

## Cada item deve exibir

* risco/problema;
* origem;
* recomendação;
* tags;
* ação para aplicar conhecimento;
* ação para abrir detalhe.

## Exemplos

```txt
Risco: Divergência de quantitativos em orçamento de UBS
Origem: revisão reprovada em projeto anterior
Recomendação: comparar quantitativos com memorial e pranchas antes do envio.
```

## Critérios de aceite

* Seção aparece no projeto.
* Lições aprendidas relevantes aparecem.
* Riscos têm explicação.
* Usuário consegue abrir/applicar knowledge.
* Revisões reprovadas do projeto aparecem como atenção.
* Empty state é claro.

## QA — Cenários mínimos

* Projeto UBS mostra lição de orçamento.
* Projeto sem riscos mostra empty state.
* Revisão reprovada aparece.
* Lição aplicada sai das sugestões ou muda estado.
* Deprecated aplicado gera alerta.

---

# Task 12 — Melhorar fluxos guiados de vínculo com Knowledge

## Objetivo

Substituir a escolha técnica de relationType por ações orientadas ao usuário.

## Contexto

A UI atual ainda expõe conceitos técnicos demais, como “tipo de relação”.

O usuário deve escolher uma intenção, não um enum.

## O que deve ser feito

Criar fluxo guiado para aplicar knowledge.

Ações de UI:

* Usar como referência;
* Aplicar padrão;
* Aplicar checklist;
* Usar documento modelo;
* Considerar lição aprendida;
* Aplicar ao entregável;
* Aplicar ao projeto.

Mapeamento interno:

* Usar como referência → reference_for;
* Aplicar padrão → standard_for;
* Aplicar checklist → checklist_for;
* Usar documento modelo → model_for;
* Considerar lição aprendida → lesson_from ou reference_for, conforme contexto;
* Criado com base em → based_on.

## Onde aplicar

* seção de Knowledge aplicado no projeto;
* seção de recomendações;
* detalhe do KnowledgeItem;
* entregável técnico.

## Critérios de aceite

* Usuário não vê relationType cru.
* Fluxos usam linguagem de negócio.
* Backend continua recebendo relationType correto.
* Ações respeitam tipo de KnowledgeItem.
* UI fica mais intuitiva.

## QA — Cenários mínimos

* Aplicar checklist.
* Aplicar padrão.
* Usar referência.
* Usar documento modelo.
* Aplicar lição aprendida.
* Confirmar relationType salvo corretamente.
* Validar que usuário não escolhe opção incompatível.

---

# Task 13 — Ajustar visual do Conhecimento Aplicado no cockpit

## Objetivo

Transformar a seção de conhecimento aplicado em uma visualização organizada por finalidade.

## Contexto

A seção atual funciona, mas ainda parece uma lista simples.

## O que deve ser feito

Agrupar conhecimento aplicado por tipo/finalidade:

* Padrões aplicados;
* Checklists aplicados;
* Lições aprendidas observadas;
* Referências usadas;
* Documentos modelo usados;
* Padrões de entrega.

Cada grupo deve exibir:

* contador;
* itens;
* status;
* tags;
* origem;
* ação de abrir;
* ação de remover vínculo, se permitido.

## Critérios de aceite

* Conhecimento aplicado não aparece mais como lista plana.
* Usuário entende finalidade de cada item.
* Deprecated sinalizado.
* Archived não deve estar aplicado ou deve mostrar alerta.
* Remoção continua funcionando.
* Abertura de detalhe funciona.

## QA — Cenários mínimos

* Ver padrões aplicados.
* Ver checklists aplicados.
* Ver lições aprendidas.
* Remover vínculo.
* Abrir detalhe.
* Ver empty state por grupo ou geral.

---

# Task 14 — Criar resumo operacional do cockpit

## Objetivo

Criar um bloco de resumo que diga ao usuário o que precisa de atenção no projeto.

## Contexto

O usuário precisa entender rapidamente o estado do projeto.

## O que deve ser feito

Criar componente:

```txt
ProjectOperationalSummary
```

Exibir mensagens como:

* “Este projeto possui 1 revisão reprovada.”
* “2 entregáveis estão próximos do prazo.”
* “Nenhum checklist foi aplicado ao orçamento.”
* “Há 3 conhecimentos recomendados para este projeto.”
* “Existe 1 documento sem versão oficial.”

## Backend

Pode consumir dados do cockpit endpoint.

## Critérios de aceite

* Resumo aparece no topo ou próximo ao topo.
* Mensagens são úteis e não genéricas.
* Empty state positivo quando tudo está ok.
* Mensagens levam a seções relevantes.

## QA — Cenários mínimos

* Projeto com revisão reprovada.
* Projeto sem knowledge aplicado.
* Projeto com documento sem oficial.
* Projeto com recomendações.
* Projeto sem pendências.

---

# Task 15 — Atualizar seeds e demo flow do Épico 2

## Objetivo

Criar dados de demonstração para validar cockpit, taxonomia e recomendações.

## O que deve ser feito

Atualizar seeds para incluir:

* tags governadas;
* projetos com tags;
* entregáveis com tags;
* knowledge com tags governadas;
* relações em projeto;
* relações em entregável;
* recomendações possíveis;
* riscos aplicáveis.

## Demo esperada

Fluxo de 5 minutos:

1. Abrir projeto “Construção da UBS Vila Esperança”.
2. Ver resumo operacional.
3. Ver entregável “Orçamento”.
4. Ver revisão reprovada.
5. Ver lição aprendida recomendada.
6. Aplicar checklist.
7. Ver conhecimento aplicado.
8. Abrir Base Técnica sugerida.
9. Explicar ciclo de valor.

## Critérios de aceite

* Seeds idempotentes.
* Tags criadas corretamente.
* Projeto possui recomendações.
* Entregável possui knowledge aplicado.
* Demo é compreensível.
* Documentação da demo atualizada.

## QA — Cenários mínimos

* Rodar seed duas vezes.
* Ver tags na organização.
* Ver recomendações no projeto.
* Ver knowledge aplicado.
* Ver riscos.
* Executar demo completa.

---

# Task 16 — Revisar permissões do cockpit e taxonomia

## Objetivo

Garantir que ações novas respeitem papéis e responsabilidades.

## Permissões novas sugeridas

```txt
technical_tags.view
technical_tags.create
technical_tags.edit
technical_tags.archive
technical_tags.deprecate
project_cockpit.view
project_knowledge.recommend
project_knowledge.apply
project_knowledge.remove
deliverable_knowledge.apply
deliverable_knowledge.remove
```

## Regras sugeridas

Owner/Admin:

* tudo.

Coordinator:

* gerencia tags;
* aplica/remove knowledge;
* vê recomendações;
* gerencia cockpit.

Engineer:

* vê cockpit;
* aplica knowledge;
* cria sugestão de tag, se permitido;
* não arquiva/deprecia tags.

Viewer:

* apenas visualiza.

## Critérios de aceite

* Backend protege ações.
* UI esconde/desabilita ações.
* Viewer não aplica knowledge.
* Engineer não gerencia taxonomia crítica.
* Coordinator gerencia tags.
* Tenant continua isolado.

## QA — Cenários mínimos

* Viewer acessa cockpit sem ações.
* Engineer aplica knowledge.
* Engineer não arquiva tag.
* Coordinator cria tag.
* Admin remove vínculo.
* Usuário de outro tenant não acessa.

---

# Task 17 — Documentar Épico 2 e criar cenários de teste

## Objetivo

Documentar o funcionamento real do Épico 2 e criar cenários de teste para validação.

## O que deve ser feito

Criar/atualizar:

```txt
docs/epics/02-epic-cockpit-tecnico.md
docs/epics/02-epic-cockpit-tecnico-backlog.md
docs/modules/technical-taxonomy.md
docs/modules/project-cockpit.md
docs/modules/project-cockpit-test-scenarios.md
docs/demo/project-cockpit-demo-flow.md
```

## Conteúdo esperado

* visão geral;
* entidades;
* endpoints;
* regras;
* permissões;
* fluxos;
* decisões técnicas;
* limitações;
* próximos passos;
* cenários de teste por task.

## Critérios de aceite

* Documentação reflete implementação.
* Cenários cobrem todas as tasks.
* Próxima sessão do Codex entende o épico.
* QA consegue testar sem depender de memória.
* Produto consegue apresentar demo.

## QA — Cenários mínimos

* Conferir docs criadas.
* Conferir endpoints documentados.
* Conferir permissões.
* Conferir demo flow.
* Conferir checklist por task.

---

# 6. Checklist final de aceite do épico

O Épico 2 será considerado concluído quando:

* Tags livres forem substituídas por taxonomia governada nos fluxos principais.
* Taxonomia técnica existir por tenant.
* Admin/coordinator conseguirem gerenciar tags.
* KnowledgeItems usarem tags governadas.
* Projeto possuir cockpit técnico organizado.
* Entregáveis forem exibidos como eixo operacional.
* Knowledge puder ser aplicado ao projeto e entregável.
* Recomendações simples por tags funcionarem.
* Riscos e lições aprendidas aparecerem no contexto.
* Fluxos de vínculo forem guiados e não técnicos.
* Seeds demonstrarem o ciclo completo.
* Permissões protegerem ações novas.
* Documentação e cenários de teste estiverem atualizados.

---

# 7. Fora do escopo

Este épico não deve implementar ainda:

* IA generativa;
* embeddings;
* busca semântica;
* recomendação por LLM;
* workflow formal de aprovação;
* versionamento avançado de knowledge;
* relatórios PDF;
* scraping de prefeitura;
* integrações externas;
* cronograma avançado;
* Gantt;
* notificações complexas.

---

# 8. Próximo épico sugerido após este

Após este épico, a plataforma estará pronta para um próximo passo mais inteligente:

## Épico 3 — Recomendações Semânticas e Inteligência Técnica

Possíveis frentes:

* embeddings por tenant;
* busca semântica;
* recomendação por similaridade;
* detecção automática de riscos;
* sugestão de checklists;
* copiloto técnico por projeto;
* resumo inteligente do projeto;
* análise de documentos.

Mas isso só deve vir depois que o contexto estiver bem estruturado.

Antes da IA, vem a taxonomia.

Antes da automação, vem o fluxo.

Antes da inteligência, vem o dado confiável.
