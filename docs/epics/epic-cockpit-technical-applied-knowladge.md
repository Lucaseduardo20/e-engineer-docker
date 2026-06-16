# Épico 2 — Cockpit Técnico do Projeto e Conhecimento Aplicado

## 1. Visão geral

O Épico 2 tem como objetivo transformar o detalhe do projeto no principal cockpit operacional da plataforma.

Após a implementação do módulo de Base de Conhecimento, a plataforma passou a conseguir registrar, publicar, relacionar e reutilizar itens como padrões técnicos, documentos modelo, projetos de referência, lições aprendidas, checklists de revisão e padrões de entrega.

Agora, o próximo passo estratégico não é simplesmente adicionar mais funcionalidades isoladas à Base de Conhecimento. O próximo passo é levar esse conhecimento para o local onde o usuário realmente trabalha: o projeto.

A tese central da plataforma continua sendo:

> Projetos geram conhecimento. Conhecimento melhora novos projetos.

O Épico 2 existe para fazer essa tese aparecer de forma prática no dia a dia do usuário.

O projeto deve deixar de ser apenas uma tela com dados, entregáveis e documentos. Ele deve se tornar uma central técnica que ajuda o usuário a entender:

* o que precisa ser produzido;
* o que está atrasado;
* o que está bloqueado;
* quais documentos precisam de atenção;
* quais revisões exigem ação;
* quais conhecimentos da organização se aplicam àquele contexto;
* quais riscos já foram aprendidos em projetos anteriores;
* quais padrões devem ser seguidos;
* quais checklists podem evitar retrabalho;
* quais referências podem acelerar a produção.

O objetivo deste épico é fazer com que a plataforma pareça menos uma gerenciadora de projetos genérica e mais uma ferramenta de inteligência operacional técnica para empresas de engenharia.

---

## 2. Problema que este épico resolve

### 2.1 O problema principal

Empresas de engenharia normalmente sofrem com um problema recorrente: o conhecimento operacional fica espalhado.

Ele fica em:

* pastas no Drive;
* arquivos duplicados;
* versões locais;
* conversas de WhatsApp;
* memória dos coordenadores;
* documentos antigos;
* revisões reprovadas;
* comentários soltos;
* planilhas;
* padrões informais;
* experiências passadas que ninguém documenta direito.

Quando um novo projeto começa, a equipe muitas vezes não sabe rapidamente:

* se já existiu projeto parecido;
* qual documento pode servir de modelo;
* quais erros já aconteceram antes;
* quais checklists devem ser aplicados;
* quais padrões técnicos a empresa segue;
* quais entregáveis são esperados para aquele tipo de projeto;
* quais riscos precisam ser observados.

Isso faz com que a empresa dependa demais da memória das pessoas e menos de um processo técnico estruturado.

O resultado é:

* retrabalho;
* atrasos;
* inconsistência nas entregas;
* perda de padrão;
* dificuldade de treinar novos colaboradores;
* dificuldade de escalar operação;
* risco de repetir erros já conhecidos;
* dificuldade de demonstrar maturidade técnica para clientes.

---

### 2.2 O problema específico após o Épico 1

O Épico 1 criou a Base de Conhecimento e seus principais fluxos.

Porém, após a implementação, ficou claro que a Base de Conhecimento ainda pode parecer um módulo separado, onde o usuário precisa entrar manualmente para consultar, criar, editar, vincular ou promover conhecimento.

Isso é poderoso, mas ainda exige esforço cognitivo.

O usuário final não acorda pensando:

> “Hoje vou alimentar a Base de Conhecimento.”

Ele pensa:

> “Tenho um projeto para entregar.”

Ou:

> “Preciso resolver essa revisão.”

Ou:

> “Tenho que fechar esse documento.”

Ou:

> “Preciso evitar que esse orçamento volte reprovado.”

Portanto, o valor da Base de Conhecimento precisa aparecer no fluxo natural do projeto.

O projeto precisa mostrar conhecimento aplicado, recomendações, riscos e padrões de forma contextual.

---

### 2.3 O problema das tags livres

Durante o uso inicial da Base de Conhecimento, foi identificado um ponto crítico: o sistema atual permite criar tags livres digitadas manualmente, separadas por vírgula.

Isso cria risco de bagunça semântica.

Exemplos de variação indesejada:

