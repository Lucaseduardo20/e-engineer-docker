# Épico 1 — Base de Conhecimento Operacional

## 1. Resumo executivo

A Base de Conhecimento Operacional é o primeiro grande passo para transformar a plataforma de uma gerenciadora técnica de projetos em uma plataforma de inteligência operacional para empresas de engenharia.

Hoje a plataforma já possui uma fundação importante: organizações, colaboradores, projetos, entregáveis, documentos, versões e revisões. Porém, sem a Base de Conhecimento funcionando de forma viva e integrada, o produto ainda corre o risco de parecer apenas um gerenciador de projetos técnico.

Este épico tem como objetivo criar o módulo que representa o cérebro técnico do tenant: o lugar onde a empresa registra, organiza, publica, consulta e reutiliza padrões técnicos, documentos modelo, projetos de referência, checklists, lições aprendidas e padrões de entrega.

A regra central da plataforma é:

> Projetos geram conhecimento. Conhecimento melhora novos projetos.

Este épico implementa a primeira metade desse ciclo: estruturar o conhecimento do tenant de forma organizada, pesquisável, confiável e reutilizável.

---

## 2. Problema que este épico resolve

Empresas de engenharia frequentemente trabalham com conhecimento espalhado em várias fontes informais:

- arquivos antigos no Drive;
- mensagens de WhatsApp;
- planilhas soltas;
- modelos em computadores pessoais;
- memória de coordenadores e engenheiros mais experientes;
- projetos antigos difíceis de encontrar;
- revisões passadas que ninguém transforma em aprendizado;
- documentos oficiais que poderiam virar modelo, mas ficam perdidos;
- padrões internos que existem na prática, mas não estão registrados.

O resultado disso é retrabalho.

Quando um novo projeto começa, a equipe muitas vezes precisa perguntar:

- Qual projeto parecido já fizemos?
- Qual modelo de memorial usamos?
- Qual checklist de revisão devemos seguir?
- Qual padrão de nomenclatura vale para esse tipo de entrega?
- Quem sabe onde está o documento certo?
- Qual erro já aconteceu nesse tipo de projeto?
- Qual versão antiga pode servir como referência?

Essa dependência de memória humana e organização informal cria risco técnico, perda de tempo e inconsistência entre projetos.

A Base de Conhecimento resolve isso criando um acervo técnico próprio de cada tenant, conectado ao fluxo de projetos, documentos, entregáveis e revisões.

---

## 3. Objetivo do épico

Criar a primeira versão operacional da Base de Conhecimento da plataforma.

Ao final deste épico, o usuário deve conseguir:

1. Acessar a área de Base de Conhecimento.
2. Visualizar itens de conhecimento do tenant.
3. Buscar e filtrar itens por tipo, status e texto.
4. Criar novos itens de conhecimento.
5. Editar itens existentes.
6. Publicar itens para uso oficial.
7. Arquivar itens obsoletos.
8. Consultar detalhes de um item.
9. Vincular itens a projetos, documentos ou outros contextos relevantes, quando aplicável.
10. Preparar a base para futuros fluxos de promoção de projeto, documento e revisão.

Este épico não precisa implementar toda a inteligência futura, mas deve criar uma fundação sólida para ela.

---

## 4. O que a Base de Conhecimento é

A Base de Conhecimento é o acervo técnico reutilizável de uma organização.

Ela não deve ser tratada como uma wiki genérica, uma pasta de arquivos ou um CRUD de textos. Ela é uma camada de inteligência operacional conectada ao domínio da engenharia.

Ela armazena conhecimento que ajuda a empresa a executar novos projetos com mais padrão, menos retrabalho e mais segurança técnica.

A Base de Conhecimento deve guardar:

- padrões técnicos;
- documentos modelo;
- projetos de referência;
- lições aprendidas;
- checklists de revisão;
- padrões de entrega;
- orientações internas;
- observações sobre clientes ou prefeituras;
- boas práticas;
- erros recorrentes;
- materiais que podem ser reaproveitados em novos projetos.

A Base de Conhecimento deve responder perguntas como:

- Como a empresa costuma fazer esse tipo de projeto?
- Que projeto antigo pode servir como referência?
- Que modelo de documento devemos usar?
- Que checklist evita erro antes da entrega?
- Que problema já aconteceu em projetos parecidos?
- Que padrão interno precisa ser seguido?
- Que conhecimento deve ser reaproveitado neste novo projeto?

---

## 5. O que a Base de Conhecimento não é

A Base de Conhecimento não deve ser:

- um Notion genérico;
- um Google Drive alternativo;
- uma wiki solta;
- um repositório de arquivos sem contexto;
- um mural de anotações;
- uma lista de tarefas;
- um clone de ferramenta de documentação;
- uma área sem relação com projetos, documentos e revisões.

O diferencial está na conexão com a operação técnica.

Um item de conhecimento deve ter contexto, tipo, status, tags, relações e finalidade de reutilização.

A plataforma não deve criar mais um lugar para a empresa guardar bagunça. Ela deve criar um lugar para transformar experiência técnica em ativo operacional.

---

## 6. Linguagem de domínio

Este módulo deve usar uma linguagem coerente com o negócio.

Termos principais:

- Base de Conhecimento;
- Item de Conhecimento;
- Padrão Técnico;
- Documento Modelo;
- Projeto de Referência;
- Lição Aprendida;
- Checklist de Revisão;
- Padrão de Entrega;
- Publicado;
- Rascunho;
- Arquivado;
- Obsoleto;
- Tags;
- Relações;
- Uso em Projeto;
- Reaproveitamento;
- Acervo Técnico;
- Conhecimento do Tenant.

Evitar termos excessivamente genéricos como:

- post;
- artigo;
- anotação;
- card;
- tarefa;
- item solto;
- documento qualquer.

O módulo deve reforçar que estamos falando de conhecimento técnico operacional.

---

## 7. Tipos iniciais de item de conhecimento

Para o MVP deste épico, a Base de Conhecimento deve suportar pelo menos os seguintes tipos.

### 7.1 Padrão Técnico

Representa uma regra, orientação ou padronização interna da empresa.

Exemplos:

- Padrão de nomenclatura de arquivos técnicos.
- Padrão de organização de entregáveis por disciplina.
- Padrão de revisão de projeto arquitetônico.
- Padrão para fechamento de orçamento.
- Padrão de apresentação de prancha.
- Padrão para envio de pacote técnico à prefeitura.

Pergunta que responde:

> Como a empresa faz isso de forma padronizada?

### 7.2 Documento Modelo

Representa um documento, arquivo ou estrutura que pode ser reutilizada como base em novos projetos.

Exemplos:

- Modelo de memorial descritivo.
- Modelo de cronograma físico-financeiro.
- Modelo de relatório fotográfico.
- Modelo de planilha orçamentária.
- Modelo de checklist de entrega.
- Modelo de relatório técnico.

Pergunta que responde:

> Qual documento base devo usar para começar?

### 7.3 Projeto de Referência

Representa um projeto antigo que foi considerado útil para consulta e reutilização em novos projetos.

Exemplos:

- Reforma da Escola Municipal Jardim Primavera.
- Construção da UBS Vila Esperança.
- Revitalização da Praça Central.
- Sistema de Drenagem do Bairro São Lucas.

Pergunta que responde:

> Que projeto parecido já fizemos e pode servir como referência?

### 7.4 Lição Aprendida

Representa um aprendizado gerado pela prática, normalmente a partir de erro, retrabalho, revisão, atraso ou decisão técnica importante.

Exemplos:

- Em reformas escolares, validar acessibilidade antes de fechar orçamento.
- Em projetos de UBS, compatibilizar hidráulica e arquitetura antes da revisão final.
- Em pavimentação, revisar drenagem antes da planilha orçamentária.
- Em relatórios fotográficos, sempre registrar antes e depois do mesmo ponto.

Pergunta que responde:

> O que já aprendemos e não queremos esquecer?