* `ubs`
* `UBS`
* `unidade-basica-saude`
* `unidade de saúde`
* `saude`
* `saúde`
* `orcamento`
* `orçamento`
* `quantitativo`
* `quantitativos`
* `prefeitura`
* `prefeitura-sp`
* `sp`
* `são-paulo`

Se cada usuário puder criar qualquer tag sem regra, a plataforma perde eficiência com o tempo.

A Base de Conhecimento depende de tags para:

* busca;
* filtros;
* recomendações simples;
* relação entre projetos e conhecimentos;
* identificação de contexto;
* classificação de dores recorrentes;
* reaproveitamento técnico;
* inteligência futura.

Portanto, tags não podem ser tratadas como simples texto solto. Elas precisam evoluir para uma taxonomia técnica controlada por tenant.

Esse ponto passa a ser uma fundação importante do Épico 2.

---

## 3. Objetivo do épico

Transformar o detalhe do projeto em um cockpit técnico inteligente, conectando entregáveis, documentos, revisões, riscos, padrões e conhecimento aplicado, para que o usuário consiga executar projetos com mais clareza, menos retrabalho e maior reaproveitamento do conhecimento acumulado pela organização.

Em termos práticos, este épico deve permitir que o usuário abra um projeto e consiga responder rapidamente:

* Qual é a situação geral deste projeto?
* Quais entregáveis exigem atenção?
* Quais documentos estão oficiais, em rascunho ou pendentes?
* Quais revisões foram reprovadas ou ainda precisam de decisão?
* Quais conhecimentos da empresa já estão aplicados neste projeto?
* Quais conhecimentos são recomendados para este projeto?
* Quais riscos já foram aprendidos em projetos anteriores?
* Quais checklists devem ser usados antes de enviar algo?
* Quais modelos e referências podem acelerar a produção?
* O que precisa ser feito agora?

---

## 4. Princípio central de produto

O projeto deve ser o centro operacional.

A Base de Conhecimento deve ser o motor de inteligência.

As tags/taxonomias devem ser o vocabulário técnico que conecta tudo.

A experiência ideal é:

> O usuário não precisa procurar conhecimento do zero. A plataforma deve trazer o conhecimento certo para perto do projeto certo, no momento certo.

---

## 5. Usuário principal deste épico

O usuário principal deste épico é o profissional técnico ou coordenador de uma empresa de engenharia que precisa acompanhar projetos, entregáveis, documentos e revisões.

Exemplos de usuários:

* engenheiro civil;
* arquiteto;
* coordenador técnico;
* analista de projetos;
* responsável por documentação técnica;
* gestor de projetos;
* dono de pequena empresa de engenharia.

---

## 6. Como pensar no usuário

O usuário não quer navegar por uma plataforma complexa.

Ele quer resolver a operação.

Ele quer saber:

* o que está pendente;
* o que precisa revisar;
* qual documento usar;
* qual padrão seguir;
* onde está o erro;
* o que pode atrasar;
* como evitar retrabalho;
* como entregar com segurança.

O usuário não quer pensar em conceitos internos como:

* `relationType`;
* `targetType`;
* `based_on`;
* `lesson_from`;
* `standard_for`;
* `checklist_for`;
* `metadata`;
* `content.sections`;
* `tag normalization`.

Esses conceitos podem existir no domínio e no backend, mas a interface precisa traduzir tudo isso em linguagem natural.

Em vez de perguntar ao usuário:

> Qual tipo de relação você quer criar?

A interface deveria oferecer ações como:

* Aplicar checklist neste entregável;
* Usar como referência;
* Aplicar padrão técnico;
* Vincular lição aprendida;
* Usar documento modelo;
* Ver conhecimentos recomendados;
* Registrar aprendizado a partir desta revisão.

---

## 7. Solução proposta

O Épico 2 será dividido em três grandes frentes:

1. Cockpit Técnico do Projeto;
2. Conhecimento aplicado e recomendado;
3. Taxonomia técnica governada do tenant.

---

# Parte 1 — Cockpit Técnico do Projeto

## 8. O que é o Cockpit Técnico do Projeto

O Cockpit Técnico do Projeto é a evolução da tela de detalhe do projeto.

Ele deve reunir, em uma única experiência clara:

* resumo operacional;
* entregáveis;
* documentos;
* revisões;
* conhecimento aplicado;
* riscos;
* recomendações;
* histórico técnico;
* próximas ações.

O objetivo não é criar uma tela carregada de informação.

O objetivo é organizar a operação técnica para que o usuário saiba o que fazer.

---

## 9. Estrutura ideal do detalhe do projeto

A tela do projeto deve ser reorganizada em blocos claros.

### 9.1 Header executivo do projeto

O topo do projeto deve exibir:

* nome do projeto;
* cliente/contratante;
* status;
* progresso;
* responsável principal;
* prazo, se existir;
* ações principais.

Também deve exibir indicadores rápidos:

* total de entregáveis;
* entregáveis atrasados;
* documentos oficiais;
* revisões pendentes;
* revisões reprovadas;
* conhecimentos aplicados;
* riscos detectados.

Exemplo de leitura esperada:

> Este projeto possui 6 entregáveis, 2 documentos oficiais, 1 revisão reprovada e 5 conhecimentos aplicados.

---

### 9.2 Resumo operacional

Criar uma seção de resumo que ajude o usuário a entender a situação do projeto.

Exemplo:

* 3 entregáveis em produção;
* 1 entregável bloqueado;
* 2 documentos aguardando revisão;
* 1 revisão reprovada;
* 5 conhecimentos aplicados;
* 2 recomendações disponíveis.

Essa seção deve ser visual, simples e rápida.

---

### 9.3 Entregáveis como eixo principal

Entregáveis devem ser o centro da operação técnica.

Cada entregável deve mostrar:

* nome;
* tipo;
* status;
* responsável;
* prazo;
* progresso;
* documentos vinculados;
* revisões vinculadas;
* knowledge aplicado;
* pendências;
* alertas.

Exemplo:

```txt
Orçamento
Status: Em produção
Responsável: Leonardo
Prazo: 22/06/2026
Documentos: 1
Revisões: 1 reprovada
Conhecimentos aplicados:
- Checklist de revisão de orçamento
- Divergência de quantitativos em orçamento de UBS
```

Isso aproxima a plataforma da realidade da engenharia.

---

### 9.4 Documentos no contexto do projeto

A seção de documentos deve deixar claro:

* quais documentos existem;
* quais estão oficiais;
* quais estão em minuta;
* quais precisam de nova versão;
* quais foram usados como modelo;
* quais poderiam virar modelo;
* quais estão vinculados a knowledge.

A ação “Salvar como modelo” deve continuar existindo, mas integrada ao contexto do documento.

---

### 9.5 Revisões no contexto do projeto

A seção de revisões deve mostrar:

* revisões pendentes;
* revisões aprovadas;
* revisões reprovadas;
* revisões atrasadas;
* revisões que geraram lições aprendidas;
* revisões que ainda poderiam gerar aprendizado.

A ação “Registrar lição aprendida” deve aparecer de forma contextual.

Exemplo:

> Esta revisão foi reprovada. Registre uma lição aprendida para evitar que esse problema se repita.

---

### 9.6 Conhecimento aplicado

A seção de conhecimento aplicado deve deixar de parecer uma lista técnica simples.

Ela deve ser organizada por finalidade.

Exemplo:

#### Padrões aplicados

* Organização de disciplinas em projetos de UBS

#### Checklists aplicados

* Revisão de orçamento antes de envio ao cliente

#### Lições aprendidas observadas

* Divergência de quantitativos em orçamento de UBS

#### Referências usadas

* Construção da UBS Vila Esperança

#### Documentos modelo usados

* Memorial descritivo para reforma escolar

Essa organização é muito mais útil do que uma lista plana.

---

### 9.7 Riscos e aprendizados aplicáveis

Criar uma seção de riscos e aprendizados aplicáveis.

Essa seção deve mostrar conhecimentos que ainda não estão vinculados ao projeto, mas parecem relevantes.

Inicialmente, isso pode ser feito por regras simples, usando tags e tipo do projeto.

Exemplo:

Projeto possui tags:

* `ubs`;
* `orçamento`;
* `prefeitura-sp`.

Knowledge publicado possui tags:

* `ubs`;
* `orçamento`;
* `quantitativos`;
* `retrabalho`.

A plataforma sugere:

> Lição aprendida aplicável: Divergência de quantitativos em orçamento de UBS.

Sem IA ainda.

Apenas recomendação simples por taxonomia.

Mesmo assim, isso já comunica inteligência.

---

# Parte 2 — Conhecimento aplicado e recomendado