### 7.5 Checklist de Revisão

Representa uma lista de verificação usada antes de aprovar, enviar ou finalizar um entregável.

Exemplos:

- Checklist de revisão de orçamento.
- Checklist de compatibilização de projeto arquitetônico.
- Checklist de documentos para envio à prefeitura.
- Checklist de memorial descritivo.

Pergunta que responde:

> O que precisa ser conferido antes de aprovar ou entregar?

### 7.6 Padrão de Entrega

Representa a forma esperada de montagem e envio de um pacote técnico.

Exemplos:

- Padrão de entrega para prefeitura.
- Padrão de pacote técnico final.
- Padrão de envio para fiscalização.
- Padrão de organização de arquivos finais.

Pergunta que responde:

> Como a entrega deve ser montada para evitar inconsistência?

---

## 8. Status dos itens

Cada item deve ter um status claro. Isso é essencial para garantir confiança no acervo.

### 8.1 Rascunho

Item ainda em construção.

Pode estar incompleto, aguardando revisão interna ou sendo preparado por algum colaborador.

Deve ser visível para quem tem permissão de gestão, mas não deve ser tratado como conhecimento oficial.

### 8.2 Publicado

Item validado e disponível para uso oficial dentro do tenant.

Itens publicados podem ser recomendados, vinculados e utilizados em projetos.

### 8.3 Arquivado

Item removido do uso ativo, mas mantido para histórico.

Pode ter sido substituído por outro padrão, perdido relevância ou deixado de ser usado.

### 8.4 Obsoleto

Item que ainda pode ser consultado, mas não deve ser usado como referência atual.

Esse status é importante para padrões antigos, legislações superadas, modelos antigos ou documentos que foram substituídos.

---

## 9. Estrutura de um KnowledgeItem

A entidade principal do módulo será o `KnowledgeItem`.

Ela deve representar um item de conhecimento reutilizável dentro de uma organização.

Campos conceituais recomendados:

- id;
- organizationId;
- title;
- description;
- type;
- status;
- content;
- tags;
- createdBy;
- updatedBy;
- publishedAt;
- archivedAt;
- deprecatedAt;
- createdAt;
- updatedAt.

### 9.1 Título

Deve ser claro, específico e orientado ao uso.

Exemplos bons:

- Checklist de revisão de orçamento para UBS.
- Modelo de memorial descritivo para reforma escolar.
- Projeto de referência — Praça Central Santo André.
- Lição aprendida — divergência entre memorial e orçamento.

Exemplos ruins:

- Documento 1.
- Teste.
- Padrão.
- Coisas da prefeitura.

### 9.2 Descrição

Deve explicar resumidamente o que é o item e por que ele existe.

A descrição precisa ajudar o usuário a decidir se aquele conhecimento serve para o contexto atual.

### 9.3 Tipo

Define a natureza do conhecimento.

Tipos iniciais:

- technical_standard;
- document_model;
- reference_project;
- lesson_learned;
- review_checklist;
- delivery_standard.

### 9.4 Status

Define se o item está em rascunho, publicado, arquivado ou obsoleto.

### 9.5 Conteúdo

Campo principal de conteúdo do item.

Pode ser um texto rico ou estrutura JSON, dependendo da implementação.

Para o MVP, pode começar como texto/markdown simples. Futuramente, pode evoluir para blocos estruturados.

### 9.6 Tags

Tags permitem busca, recomendação e classificação.

Exemplos:

- reforma;
- escola;
- UBS;
- pavimentação;
- drenagem;
- prefeitura-sp;
- orçamento;
- memorial;
- acessibilidade;
- revisão;
- projeto-arquitetônico;
- relatório-fotográfico.

As tags são essenciais para a primeira versão de recomendação sem IA.

---

## 10. Relações com outros módulos

A Base de Conhecimento não deve ser isolada.

Ela precisa se relacionar com os principais elementos da plataforma.

### 10.1 Relação com Projetos

Um projeto pode usar itens de conhecimento.

Exemplos:

- projeto usa um documento modelo;
- projeto usa um checklist de revisão;
- projeto se baseia em um projeto de referência;
- projeto segue um padrão técnico;
- projeto registra uma lição aprendida ao final.

No futuro, um projeto também poderá gerar itens de conhecimento.

Fluxo desejado:

1. Projeto é finalizado.
2. Coordenador seleciona a ação “Promover para Base de Conhecimento”.
3. Sistema cria um item do tipo Projeto de Referência.
4. Usuário seleciona documentos, entregáveis e observações úteis.
5. Item é publicado para uso futuro.

### 10.2 Relação com Documentos

Documentos oficiais podem virar conhecimento.

Exemplos:

- documento oficial salvo como modelo;
- histórico de versões usado como aprendizado;
- documento aprovado vira referência;
- documento reprovado pode gerar lição aprendida.

Fluxo desejado:

1. Documento é marcado como versão oficial.
2. Sistema oferece a opção “Salvar como documento modelo”.
3. Usuário define título, descrição, tags e tipo.
4. Item é criado na Base de Conhecimento.

### 10.3 Relação com Revisões

Revisões são fonte de conhecimento.

Uma revisão reprovada geralmente contém um aprendizado.

Exemplos:

- orçamento reprovado por divergência de quantitativos;
- memorial incompatível com projeto arquitetônico;
- prancha enviada sem padrão correto;
- documento faltando assinatura do responsável técnico.

Fluxo desejado:

1. Revisão é reprovada.
2. Sistema sugere “Registrar lição aprendida”.
3. Usuário transforma o motivo da reprovação em item de conhecimento.
4. Esse item pode ser recomendado em projetos futuros similares.

### 10.4 Relação com Entregáveis

Itens de conhecimento podem apoiar entregáveis específicos.

Exemplos:

- checklist de revisão para orçamento;
- modelo de memorial para entregável “Memorial descritivo”;
- padrão técnico para entregável “Projeto arquitetônico”;
- lição aprendida relacionada ao entregável “Cronograma físico-financeiro”.

### 10.5 Relação com Templates

Templates continuam sendo entidades operacionais próprias.

A Base de Conhecimento pode referenciar templates, mas não deve substituir o módulo de templates.

O template é usado para gerar estrutura operacional de projeto.

A Knowledge Base documenta, explica, recomenda e contextualiza o uso desse template.

---

## 11. Conceito de KnowledgeRelation

Para manter flexibilidade, recomenda-se criar uma entidade ou estrutura chamada `KnowledgeRelation`.

Ela representa vínculos entre um item de conhecimento e outros elementos do sistema.

Campos conceituais:

- id;
- organizationId;
- knowledgeItemId;
- targetType;
- targetId;
- relationType;
- createdBy;
- createdAt.

Exemplos de targetType:

- project;
- deliverable;
- document;
- document_version;
- review;
- project_template.

Exemplos de relationType:

- used_in;
- generated_from;
- reference_for;
- model_for;
- checklist_for;
- lesson_from;
- related_to.

Essa estrutura evita acoplamento rígido e permite evoluir o módulo sem quebrar o domínio.

---

## 12. Conceito de KnowledgeAttachment

Alguns itens precisam ter arquivos anexados.

Exemplos:

- documento modelo em DOCX;
- planilha modelo em XLSX;
- relatório exemplo em PDF;
- prancha de referência;
- imagem ou evidência técnica.

A entidade `KnowledgeAttachment` deve representar arquivos vinculados a um item de conhecimento.

Campos conceituais:

- id;
- organizationId;
- knowledgeItemId;
- fileId;
- label;
- description;
- createdBy;
- createdAt.

Para MVP, caso o módulo de arquivos ainda esteja simples, o attachment pode começar vinculado à estrutura atual de documentos/arquivos.

---

## 13. Permissões e governança

A Base de Conhecimento precisa ter governança.

Nem todo colaborador deve conseguir publicar conhecimento oficial.

Papéis sugeridos:

### Owner / Admin

Pode:

- criar item;
- editar item;
- publicar item;
- arquivar item;
- marcar como obsoleto;
- excluir, se a regra permitir;
- gerenciar relações.

### Coordenador

Pode:

- criar item;
- editar seus itens;
- publicar, se autorizado;
- promover projeto para referência;
- registrar lições aprendidas;
- vincular conhecimento a projetos.

### Engenheiro / Projetista

Pode:

- consultar itens publicados;
- criar rascunhos;
- sugerir lições aprendidas;
- sugerir documentos modelo;
- usar conhecimento em projetos.

### Viewer

Pode:

- consultar itens publicados;
- não pode criar ou publicar.

Para MVP, permissões podem ser mais simples, mas a documentação e arquitetura devem considerar essa evolução.

---

## 14. Fluxos principais do épico

### 14.1 Criar item manualmente

Fluxo:

1. Usuário acessa Base de Conhecimento.
2. Clica em “Novo item”.
3. Seleciona o tipo de conhecimento.
4. Preenche título, descrição, conteúdo e tags.
5. Opcionalmente vincula projeto, documento ou entregável.
6. Salva como rascunho.
7. Usuário autorizado publica o item.

Esse é o fluxo mínimo do MVP.

### 14.2 Publicar item

Fluxo:

1. Item está em rascunho.
2. Usuário autorizado revisa o conteúdo.
3. Clica em “Publicar”.
4. Sistema registra data de publicação e usuário responsável.
5. Item passa a aparecer como conhecimento oficial.

Regra:

- apenas itens publicados devem ser considerados em recomendações operacionais.

### 14.3 Arquivar item

Fluxo:

1. Usuário identifica item que não deve mais ser usado.
2. Clica em “Arquivar”.
3. Sistema muda status para arquivado.
4. Item deixa de aparecer em recomendações padrão.
5. Histórico é preservado.

### 14.4 Buscar item

Fluxo:

1. Usuário acessa Base de Conhecimento.
2. Digita termo de busca.
3. Filtra por tipo, status e tags.
4. Sistema retorna itens correspondentes do tenant.

Busca inicial:

- título;
- descrição;
- conteúdo;
- tags;
- tipo;
- status.

### 14.5 Consultar detalhe

Fluxo:

1. Usuário abre item.
2. Sistema mostra título, tipo, status, descrição, conteúdo, tags e relações.
3. Usuário visualiza projetos, documentos ou entregáveis relacionados.
4. Usuário pode editar, publicar, arquivar ou usar em projeto, conforme permissão.

---

## 15. Fluxos preparados para próximos épicos

Este épico deve deixar espaço para os próximos fluxos, mesmo que nem todos sejam implementados agora.

### 15.1 Promover projeto para conhecimento

Objetivo futuro:

Transformar projeto finalizado em projeto de referência.

### 15.2 Salvar documento oficial como modelo

Objetivo futuro:

Transformar documento validado em documento modelo reutilizável.

### 15.3 Registrar revisão reprovada como lição aprendida

Objetivo futuro:

Transformar erro ou decisão de revisão em aprendizado reutilizável.

### 15.4 Recomendar conhecimento em projeto

Objetivo futuro:

Com base em tipo, tags e contexto do projeto, recomendar itens úteis da Base de Conhecimento.

### 15.5 Usar conhecimento ao criar projeto

Objetivo futuro:

Durante criação de projeto, permitir aplicar padrões, documentos modelo, checklists e referências.

---

## 16. Experiência de usuário esperada

A tela da Base de Conhecimento deve transmitir a ideia de acervo técnico vivo.

Ela não deve parecer apenas uma listagem vazia ou CRUD administrativo.

### 16.1 Listagem

Deve conter:

- título da página;
- descrição clara;
- busca principal;
- filtro por tipo;
- filtro por status;
- filtro por tags, se possível;
- botão “Novo item”;
- cards ou tabela de itens;
- estado vazio bem orientado.

Texto sugerido para estado vazio:

> Sua Base de Conhecimento ainda está vazia. Comece registrando padrões técnicos, documentos modelo, projetos de referência ou lições aprendidas para que a empresa reaproveite conhecimento em novos projetos.

### 16.2 Card de item

Cada card deve mostrar:

- título;
- tipo;
- status;
- descrição curta;
- tags;
- data de atualização;
- autor;
- relações principais, se existirem;
- ação para abrir.

### 16.3 Detalhe do item

Deve mostrar:

- cabeçalho com título, tipo e status;
- descrição;
- conteúdo;
- tags;
- anexos;
- relações;
- histórico básico;
- ações: editar, publicar, arquivar, usar em projeto.

### 16.4 Formulário de criação

Campos mínimos:

- tipo;
- título;
- descrição;
- conteúdo;
- tags;
- status inicial, geralmente rascunho;
- relações opcionais.

O formulário pode mudar conforme o tipo no futuro.

---

## 17. Regras de negócio

1. Todo item de conhecimento pertence a uma organização.
2. Nenhum usuário pode acessar item de conhecimento de outro tenant.
3. Todo item deve ter título, tipo, status e organização.
4. Itens publicados representam conhecimento validado ou aceito pela organização.
5. Itens em rascunho não devem ser usados em recomendações oficiais.
6. Itens arquivados devem permanecer consultáveis, mas fora do fluxo principal.
7. Itens obsoletos devem indicar que não são recomendados para novos projetos.
8. Tags devem ser usadas para busca e recomendação inicial.
9. Relações devem respeitar organizationId.
10. Não deve existir relação entre item de conhecimento de uma organização e projeto/documento de outra.
11. Publicação deve registrar quem publicou e quando.
12. Arquivamento deve registrar quem arquivou e quando, se possível.
13. Excluir fisicamente deve ser evitado no início; preferir arquivamento.
14. O módulo deve ser preparado para auditoria e histórico.

---

## 18. Eventos de domínio sugeridos

Eventos importantes:

- KnowledgeItemCreated;
- KnowledgeItemUpdated;
- KnowledgeItemPublished;
- KnowledgeItemArchived;
- KnowledgeItemDeprecated;
- KnowledgeItemLinkedToProject;
- KnowledgeItemLinkedToDocument;
- KnowledgeItemUsedInProject.

No MVP, os eventos podem ser in-process ou apenas registrados em ActivityLog.

No futuro, podem alimentar notificações, auditoria, recomendações e IA.

---

## 19. Arquitetura recomendada no backend

Módulo:

```txt
src/modules/knowledge-base/
  domain/
    entities/
      knowledge-item.entity.ts
      knowledge-relation.entity.ts
      knowledge-attachment.entity.ts
    value-objects/
      knowledge-item-type.vo.ts
      knowledge-item-status.vo.ts
      knowledge-tag.vo.ts
    repositories/
      knowledge-item.repository.ts
    events/
  application/
    use-cases/
      create-knowledge-item.use-case.ts
      update-knowledge-item.use-case.ts
      publish-knowledge-item.use-case.ts
      archive-knowledge-item.use-case.ts
      get-knowledge-item-details.use-case.ts
      search-knowledge-items.use-case.ts
      link-knowledge-item.use-case.ts
    dto/
    ports/
  infrastructure/
    persistence/
      typeorm/
        knowledge-item.orm-entity.ts
        knowledge-relation.orm-entity.ts
        knowledge-attachment.orm-entity.ts
        knowledge-item-typeorm.repository.ts
    mappers/
      knowledge-item.mapper.ts
  presentation/
    controllers/
      knowledge-base.controller.ts
```

Seguir os princípios do projeto:

- Clean Architecture;
- DDD;
- TypeORM isolado na infraestrutura;
- entidade de domínio separada da entidade ORM;
- use cases na camada application;
- controllers finos;
- organizationId obrigatório;
- testes unitários para casos de uso e regras de domínio.

---

## 20. Endpoints sugeridos

Endpoints REST iniciais:

```txt
GET    /knowledge-items
GET    /knowledge-items/:id
POST   /knowledge-items
PUT    /knowledge-items/:id
POST   /knowledge-items/:id/publish
POST   /knowledge-items/:id/archive
POST   /knowledge-items/:id/relations
DELETE /knowledge-items/:id/relations/:relationId
```

Filtros em `GET /knowledge-items`:

- search;
- type;
- status;
- tags;
- page;
- limit.

Exemplo:

```txt
GET /knowledge-items?search=orçamento&type=lesson_learned&status=published
```

---

## 21. Modelo de resposta sugerido

Listagem:

```json
{
  "items": [
    {
      "id": "uuid",
      "title": "Checklist de revisão de orçamento para UBS",
      "description": "Itens obrigatórios para validar orçamento antes do envio.",
      "type": "review_checklist",
      "status": "published",
      "tags": ["UBS", "orçamento", "revisão"],
      "updatedAt": "2026-05-29T10:00:00.000Z",
      "createdBy": {
        "id": "uuid",
        "name": "Lucas Eduardo"
      }
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 1
  }
}
```

Detalhe:

```json
{
  "id": "uuid",
  "title": "Checklist de revisão de orçamento para UBS",
  "description": "Itens obrigatórios para validar orçamento antes do envio.",
  "content": "...",
  "type": "review_checklist",
  "status": "published",
  "tags": ["UBS", "orçamento", "revisão"],
  "relations": [],
  "attachments": [],
  "createdAt": "2026-05-29T10:00:00.000Z",
  "updatedAt": "2026-05-29T10:00:00.000Z",
  "publishedAt": "2026-05-29T10:10:00.000Z"
}
```

---

## 22. Arquitetura recomendada no frontend

Módulo:

```txt
src/modules/knowledge-base/
  pages/
    KnowledgeBaseListPage.vue
    KnowledgeBaseDetailPage.vue
    KnowledgeBaseCreatePage.vue
    KnowledgeBaseEditPage.vue
  components/
    KnowledgeItemCard.vue
    KnowledgeItemForm.vue
    KnowledgeTypeSelect.vue
    KnowledgeStatusChip.vue
    KnowledgeTagsInput.vue
    KnowledgeRelationsPanel.vue
    KnowledgeEmptyState.vue
  services/
    knowledge-base.service.ts
  stores/
    knowledge-base.store.ts
  types/
    knowledge-item.types.ts
  composables/
    useKnowledgeItems.ts
```

A experiência deve ser integrada ao padrão visual atual da plataforma.

A tela não precisa ser extravagante, mas deve parecer útil e estratégica.

---

## 23. Rotas sugeridas no frontend

```txt
/knowledge-base
/knowledge-base/new
/knowledge-base/:id
/knowledge-base/:id/edit
```

---

## 24. Métricas de sucesso do épico

Este épico será considerado bem-sucedido quando:

1. Usuário conseguir criar item de conhecimento.
2. Usuário conseguir publicar item.
3. Usuário conseguir listar e buscar itens.
4. Usuário conseguir abrir detalhe de item.
5. Usuário conseguir arquivar item.
6. Itens respeitarem tenant/organizationId.
7. Tela da Base de Conhecimento deixar claro o valor do módulo.
8. Dados seedados permitirem testar a experiência.
9. Backend respeitar Clean Architecture e DDD.
10. Frontend estiver integrado aos endpoints reais.

---

## 25. Dados fake recomendados para seed

Criar itens iniciais para a organização `Engenharia Horizonte Ltda`.

### Item 1

Tipo: technical_standard  
Status: published  
Título: Padrão de nomenclatura de arquivos técnicos  
Tags: arquivos, padronização, entrega  
Descrição: Define como arquivos técnicos devem ser nomeados antes do envio ou armazenamento oficial.

### Item 2

Tipo: document_model  
Status: published  
Título: Modelo de memorial descritivo para reforma escolar  
Tags: memorial, escola, reforma  
Descrição: Documento modelo para iniciar memoriais descritivos de reformas escolares.

### Item 3