## 10. Conhecimento aplicado vs conhecimento recomendado

É importante diferenciar dois conceitos.

### Conhecimento aplicado

É conhecimento que alguém vinculou explicitamente ao projeto.

Exemplo:

* este projeto usa este checklist;
* este projeto segue este padrão;
* este projeto foi baseado nesta referência.

### Conhecimento recomendado

É conhecimento que a plataforma sugere com base em contexto.

Exemplo:

* este projeto parece uma UBS;
* existe uma lição aprendida sobre orçamento de UBS;
* talvez esse conhecimento seja útil.

O aplicado é decisão humana.

O recomendado é sugestão da plataforma.

---

## 11. Recomendação simples sem IA

Antes de usar IA ou embeddings, a plataforma pode gerar valor com recomendação baseada em regras.

Critérios iniciais:

* tags do projeto;
* tags dos entregáveis;
* tipo do projeto;
* tipo dos entregáveis;
* status dos documentos;
* revisões reprovadas;
* tipo dos KnowledgeItems;
* tags dos KnowledgeItems;
* status published;
* ignorar archived;
* sinalizar deprecated.

Exemplo de lógica:

```txt
Se projeto possui tag "ubs"
e entregável possui nome/tipo "orçamento"
e existe lesson_learned published com tags ["ubs", "orçamento"]
então sugerir esse KnowledgeItem no projeto.
```

Isso cria a primeira camada de inteligência operacional.

---

## 12. UX para recomendações

A recomendação deve ser explicável.

Não basta mostrar uma lista.

Cada recomendação deve explicar por que apareceu.

Exemplo:

> Recomendado porque este projeto possui tags "UBS" e "orçamento".

Ou:

> Recomendado porque existe uma lição aprendida relacionada a revisões reprovadas de orçamento em UBS.

Isso aumenta confiança.

---

## 13. Ações sobre recomendações

Cada item recomendado deve permitir:

* aplicar ao projeto;
* abrir detalhe;
* ignorar por enquanto;
* marcar como não relevante, se fizer sentido futuro.

Para MVP, ações mínimas:

* abrir detalhe;
* aplicar ao projeto.

---

# Parte 3 — Taxonomia técnica do tenant

## 14. Por que refatorar tags

As tags são o vocabulário operacional da inteligência da plataforma.

Se as tags forem livres demais, a plataforma perde capacidade de:

* buscar corretamente;
* recomendar conhecimento;
* identificar padrões;
* agrupar dores;
* comparar projetos;
* sugerir checklists;
* reaproveitar documentos;
* detectar riscos.

Portanto, tags precisam evoluir de simples strings soltas para uma taxonomia governada por tenant.

---

## 15. Problema atual das tags

Hoje, a criação de KnowledgeItem permite digitar tags separadas por vírgula.

Isso causa problemas como:

* duplicidade;
* variações de escrita;
* acentos inconsistentes;
* plural/singular;
* tags inúteis;
* tags muito genéricas;
* tags muito específicas;
* tags sem relação com o domínio;
* baixa confiabilidade para recomendação.

Exemplos ruins:

```txt
teste
abc
coisa
novo
importante
sp
obra
projeto
documento
qualquer coisa
```

Essas tags não ajudam a inteligência do produto.

---

## 16. Nova visão de tags

Tags devem ser tratadas como entidades do tenant.

Uma tag deve ter:

* id;
* organizationId;
* name;
* slug;
* category;
* description;
* status;
* createdBy;
* createdAt;
* updatedAt;
* usageCount, se possível.

Exemplo:

```txt
Nome: UBS
Slug: ubs
Categoria: Tipo de projeto
Descrição: Projetos relacionados a Unidade Básica de Saúde.
Status: Ativa
```

---

## 17. Categorias de tags

As tags devem ser categorizadas.

Categorias iniciais sugeridas:

### Tipo de projeto

Exemplos:

* UBS;
* reforma escolar;
* praça pública;
* pavimentação;
* drenagem;
* unidade de saúde;
* obra pública.

### Disciplina técnica

Exemplos:

* arquitetura;
* estrutura;
* hidráulica;
* elétrica;
* orçamento;
* cronograma;
* memorial;
* acessibilidade.

### Tipo de documento

Exemplos:

* memorial descritivo;
* relatório fotográfico;
* orçamento;
* cronograma físico-financeiro;
* ART/RRT;
* prancha;
* planilha.

### Dor operacional

Exemplos:

* retrabalho;
* revisão reprovada;
* quantitativos divergentes;
* nomenclatura incorreta;
* falta de compatibilização;
* versão errada;
* documento incompleto.

### Contexto de cliente/órgão

Exemplos:

* prefeitura-sp;
* órgão público;
* licitação;
* contrato público;
* zeladoria urbana.

### Etapa do projeto

Exemplos:

* levantamento;
* projeto básico;
* projeto executivo;
* revisão;
* entrega final;
* pós-entrega.

### Finalidade do conhecimento

Exemplos:

* padrão;
* modelo;
* checklist;
* referência;
* lição aprendida;
* entrega.

---

## 18. Tags livres vs tags aprovadas

A plataforma pode adotar um modelo progressivo.

### Fase 1 — Tags controladas com criação rápida

O usuário pode criar uma nova tag, mas ela passa a ser uma entidade real.

O sistema normaliza:

* caixa baixa;
* slug;
* remoção de espaços extras;
* remoção de duplicidade;
* tratamento de acento, se fizer sentido;
* categoria obrigatória ou sugerida.

### Fase 2 — Tags sugeridas

Ao criar conhecimento ou projeto, o sistema sugere tags existentes.

O usuário escolhe tags em um autocomplete, em vez de digitar qualquer texto.

### Fase 3 — Tags pendentes de revisão

Se o usuário criar uma nova tag, ela pode entrar como:

```txt
pending_review
```

Um admin/coordinator pode aprovar, editar ou mesclar.

### Fase 4 — Governança completa

Tags podem ter:

* sinônimos;
* merge;
* desativação;
* uso por categoria;
* métricas;
* recomendação inteligente.

Para o MVP do Épico 2, a Fase 1 e parte da Fase 2 já são suficientes.

---

## 19. Status de uma tag

Status sugeridos:

```txt
active
pending_review
deprecated
archived
```

### active

Tag válida para uso.

### pending_review

Tag criada por usuário, aguardando revisão.

### deprecated

Tag antiga, ainda visível em histórico, mas não recomendada para novos vínculos.

### archived

Tag arquivada, não aparece para seleção.

---

## 20. Regras para tags

Regras mínimas:

1. Tags pertencem a uma organização.
2. Tags devem ter nome único por organização, considerando slug.
3. Tags devem ter categoria.
4. Tags não devem ser criadas como texto solto dentro do KnowledgeItem.
5. KnowledgeItem deve referenciar tags existentes.
6. Tags archived não devem aparecer para seleção.
7. Tags deprecated devem aparecer com alerta, se ainda forem usadas.
8. O sistema deve evitar duplicatas como `ubs`, `UBS`, `U.B.S`.
9. Tags precisam ser reutilizáveis entre projetos, documentos, revisões e knowledge.
10. Tags são base para recomendação simples.

---

## 21. UX de tags

O usuário não deve sentir que está preenchendo uma burocracia.

O ideal é um campo de autocomplete.

Ao digitar:

```txt
orça...
```

A plataforma sugere:

* Orçamento;
* Revisão de orçamento;
* Quantitativos divergentes.

Se a tag não existir, pode aparecer:

> Criar nova tag “orçamento executivo”

Mas com categoria.

Exemplo de criação rápida:

```txt
Nome: Orçamento executivo
Categoria: Disciplina técnica
Descrição opcional
```

---

## 22. Governança simples de tags

Criar uma tela ou seção em Organização chamada:

```txt
Taxonomia técnica
```

Ou:

```txt
Tags do tenant
```

Essa tela deve permitir:

* listar tags;
* filtrar por categoria;
* criar tag;
* editar tag;
* arquivar tag;
* marcar como deprecated;
* ver uso da tag;
* futuramente mesclar tags.

Para o Épico 2, a primeira versão pode ser simples.

---

## 23. Como as tags melhoram o cockpit

Com tags governadas, o cockpit do projeto consegue fazer sugestões melhores.

Exemplo:

Projeto:

* Tipo de projeto: UBS;
* Disciplina ativa: orçamento;
* Cliente: prefeitura-sp.

Knowledge:

* Lição aprendida: Divergência de quantitativos em orçamento de UBS;
* Tags: UBS, orçamento, quantitativos divergentes, revisão reprovada.

A plataforma recomenda essa lição.

Sem tags responsáveis, essa recomendação ficaria fraca.