Tipo: reference_project  
Status: published  
Título: Projeto de referência — Reforma da Escola Municipal Jardim Primavera  
Tags: escola, reforma, prefeitura-sp, acessibilidade  
Descrição: Projeto usado como referência para reformas escolares com adequação de acessibilidade.

### Item 4

Tipo: lesson_learned  
Status: published  
Título: Validar quantitativos antes de fechar orçamento  
Tags: orçamento, quantitativos, revisão  
Descrição: Lição aprendida a partir de revisão reprovada por divergência entre memorial e planilha orçamentária.

### Item 5

Tipo: review_checklist  
Status: draft  
Título: Checklist de revisão de orçamento para UBS  
Tags: UBS, orçamento, revisão  
Descrição: Lista inicial de verificações para orçamento de unidades de saúde.

### Item 6

Tipo: delivery_standard  
Status: published  
Título: Padrão de entrega de pacote técnico para prefeitura  
Tags: prefeitura, entrega, pacote-técnico  
Descrição: Orienta a estrutura mínima de arquivos e documentos para envio de pacote técnico final.

---

## 26. Riscos e cuidados

### 26.1 Risco de virar wiki genérica

Mitigação:

- manter tipos de conhecimento claros;
- conectar itens com projetos/documentos/revisões;
- usar linguagem de engenharia;
- evitar campos genéricos demais sem contexto.

### 26.2 Risco de acervo vazio

Mitigação:

- criar seed realista;
- criar bons empty states;
- futuramente sugerir criação de conhecimento a partir de projetos e revisões.

### 26.3 Risco de conhecimento não confiável

Mitigação:

- usar status draft/published/archived/deprecated;
- limitar publicação por permissão;
- registrar autor e data;
- manter histórico.

### 26.4 Risco de overengineering

Mitigação:

- começar com tipos e relações simples;
- tags como array simples no MVP;
- conteúdo em markdown/texto no início;
- evoluir para blocos e embeddings depois.

---

## 27. O que fica fora deste épico

Este épico não precisa implementar:

- IA;
- embeddings;
- busca semântica;
- recomendações avançadas;
- promoção automática de projeto;
- análise automática de revisão;
- geração automática de documentos;
- estudo de viabilidade urbanística;
- permissões refinadas por campo;
- editor rico complexo;
- versionamento completo de KnowledgeItem.

Esses itens ficam para próximos épicos.

---

## 28. Backlog macro derivado deste épico

Este documento ainda não quebra as tarefas em granularidade final, mas sugere os blocos principais:

1. Modelagem de domínio da Knowledge Base.
2. Persistência e migrations.
3. Use cases principais.
4. Endpoints REST.
5. Seeds de dados realistas.
6. Listagem e filtros no frontend.
7. Formulário de criação/edição.
8. Tela de detalhe.
9. Publicar/arquivar.
10. Relações iniciais com projetos/documentos.
11. Ajustes de UX e empty states.
12. Testes unitários e integração mínima.

---

## 29. Direção estratégica

A Base de Conhecimento é mais do que um módulo funcional.

Ela é a peça que sustenta o posicionamento da plataforma.

Sem ela, o produto parece uma ferramenta de gestão técnica.

Com ela, o produto começa a se posicionar como uma plataforma de inteligência operacional para engenharia.

A implementação deste épico deve sempre proteger a tese:

> Projetos geram conhecimento. Conhecimento melhora novos projetos.

Esse épico cria o acervo.

Os próximos épicos farão esse acervo ser alimentado automaticamente, recomendado no momento certo e usado para melhorar a execução de novos projetos.
## Atualizacao pos-epico (implementacao)

Status: modulo Knowledge Base operacional entregue com:
- fluxos principais e fluxos derivados (projeto/documento/revisao);
- rastreabilidade por activity log;
- RBAC minimo aplicado no backend e frontend;
- roteiro de testes consolidado em `docs/modules/knowledge-base-test-scenarios.md`.

Pendencias para proximas fases:
- busca semantica/embeddings;
- versionamento de itens publicados;
- workflow de aprovacao avancado.