---

# 24. Escopo proposto do Épico 2

## Task 1 — Documentar e redesenhar o fluxo do Cockpit Técnico do Projeto

Objetivo:

Definir a nova estrutura do detalhe do projeto, priorizando clareza operacional e conhecimento aplicado.

Entregáveis:

* nova organização da tela;
* seções principais;
* comportamento esperado;
* microcopy;
* estados vazios;
* ações principais.

---

## Task 2 — Refatorar tags para Taxonomia Técnica do Tenant

Objetivo:

Transformar tags de strings livres em entidades governadas por organização.

Entregáveis:

* entidade Tag/TechnicalTag;
* categorias de tag;
* status de tag;
* migration;
* repository;
* use cases;
* seed inicial;
* normalização;
* proteção multi-tenant.

Essa task deve ser priorizada cedo, porque as recomendações simples dependem disso.

---

## Task 3 — Criar autocomplete de tags no frontend

Objetivo:

Substituir campos de texto livre por seleção assistida de tags.

Aplicar em:

* KnowledgeItem;
* Project;
* Deliverable, se já tiver tags;
* Document, se fizer sentido;
* Review, se fizer sentido.

Entregáveis:

* componente reutilizável de tag selector;
* busca de tags por tenant;
* criação rápida controlada;
* categorias visíveis;
* bloqueio de duplicidade.

---

## Task 4 — Criar gestão mínima de Taxonomia na Organização

Objetivo:

Permitir que admin/coordinator gerenciem tags do tenant.

Entregáveis:

* tela de tags;
* criação;
* edição;
* arquivamento;
* depreciação;
* listagem por categoria;
* contador de uso, se viável.

---

## Task 5 — Reorganizar detalhe do projeto como cockpit

Objetivo:

Transformar o detalhe do projeto em uma visão operacional clara.

Entregáveis:

* header executivo;
* indicadores rápidos;
* resumo operacional;
* seções reorganizadas;
* knowledge aplicado agrupado por finalidade;
* estados vazios melhores.

---

## Task 6 — Criar visão rica de entregáveis no projeto

Objetivo:

Fazer o entregável técnico virar o eixo operacional.

Entregáveis:

* cards/seções de entregável;
* documentos vinculados;
* revisões vinculadas;
* knowledge aplicado ao entregável;
* pendências;
* alertas.

---

## Task 7 — Permitir aplicar KnowledgeItem diretamente em entregáveis

Objetivo:

Usar a relação `targetType = deliverable` de forma real.

Entregáveis:

* vincular knowledge a entregável;
* remover vínculo;
* exibir knowledge no entregável;
* ações guiadas por tipo.

---

## Task 8 — Criar recomendações simples por tags

Objetivo:

Sugerir conhecimentos publicados com base em tags do projeto e entregáveis.

Entregáveis:

* use case de recomendação;
* endpoint de recomendações;
* algoritmo simples por interseção de tags;
* score básico;
* explicação da recomendação;
* UI no cockpit.

---

## Task 9 — Criar seção de riscos e aprendizados aplicáveis

Objetivo:

Destacar lições aprendidas e riscos técnicos relacionados ao projeto.

Entregáveis:

* bloco visual de riscos;
* lições recomendadas;
* revisões reprovadas do projeto;
* alertas por deprecated knowledge;
* ação para aplicar conhecimento.

---

## Task 10 — Melhorar fluxos guiados de vínculo

Objetivo:

Esconder complexidade técnica de relationType da UI.

Entregáveis:

* substituir “tipo de relação” por ações orientadas;
* aplicar como padrão;
* usar como referência;
* aplicar checklist;
* usar documento modelo;
* registrar aprendizado;
* mapear ação para relationType internamente.

---

## Task 11 — Ajustar demo flow do Cockpit Técnico

Objetivo:

Atualizar seeds e roteiro para apresentar o novo valor do cockpit.

Entregáveis:

* projeto com recomendações;
* projeto com riscos;
* entregável com knowledge aplicado;
* tags governadas;
* fluxo demonstrável em 5 minutos;
* documentação de demo atualizada.

---

# 25. Fora do escopo deste épico

Este épico não deve implementar ainda:

* IA generativa;
* embeddings;
* busca semântica;
* recomendação por LLM;
* workflow formal de aprovação;
* versionamento avançado de KnowledgeItem;
* relatório PDF;
* scraping de dados da prefeitura;
* integração externa;
* gestão financeira;
* cronograma avançado;
* Gantt;
* chat interno;
* notificações complexas.

O foco é:

```txt
Projeto + Entregáveis + Knowledge aplicada + Taxonomia + Recomendação simples.
```

---

# 26. Critérios de sucesso do épico

O Épico 2 será considerado bem-sucedido quando:

1. A tela do projeto comunicar claramente a situação operacional.
2. Entregáveis forem o eixo principal do projeto.
3. Conhecimentos aplicados aparecerem de forma organizada.
4. Usuário conseguir aplicar conhecimento sem entender relationType.
5. Tags forem entidades governadas por tenant.
6. Usuário não conseguir criar tags inúteis livremente sem regra.
7. Recomendações simples por tags funcionarem.
8. O projeto sugerir conhecimentos relevantes.
9. Riscos e lições aprendidas aparecerem no contexto do projeto.
10. O fluxo for demonstrável para Leo/Rafael em poucos minutos.
11. A experiência parecer mais inteligente sem depender ainda de IA.
12. A plataforma reforçar a tese central:

    > Projetos geram conhecimento. Conhecimento melhora novos projetos.

---

# 27. Métricas qualitativas de validação

Durante demonstrações e testes, observar se o usuário consegue responder:

* Eu entendo rapidamente a situação do projeto?
* Eu vejo o que precisa de atenção?
* Eu encontro padrões aplicáveis sem procurar manualmente?
* Eu entendo por que um conhecimento foi recomendado?
* Eu consigo aplicar conhecimento com poucos cliques?
* Eu entendo quais tags classificam o contexto do projeto?
* Eu sinto que a plataforma evita retrabalho?
* Eu sinto que isso é diferente de um gerenciador de tarefas genérico?

---

# 28. Riscos do épico

## 28.1 Risco de complexidade visual

Ao colocar muita coisa no detalhe do projeto, a tela pode ficar poluída.

Mitigação:

* priorizar seções claras;
* usar progressive disclosure;
* esconder detalhes secundários;
* usar cards e agrupamentos;
* evitar tabelas grandes demais.

---

## 28.2 Risco de taxonomia burocrática

Se criar tags for difícil demais, o usuário pode sentir fricção.

Mitigação:

* autocomplete;
* criação rápida;
* categorias simples;
* sugestões;
* defaults por seed;
* não exigir descrição longa no início.

---

## 28.3 Risco de recomendação ruim

Se recomendação por tags for ingênua demais, pode sugerir itens irrelevantes.

Mitigação:

* mostrar explicação;
* permitir ignorar;
* priorizar published;
* excluir archived;
* alertar deprecated;
* usar score simples;
* começar com poucos tipos de recomendação.

---

## 28.4 Risco de parecer IA fake

A recomendação simples não deve ser vendida como IA.

Mitigação:

* comunicar como “sugestões com base em tags e contexto”;
* deixar IA/embeddings para roadmap futuro;
* ser transparente.

---

# 29. Decisão estratégica

A decisão estratégica deste épico é:

> Antes de colocar IA, precisamos organizar o contexto.

A inteligência da plataforma depende de dados bem estruturados.

Por isso, tags/taxonomia, entregáveis, relações e recomendações simples são mais importantes agora do que IA generativa.

Se o tenant alimenta a plataforma com tags ruins, a inteligência futura será ruim.

Se o projeto não mostra o conhecimento no momento certo, a Base de Conhecimento vira biblioteca passiva.

Portanto, o próximo passo é fazer o conhecimento trabalhar dentro do projeto.

---

# 30. Resumo executivo

O Épico 2 transforma a plataforma de uma base técnica com projetos em um cockpit operacional inteligente.

Ele resolve três dores principais:

1. O usuário não quer procurar conhecimento manualmente.
2. O projeto precisa mostrar o que é relevante agora.
3. Tags livres demais prejudicam a inteligência da plataforma.

A solução é:

* reorganizar o detalhe do projeto;
* tornar entregáveis o centro operacional;
* aplicar e recomendar knowledge no contexto do projeto;
* criar taxonomia técnica governada do tenant;
* melhorar fluxos para o usuário não lidar com complexidade interna.

Ao final deste épico, a plataforma deve começar a parecer o que ela se propõe a ser:

> Uma plataforma de inteligência operacional técnica para empresas de engenharia.
