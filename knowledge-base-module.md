# Knowledge Base Module — Documentação Principal

## 1. Visão Geral

O módulo **Knowledge Base** é um dos módulos estratégicos da plataforma. Ele não deve ser tratado como uma simples wiki, biblioteca de arquivos ou tela genérica de anotações. A Knowledge Base deve ser entendida como o **cérebro operacional do tenant**.

A proposta central é transformar o conhecimento técnico, operacional e histórico da empresa em um acervo estruturado, reutilizável, pesquisável e conectado ao fluxo real dos projetos de engenharia.

Em empresas de engenharia, muito conhecimento importante normalmente fica disperso em lugares como:

- Google Drive;
- pastas locais;
- WhatsApp;
- e-mails;
- memória de engenheiros mais experientes;
- planilhas antigas;
- projetos anteriores difíceis de localizar;
- documentos reaproveitados sem rastreabilidade;
- padrões informais conhecidos apenas por algumas pessoas.

Esse cenário gera retrabalho, erro de versão, dificuldade de padronização, perda de histórico, inconsistência nas entregas e dificuldade para reaproveitar projetos anteriores.

A Knowledge Base nasce para atacar exatamente esse problema.

A definição principal do módulo é:

> A Knowledge Base é o acervo técnico padronizado do tenant, formado por padrões, modelos, referências, lições aprendidas, documentos, checklists, decisões e ativos técnicos reutilizáveis que ajudam a empresa a reduzir retrabalho e conduzir novos projetos com mais consistência.

Ela deve funcionar como um ciclo vivo:

```txt
Projetos geram conhecimento.
Conhecimento melhora novos projetos.
Novos projetos geram mais conhecimento.
```

Esse ciclo é um dos diferenciais mais importantes da plataforma.

---

## 2. Problema que o módulo resolve

A Knowledge Base existe porque empresas de engenharia frequentemente sofrem com problemas como:

- dificuldade para lembrar qual projeto antigo pode servir de referência;
- ausência de padrões claros para tipos de projeto recorrentes;
- cada colaborador organizando arquivos e entregas do seu próprio jeito;
- documentos modelo espalhados em pastas antigas;
- entregáveis sendo recriados do zero sem necessidade;
- revisões técnicas acontecendo sem checklist padronizado;
- erros recorrentes não sendo registrados;
- projetos parecidos sendo executados de formas completamente diferentes;
- perda de conhecimento quando um colaborador sai da empresa;
- dificuldade de saber qual documento ou padrão está vigente;
- uso de arquivos antigos ou desatualizados como base;
- falta de histórico sobre por que determinada decisão técnica foi tomada;
- falta de rastreabilidade entre projeto, documento, revisão e aprendizado.

O módulo deve ajudar a responder perguntas como:

- Qual projeto antigo podemos usar como referência para este novo projeto?
- Qual modelo de memorial descritivo usamos para reforma escolar?
- Qual checklist de revisão deve ser aplicado antes de enviar o projeto?
- Quais erros já aconteceram nesse tipo de obra?
- Quais documentos são normalmente exigidos nesse contexto?
- Qual template é usado para um projeto de UBS?
- Qual padrão interno deve ser seguido para nomear arquivos?
- Qual entrega anterior foi considerada boa o suficiente para ser reutilizada?
- Qual projeto parecido teve problema de orçamento, drenagem ou compatibilização?
- Quais lições aprendidas existem sobre esse tipo de projeto?

A Knowledge Base deve transformar respostas que hoje estão espalhadas ou na cabeça das pessoas em dados estruturados dentro da plataforma.

---

## 3. O que a Knowledge Base não deve ser

É importante deixar claro o que o módulo **não** deve virar.

A Knowledge Base não deve ser apenas:

- uma wiki genérica;
- uma pasta de arquivos;
- um clone de Notion;
- uma biblioteca solta de documentos;
- um repositório morto de PDFs;
- um CRUD de artigos sem relação com projetos;
- uma tela para escrever textos desconectados do domínio;
- um substituto genérico para Google Drive ou SharePoint.

Essas ferramentas já existem e são genéricas.

O diferencial da plataforma é que a Knowledge Base deve estar conectada ao domínio de engenharia e ao fluxo operacional do sistema.

Ou seja, um item da Knowledge Base pode estar relacionado com:

- projetos técnicos;
- templates de projeto;
- entregáveis;
- documentos versionados;
- revisões;
- checklists;
- padrões internos;
- projetos antigos;
- lições aprendidas;
- estudos de viabilidade;
- regras urbanísticas;
- históricos de aprovação;
- decisões técnicas.

A Knowledge Base deve ser uma camada de inteligência operacional, não apenas uma camada de conteúdo.

---

## 4. Papel estratégico dentro da plataforma

A plataforma como um todo busca ajudar empresas de engenharia a:

- padronizar projetos;
- controlar documentos;
- controlar versões;
- controlar revisões;
- organizar entregas;
- reutilizar projetos antigos;
- reduzir retrabalho;
- aumentar rastreabilidade;
- melhorar qualidade técnica;
- profissionalizar processos internos.

A Knowledge Base é o módulo que transforma essa operação em aprendizado acumulado.

Ela deve permitir que a empresa pare de depender exclusivamente da experiência individual das pessoas e passe a criar uma memória organizacional estruturada.

Em termos de produto, esse módulo muda a percepção do SaaS.

Sem Knowledge Base, a plataforma pode parecer um sistema de gestão de projetos, documentos e revisões.

Com Knowledge Base, a plataforma se torna uma **plataforma de inteligência operacional para engenharia**.

A Knowledge Base é o lugar onde ficam guardados:

- como a empresa trabalha;
- o que a empresa já fez;
- o que deu certo;
- o que deu errado;
- quais padrões devem ser seguidos;
- quais documentos devem ser reutilizados;
- quais projetos anteriores servem como base;
- quais cuidados precisam ser lembrados;
- quais revisões devem acontecer;
- quais aprendizados precisam ser preservados.

---

## 5. Conceito principal: KnowledgeItem

O conceito principal do módulo será o `KnowledgeItem`.

Um `KnowledgeItem` representa uma unidade de conhecimento reutilizável dentro da organização.

Ele pode representar diferentes tipos de conhecimento, como:

- padrão técnico;
- documento modelo;
- projeto de referência;
- lição aprendida;
- checklist de revisão;
- padrão de entrega;
- referência de regra urbanística;
- item conectado a um template de projeto.

A entidade `KnowledgeItem` deve ser flexível o suficiente para representar diferentes tipos de conhecimento, mas estruturada o suficiente para não virar uma anotação genérica.

Campos conceituais básicos:

```txt
KnowledgeItem
- id
- organizationId
- title
- description
- type
- status
- visibility
- tags
- content
- createdBy
- updatedBy
- createdAt
- updatedAt
- publishedAt
- archivedAt
```

A presença do `organizationId` é obrigatória porque o sistema é multi-tenant. Cada tenant tem sua própria base de conhecimento, seus próprios padrões, seus próprios documentos e seu próprio histórico.

Nenhum item de conhecimento deve ser compartilhado entre organizações sem uma decisão explícita de produto no futuro.

---

## 6. Tipos de itens da Knowledge Base

A Knowledge Base deve começar com tipos bem definidos. Isso evita que o módulo vire uma wiki genérica e ajuda a interface a guiar melhor o usuário.

A recomendação inicial é trabalhar com os seguintes tipos.

---

### 6.1 Technical Standard

Representa um padrão técnico ou operacional da empresa.

Esse tipo responde à pergunta:

> Como fazemos isso aqui dentro?

Exemplos:

- Padrão de nomenclatura de arquivos;
- Padrão de organização de pastas por projeto;
- Padrão de revisão de projeto arquitetônico;
- Padrão de montagem de memorial descritivo;
- Padrão de apresentação de prancha;
- Padrão para cálculo de quantitativos;
- Padrão de entrega para prefeitura;
- Padrão interno para revisão de orçamento;
- Padrão de validação de compatibilização entre disciplinas.

Campos adicionais úteis:

```txt
- context
- whenToUse
- whenNotToUse
- rules
- examples
- relatedDeliverables
- relatedDocuments
```

Exemplo de item:

```txt
Título: Padrão de nomenclatura de arquivos técnicos
Tipo: technical_standard
Descrição: Define como os arquivos devem ser nomeados antes de serem enviados para revisão ou entrega final.
Tags: documentos, padrão, revisão, nomenclatura
```

---

### 6.2 Document Model

Representa um documento modelo reutilizável.

Esse tipo responde à pergunta:

> Qual arquivo base usamos para começar?

Exemplos:

- Modelo de memorial descritivo;
- Modelo de cronograma físico-financeiro;
- Modelo de relatório técnico;
- Modelo de planilha orçamentária;
- Modelo de relatório fotográfico;
- Modelo de ART/RRT;
- Modelo de checklist de fiscalização;
- Modelo de termo de entrega;
- Modelo de estudo de viabilidade.

Campos adicionais úteis:

```txt
- documentType
- fileId
- usageInstructions
- relatedProjectTypes
- relatedDeliverables
- version
- validFrom
- deprecatedAt
```

Esse tipo de item deve conseguir se relacionar com o módulo de documentos e versões.

Um documento modelo pode ter um arquivo principal, mas também pode ter descrição, instruções de uso, tags e contexto de aplicação.

Exemplo de item:

```txt
Título: Modelo de Memorial Descritivo para Reforma Escolar
Tipo: document_model
Descrição: Documento base usado em projetos de reforma escolar executados para prefeituras.
Tags: memorial, reforma escolar, prefeitura, documento modelo
```

---

### 6.3 Project Reference

Representa um projeto antigo promovido como referência reutilizável.

Esse tipo responde à pergunta:

> Que projeto real parecido já fizemos e podemos usar como base?

Nem todo projeto finalizado deve automaticamente virar referência. A recomendação é criar um fluxo explícito de promoção:

```txt
Projeto finalizado
→ coordenador avalia
→ escolhe o que vale reaproveitar
→ registra observações
→ adiciona tags
→ publica como referência na Knowledge Base
```

Exemplos:

- Reforma da Escola Municipal Jardim Primavera;
- Construção da UBS Vila Esperança;
- Projeto de Pavimentação da Rua das Acácias;
- Revitalização da Praça Central;
- Sistema de Drenagem do Bairro São Lucas.

Campos adicionais úteis:

```txt
- sourceProjectId
- referenceReason
- reusableDeliverables
- reusableDocuments
- warnings
- lessonsLearned
- projectType
- clientType
- location
```

Exemplo de item:

```txt
Título: Reforma da Escola Municipal Jardim Primavera
Tipo: project_reference
Descrição: Projeto utilizado como referência para reformas escolares com adequação de acessibilidade e revisão de cobertura.
Tags: reforma escolar, acessibilidade, cobertura, prefeitura-sp
```

Esse é um dos tipos mais importantes do módulo, porque ele ataca diretamente a dor de ter que lembrar qual projeto antigo pode servir como base.

---

### 6.4 Lesson Learned

Representa um aprendizado, problema recorrente ou cuidado técnico que a empresa não quer esquecer.

Esse tipo responde à pergunta:

> O que já aprendemos do jeito difícil e não queremos repetir?

Exemplos:

- Em reformas escolares, sempre validar acessibilidade antes de fechar orçamento;
- Em projetos de pavimentação, revisar drenagem antes de fechar quantitativos;
- Em UBS, compatibilizar hidráulica e arquitetura antes da revisão final;
- Em projetos de praça, iluminação costuma impactar orçamento mais do que o previsto;
- Erro recorrente: orçamento não bate com memorial descritivo;
- A prefeitura X costuma exigir documentação adicional;
- O uso de projeto antigo sem revisar legislação causou retrabalho.

Campos adicionais úteis:

```txt
- context
- problem
- impact
- recommendation
- relatedProjects
- relatedDeliverables
- severity
```

Exemplo de item:

```txt
Título: Validar acessibilidade antes do orçamento em reformas escolares
Tipo: lesson_learned
Descrição: Em projetos anteriores, alterações de acessibilidade feitas tardiamente geraram retrabalho no orçamento e no memorial.
Tags: acessibilidade, reforma escolar, orçamento, retrabalho
```

Esse tipo é extremamente valioso porque captura o conhecimento que normalmente fica apenas na cabeça de profissionais experientes.

---

### 6.5 Review Checklist

Representa um checklist padronizado de revisão técnica.

Esse tipo responde à pergunta:

> O que precisa ser conferido antes de aprovar ou enviar?

Exemplos:

- Checklist de revisão de projeto arquitetônico;
- Checklist de revisão de orçamento;
- Checklist de revisão de memorial descritivo;
- Checklist de compatibilização entre disciplinas;
- Checklist de revisão antes do envio para prefeitura;
- Checklist de validação de relatório fotográfico;
- Checklist de entrega final.

Campos adicionais úteis:

```txt
- checklistItems
- applicableProjectTypes
- applicableDeliverables
- approvalCriteria
- requiredRole
```

Exemplo de item:

```txt
Título: Checklist de revisão de orçamento para reforma escolar
Tipo: review_checklist
Descrição: Lista de validações obrigatórias antes de aprovar o orçamento de uma reforma escolar.
Tags: orçamento, revisão, reforma escolar, checklist
```

Esse tipo pode se integrar futuramente ao módulo de Reviews, permitindo que uma revisão técnica use um checklist publicado na Knowledge Base.

---

### 6.6 Delivery Standard

Representa um padrão de entrega para um determinado cliente, prefeitura, tipo de projeto ou contexto.

Esse tipo responde à pergunta:

> Como essa entrega deve ser preparada?

Exemplos:

- Padrão de entrega para Prefeitura de São Paulo;
- Padrão de entrega de projeto de pavimentação;
- Padrão de pacote final para reforma escolar;
- Padrão de envio de relatório fotográfico;
- Padrão de organização de arquivos finais.

Campos adicionais úteis:

```txt
- requiredDocuments
- namingRules
- outputFormats
- submissionInstructions
- relatedClient
- relatedProjectTypes
```

Esse tipo pode se relacionar com entregáveis e documentos finais do projeto.

---

### 6.7 Zoning Rule Reference

Representa uma referência técnica ou legal associada a regras urbanísticas, zoneamento, plano diretor ou estudos de viabilidade.

Esse tipo deve se tornar especialmente útil quando o módulo de Estudos de Viabilidade Urbanística for implementado.

Esse tipo responde à pergunta:

> Que regra, fonte ou interpretação urbanística precisa ser considerada nesse contexto?

Exemplos:

- Parâmetros urbanísticos para Zona Mista;
- Observações sobre ZM-1 em São Paulo;
- Cuidados ao consultar GeoSampa;
- Interpretação interna sobre determinada tabela do plano diretor;
- Fonte oficial para zoneamento de São Paulo;
- Checklist de validação antes de emitir estudo de viabilidade.

Campos adicionais úteis:

```txt
- sourceName
- sourceUrl
- legalReference
- validFrom
- validTo
- zoneCode
- parameters
- notes
```

Esse tipo deve sempre preservar rastreabilidade da fonte.

---

## 7. Relação entre Knowledge Base e Templates

Existe uma decisão arquitetural importante: templates de projeto devem ser entidades próprias ou apenas itens da Knowledge Base?

A recomendação é usar uma abordagem híbrida.

### 7.1 Templates como domínio próprio

O módulo de Templates deve continuar existindo como domínio próprio porque templates têm comportamento operacional.

Um `ProjectTemplate` pode:

- gerar entregáveis;
- gerar checklists;
- gerar estrutura documental;
- gerar etapas padrão;
- definir padrões iniciais do projeto;
- ser aplicado em um novo projeto;
- ter versionamento próprio futuramente.

Por isso, ele não deve ser apenas um texto dentro da Knowledge Base.

### 7.2 Knowledge Base como camada de acervo

A Knowledge Base pode publicar ou referenciar um template.

Exemplo:

```txt
KnowledgeItem
- type: project_template
- linkedTemplateId: uuid
```

Nesse modelo:

- `ProjectTemplate` continua sendo uma entidade operacional;
- `KnowledgeItem` funciona como camada de documentação, descoberta, explicação e acervo;
- o usuário pode buscar o template pela Knowledge Base;
- o template pode ser usado na criação de projetos;
- a Knowledge Base pode explicar quando usar aquele template, quais cuidados tomar e quais projetos servem de referência.

Essa separação mantém o domínio limpo.

---

## 8. Relação entre Knowledge Base e Projects

A relação com projetos é uma das partes mais importantes do módulo.

Um projeto pode tanto **usar conhecimento** quanto **gerar conhecimento**.

---

### 8.1 Projeto usando conhecimento

Ao criar ou conduzir um projeto, o usuário pode usar itens da Knowledge Base.

Exemplo:

```txt
Novo projeto: Reforma da Escola Municipal Aurora

Itens usados:
- Template de Reforma Escolar
- Modelo de Memorial Descritivo para Reforma Escolar
- Checklist de Revisão de Acessibilidade
- Projeto de referência: Reforma Escola Jardim Primavera
- Lição aprendida: Validar cobertura antes de fechar orçamento
```

Isso permite que o projeto já nasça com mais maturidade e menos improviso.

---

### 8.2 Projeto gerando conhecimento

Quando um projeto é finalizado, revisado ou considerado uma boa referência, ele pode gerar itens para a base.

Exemplo:

```txt
Projeto finalizado
→ ação: Adicionar à base de conhecimento
→ usuário seleciona tipo: Projeto de referência
→ seleciona entregáveis úteis
→ seleciona documentos reutilizáveis
→ registra observações
→ registra erros evitáveis
→ adiciona tags
→ publica
```

Isso cria um ciclo de melhoria contínua.

---

## 9. Fluxos principais do módulo

### 9.1 Criar item manualmente

Fluxo:

```txt
Usuário acessa Knowledge Base
→ clica em Novo Item
→ escolhe o tipo de conhecimento
→ preenche título e descrição
→ adiciona tags
→ adiciona conteúdo específico do tipo
→ vincula projetos, documentos, templates ou entregáveis
→ salva como rascunho
→ publica quando estiver validado
```

Esse é o fluxo mais simples e deve existir no MVP.

---

### 9.2 Publicar item

Nem todo item criado deve ser imediatamente oficial.

O fluxo de publicação garante confiabilidade.

Status recomendados:

```txt
draft
published
archived
deprecated
```

Significado:

- `draft`: item em elaboração;
- `published`: item oficial e disponível para uso;
- `archived`: item arquivado, não aparece como recomendação principal;
- `deprecated`: item antigo ou substituído por outro padrão.

Apenas usuários com permissão adequada devem publicar itens.

Sugestão de permissão:

- `owner`: pode criar, editar, publicar, arquivar e remover;
- `admin`: pode criar, editar, publicar e arquivar;
- `coordinator`: pode criar, editar e publicar itens técnicos;
- `engineer`: pode criar rascunhos e sugerir alterações;
- `designer`: pode criar rascunhos e consultar;
- `viewer`: apenas consulta.

---

### 9.3 Promover projeto para referência

Esse é um fluxo nobre do módulo.

Fluxo:

```txt
Usuário acessa um projeto finalizado
→ clica em Adicionar à base de conhecimento
→ escolhe Projeto de Referência
→ sistema pré-preenche dados do projeto
→ usuário seleciona entregáveis úteis
→ usuário seleciona documentos reutilizáveis
→ usuário registra por que esse projeto é uma boa referência
→ usuário adiciona tags
→ usuário registra alertas e lições aprendidas
→ item é salvo como rascunho ou publicado
```

Esse fluxo é importante porque transforma projetos reais em ativos reutilizáveis.

---

### 9.4 Usar item em projeto

Fluxo:

```txt
Usuário acessa um projeto
→ clica em Adicionar referência da base
→ busca itens por tipo, tags ou texto
→ seleciona itens relevantes
→ vincula ao projeto
→ sistema registra uso
```

Exemplos de uso:

- usar um projeto de referência;
- aplicar um checklist de revisão;
- anexar um documento modelo;
- consultar uma lição aprendida;
- seguir um padrão técnico.

---

### 9.5 Busca na base

A busca inicial pode ser simples, mas precisa ser bem pensada.

Filtros recomendados:

- texto livre;
- tipo de item;
- tags;
- status;
- projeto relacionado;
- template relacionado;
- entregável relacionado;
- criado por;
- atualizado recentemente;
- mais usados;
- publicados;
- arquivados;
- depreciados.

No MVP, a busca pode usar campos como:

```txt
- title
- description
- tags
- type
- status
```

Futuramente, pode evoluir para busca semântica com embeddings.

---

## 10. Relações entre entidades

A Knowledge Base precisa se conectar com outros módulos do sistema.

A recomendação é usar uma entidade genérica de relacionamento chamada `KnowledgeRelation`.

### 10.1 KnowledgeRelation

Representa a relação entre um item de conhecimento e outra entidade do sistema.

Campos conceituais:

```txt
KnowledgeRelation
- id
- organizationId
- knowledgeItemId
- targetType
- targetId
- relationType
- createdBy
- createdAt
```

Exemplos de `targetType`:

```txt
project
project_template
deliverable
document_version
review
feasibility_study
```

Exemplos de `relationType`:

```txt
reference_from
used_in
standard_for
based_on
related_to
generated_from
attached_to
recommended_for
```

Exemplos práticos:

```txt
KnowledgeItem: Modelo de Memorial Descritivo
Relation:
- targetType: deliverable
- relationType: standard_for

KnowledgeItem: Reforma Escola Jardim Primavera
Relation:
- targetType: project
- relationType: generated_from

KnowledgeItem: Checklist de Revisão de Orçamento
Relation:
- targetType: review
- relationType: used_in
```

Essa abordagem evita criar muitas tabelas de relação específicas logo no começo e mantém flexibilidade.

---

## 11. Anexos e documentos vinculados

Nem todo item da Knowledge Base terá arquivo, mas muitos terão.

Para isso, a recomendação é criar `KnowledgeAttachment`.

### 11.1 KnowledgeAttachment

Campos conceituais:

```txt
KnowledgeAttachment
- id
- organizationId
- knowledgeItemId
- fileId
- label
- description
- createdBy
- createdAt
```

O `fileId` deve apontar para o módulo de arquivos/documentos da plataforma.

Exemplos:

- modelo de memorial em `.docx`;
- planilha orçamentária modelo em `.xlsx`;
- PDF de referência;
- prancha exemplo;
- relatório fotográfico;
- checklist em PDF;
- arquivo de projeto antigo.

A Knowledge Base não deve duplicar a lógica de upload do módulo de documentos. Ela deve reutilizar o mecanismo de arquivos já existente.

---

## 12. Registro de uso

No futuro, é recomendável criar `KnowledgeUsage`.

Essa entidade registra quando um item da base foi usado em um projeto.

Campos conceituais:

```txt
KnowledgeUsage
- id
- organizationId
- knowledgeItemId
- projectId
- usedBy
- usedAt
- usageContext
```

Isso permite responder perguntas importantes:

- Quais padrões são mais usados?
- Quais documentos modelo são mais úteis?
- Quais projetos de referência são mais consultados?
- Quais itens nunca são usados?
- Que conhecimento está obsoleto?
- Que template mais gera projetos?

Para o MVP, essa entidade pode ser opcional. Mas a arquitetura deve permitir sua inclusão futura sem grandes refatorações.

---

## 13. Entidades recomendadas no backend

Estrutura inicial recomendada:

```txt
knowledge-base/
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
      knowledge-item-created.event.ts
      knowledge-item-published.event.ts
      knowledge-item-archived.event.ts
      project-promoted-to-knowledge.event.ts
  application/
    use-cases/
      create-knowledge-item.use-case.ts
      update-knowledge-item.use-case.ts
      publish-knowledge-item.use-case.ts
      archive-knowledge-item.use-case.ts
      search-knowledge-items.use-case.ts
      get-knowledge-item-details.use-case.ts
      link-knowledge-item.use-case.ts
      promote-project-to-knowledge.use-case.ts
      use-knowledge-item-in-project.use-case.ts
    dto/
    ports/
  infrastructure/
    persistence/
      typeorm/
    mappers/
  presentation/
    controllers/
```

---

## 14. Value Objects recomendados

### 14.1 KnowledgeItemType

Deve controlar os tipos válidos de item.

Valores iniciais recomendados:

```txt
technical_standard
document_model
project_reference
lesson_learned
review_checklist
delivery_standard
zoning_rule_reference
project_template
```

Mesmo que `project_template` seja operacionalmente uma entidade separada, ele pode existir como tipo de KnowledgeItem para publicação/referência.

---

### 14.2 KnowledgeItemStatus

Valores recomendados:

```txt
draft
published
archived
deprecated
```

Regras:

- um item novo começa como `draft`;
- apenas itens `published` devem ser usados como recomendação principal;
- itens `archived` continuam acessíveis no histórico;
- itens `deprecated` devem indicar que existe uma versão melhor ou mais atual.

---

### 14.3 KnowledgeTag

Representa uma tag válida.

No MVP, tags podem ser armazenadas como array de strings. Porém, é importante normalizar minimamente:

- remover espaços extras;
- usar lowercase;
- evitar duplicidade;
- limitar tamanho;
- bloquear tags vazias.

Exemplos de tags:

```txt
reforma
escola
ubs
pavimentacao
drenagem
orcamento
memorial
acessibilidade
prefeitura-sp
projeto-arquitetonico
relatorio-fotografico
zoneamento
geosampa
```

---

## 15. Casos de uso iniciais

### 15.1 CreateKnowledgeItem

Responsável por criar um novo item de conhecimento.

Entrada esperada:

```txt
organizationId
createdBy
title
description
type
tags
content
```

Regras:

- título é obrigatório;
- tipo deve ser válido;
- organizationId é obrigatório;
- item deve iniciar como `draft`, salvo se houver regra explícita permitindo publicação direta;
- tags devem ser normalizadas;
- usuário precisa ter permissão para criar item.

---

### 15.2 UpdateKnowledgeItem

Responsável por editar um item existente.

Regras:

- item precisa pertencer à organização;
- usuário precisa ter permissão;
- item arquivado pode exigir fluxo especial para edição;
- alterações importantes devem registrar atividade.

---

### 15.3 PublishKnowledgeItem

Responsável por publicar um item.

Regras:

- item precisa estar em `draft` ou `deprecated`, conforme regra futura;
- usuário precisa ter permissão de publicação;
- item precisa ter conteúdo mínimo;
- `publishedAt` deve ser preenchido;
- evento `KnowledgeItemPublished` deve ser emitido.

---

### 15.4 ArchiveKnowledgeItem

Responsável por arquivar um item.

Regras:

- item precisa pertencer à organização;
- usuário precisa ter permissão;
- item arquivado não deve aparecer como recomendação principal;
- relações e histórico devem ser preservados.

---

### 15.5 SearchKnowledgeItems

Responsável por buscar itens da base.

Filtros:

```txt
organizationId
query
type
status
tags
createdBy
relatedTargetType
relatedTargetId
```

Regras:

- sempre filtrar por `organizationId`;
- por padrão, retornar itens `published`;
- permitir visualizar drafts apenas para usuários autorizados;
- ordenar por relevância, atualização ou uso.

---

### 15.6 GetKnowledgeItemDetails

Responsável por exibir detalhes completos de um item.

Deve retornar:

- dados principais;
- anexos;
- relações;
- projetos relacionados;
- templates relacionados;
- documentos vinculados;
- histórico de alterações, se disponível.

---

### 15.7 LinkKnowledgeItem

Responsável por criar relações entre item da base e outras entidades.

Exemplo:

```txt
Vincular checklist de revisão ao entregável Orçamento.
Vincular projeto de referência a um projeto novo.
Vincular documento modelo a um template.
```

---

### 15.8 PromoteProjectToKnowledge

Responsável por transformar um projeto existente em item da base.

Entrada esperada:

```txt
organizationId
projectId
createdBy
title
description
tags
selectedDeliverables
selectedDocuments
lessonsLearned
warnings
```

Regras:

- projeto precisa pertencer à organização;
- usuário precisa ter permissão;
- o item criado deve ter tipo `project_reference`;
- deve criar relação com o projeto de origem;
- pode copiar ou referenciar documentos e entregáveis selecionados;
- deve registrar evento `ProjectPromotedToKnowledge`.

---

### 15.9 UseKnowledgeItemInProject

Responsável por registrar que um item foi usado em um projeto.

No MVP, pode apenas criar uma relação.

Futuramente, pode criar um registro em `KnowledgeUsage`.

---

## 16. Eventos de domínio

Eventos recomendados:

```txt
KnowledgeItemCreated
KnowledgeItemPublished
KnowledgeItemArchived
KnowledgeItemDeprecated
KnowledgeItemLinkedToProject
ProjectPromotedToKnowledge
KnowledgeItemUsedInProject
```

No início, os eventos podem ser in-process.

Futuramente, podem alimentar:

- activity log;
- notificações;
- auditoria;
- sugestões automáticas;
- métricas de uso;
- integrações;
- inteligência artificial.

---

## 17. Integração com Activity Log

Toda ação relevante deve gerar registro de atividade.

Exemplos:

```txt
Lucas criou o item "Modelo de Memorial Descritivo para Reforma Escolar".
Leonardo publicou o checklist "Revisão de Orçamento".
Rafael promoveu o projeto "UBS Vila Esperança" para referência.
Lucas vinculou a lição aprendida "Validar acessibilidade" ao projeto "Reforma Escola Aurora".
```

Isso ajuda a manter rastreabilidade e torna a plataforma mais profissional.

---

## 18. Interface do usuário

### 18.1 Listagem da Knowledge Base

A tela de listagem deve ter:

- campo de busca;
- filtros por tipo;
- filtros por status;
- filtros por tags;
- filtros por criado por;
- filtro de itens publicados;
- filtro de itens arquivados;
- cards ou tabela;
- ação de novo item.

Cada card pode exibir:

```txt
- título
- tipo
- descrição resumida
- tags
- status
- última atualização
- criado por
- quantidade de relações ou usos
```

Tipos devem ter ícones ou cores diferentes para facilitar leitura.

---

### 18.2 Detalhe do item

A tela de detalhe deve conter:

- título;
- tipo;
- status;
- tags;
- descrição;
- conteúdo principal;
- anexos;
- projetos relacionados;
- templates relacionados;
- entregáveis relacionados;
- documentos vinculados;
- lições relacionadas;
- histórico de atividade;
- ações disponíveis.

Ações possíveis:

- editar;
- publicar;
- arquivar;
- depreciar;
- duplicar;
- usar em projeto;
- vincular a projeto;
- vincular a template;
- adicionar anexo.

---

### 18.3 Criar item

O formulário de criação deve mudar de acordo com o tipo selecionado.

Campos comuns:

```txt
title
description
type
tags
content
```

Campos específicos por tipo:

- `project_reference`: projeto base, entregáveis reutilizáveis, documentos úteis, alertas;
- `lesson_learned`: problema, impacto, recomendação, contexto;
- `document_model`: arquivo, instruções de uso, tipo de documento;
- `review_checklist`: itens do checklist, critérios de aprovação;
- `technical_standard`: regras, exemplos, quando usar;
- `delivery_standard`: documentos exigidos, formatos, instruções de envio;
- `zoning_rule_reference`: fonte, referência legal, zona, parâmetros.

---

### 18.4 Empty states

A Knowledge Base deve ter estados vazios bem escritos.

Exemplo:

```txt
Sua base de conhecimento ainda está vazia.
Comece adicionando um modelo de documento, uma lição aprendida ou promovendo um projeto finalizado como referência.
```

Outro exemplo:

```txt
Nenhum projeto de referência encontrado.
Quando um projeto for finalizado, você poderá adicioná-lo à base para reutilizar em trabalhos futuros.
```

Esses textos ajudam o usuário a entender o valor do módulo.

---

## 19. MVP recomendado

Para a primeira versão, o módulo não precisa nascer com tudo.

MVP recomendado:

Tipos iniciais:

```txt
project_reference
document_model
technical_standard
lesson_learned
```

Funcionalidades iniciais:

```txt
- criar item
- editar item
- publicar item
- arquivar item
- listar itens
- buscar por texto
- filtrar por tipo
- filtrar por tags
- ver detalhe
- vincular item a projeto
- promover projeto para referência
```

Funcionalidades que podem ficar para depois:

```txt
- busca semântica
- embeddings
- IA generativa
- sugestões automáticas
- métricas avançadas de uso
- versionamento de KnowledgeItem
- aprovação formal de alterações
- workflow complexo de revisão de conhecimento
```

---

## 20. Evolução futura com IA

A Knowledge Base é a base ideal para futura integração com IA.

Depois que os dados estiverem estruturados, o sistema poderá permitir perguntas como:

```txt
Temos algum projeto parecido com uma UBS em terreno pequeno?
Qual checklist usamos para projeto de drenagem?
Que erros já tivemos em reformas escolares?
Qual documento modelo devo usar para memorial descritivo?
Quais projetos antigos podem servir de referência para uma praça pública?
```

Para isso, futuramente pode existir uma tabela de embeddings:

```txt
knowledge_embeddings
- id
- organizationId
- knowledgeItemId
- contentChunk
- embedding
- createdAt
```

A IA não deve ser a primeira versão do módulo.

Primeiro, a plataforma precisa criar uma base estruturada.

Depois, a IA pode atuar como camada de busca, sugestão e interpretação.

---

## 21. Relação com Estudos de Viabilidade Urbanística

O módulo de Estudos de Viabilidade Urbanística poderá usar a Knowledge Base para armazenar e consultar referências técnicas relacionadas a zoneamento, legislação, fontes oficiais e padrões de análise.

Exemplos de itens:

```txt
- Referência de parâmetros para ZM-1
- Checklist de consulta no GeoSampa
- Fonte oficial do zoneamento de São Paulo
- Cuidados ao interpretar plano diretor
- Modelo de relatório de estudo de viabilidade
```

Um estudo de viabilidade pode:

- usar itens da Knowledge Base;
- gerar um item novo;
- vincular uma regra urbanística usada;
- registrar fonte oficial;
- gerar um relatório modelo.

Esse vínculo será importante para manter rastreabilidade.

---

## 22. Multi-tenancy e segurança

Todas as entidades do módulo devem respeitar `organizationId`.

Regras obrigatórias:

- nenhum item pode ser consultado sem filtro por organização;
- relações também precisam ter `organizationId`;
- anexos precisam pertencer à mesma organização;
- projetos vinculados precisam pertencer à mesma organização;
- templates vinculados precisam pertencer à mesma organização;
- permissões devem controlar criação, edição, publicação e arquivamento.

A Knowledge Base pode conter informações estratégicas da empresa. Por isso, isolamento por tenant é obrigatório.

---

## 23. Considerações sobre versionamento

No MVP, o versionamento formal de itens da Knowledge Base pode ser deixado para depois.

Porém, o design deve considerar que futuramente um item poderá ter versões.

Exemplo:

```txt
Modelo de Memorial Descritivo v1
Modelo de Memorial Descritivo v2
Modelo de Memorial Descritivo v3
```

Ou:

```txt
Checklist de Revisão de Orçamento - versão 2025
Checklist de Revisão de Orçamento - versão 2026
```

Para o MVP, campos como `updatedAt`, `updatedBy`, `status` e `deprecated` já ajudam.

No futuro, pode existir:

```txt
KnowledgeItemVersion
- id
- knowledgeItemId
- versionNumber
- contentSnapshot
- createdBy
- createdAt
- changeReason
```

---

## 24. Banco de dados conceitual

Tabelas iniciais recomendadas:

```txt
knowledge_items
knowledge_relations
knowledge_attachments
```

Tabelas futuras:

```txt
knowledge_usages
knowledge_item_versions
knowledge_embeddings
knowledge_comments
knowledge_approval_requests
```

### 24.1 knowledge_items

Campos sugeridos:

```txt
id
organization_id
title
description
type
status
visibility
tags
content
created_by
updated_by
published_at
archived_at
created_at
updated_at
```

`content` pode ser JSONB para permitir flexibilidade por tipo.

Exemplo:

```json
{
  "context": "Projetos de reforma escolar",
  "whenToUse": "Quando o projeto envolver reforma de unidade escolar existente",
  "recommendations": [
    "Validar acessibilidade antes de fechar orçamento",
    "Conferir cobertura antes da planilha final"
  ]
}
```

### 24.2 knowledge_relations

Campos sugeridos:

```txt
id
organization_id
knowledge_item_id
target_type
target_id
relation_type
created_by
created_at
```

### 24.3 knowledge_attachments

Campos sugeridos:

```txt
id
organization_id
knowledge_item_id
file_id
label
description
created_by
created_at
```

---

## 25. Regras de arquitetura

O módulo deve seguir Clean Architecture + DDD.

Regras obrigatórias:

- controller não contém regra de negócio;
- use case orquestra aplicação;
- entidade de domínio concentra comportamento e invariantes;
- TypeORM não deve ser usado como entidade de domínio;
- repositório deve ter interface na camada de domínio/aplicação;
- implementação TypeORM fica em infraestrutura;
- DTOs não devem vazar entidades de domínio diretamente;
- sempre validar `organizationId`;
- nunca criar CRUD genérico sem comportamento de domínio.

Exemplo de estrutura:

```txt
src/modules/knowledge-base/
  domain/
  application/
  infrastructure/
  presentation/
```

---

## 26. Linguagem do produto

A interface e os nomes do módulo devem usar linguagem próxima do negócio.

Evitar termos genéricos demais como:

```txt
Artigo
Post
Página
Nota
Item genérico
```

Preferir termos como:

```txt
Conhecimento
Referência
Padrão
Modelo
Lição aprendida
Checklist
Projeto de referência
Documento modelo
```

A experiência deve deixar claro que o usuário está criando um acervo técnico operacional, não uma wiki genérica.

---

## 27. Exemplo completo de item

### Item: Template de Reforma Escolar

```txt
Tipo: project_template
Status: published
Tags: reforma, escola, prefeitura, acessibilidade, orçamento
```

Descrição:

```txt
Template usado para projetos de reforma em escolas municipais, especialmente quando envolve adequação de acessibilidade, revisão de cobertura, atualização de memorial e orçamento.
```

Quando usar:

```txt
Usar quando o contrato envolver adequação, ampliação ou reforma de unidade escolar existente.
```

Entregáveis padrão:

```txt
- Levantamento técnico
- Projeto arquitetônico
- Memorial descritivo
- Orçamento
- Cronograma físico-financeiro
- Relatório fotográfico
- ART/RRT
```

Checklist de revisão:

```txt
- Conferir acessibilidade
- Conferir compatibilidade entre memorial e orçamento
- Conferir quantitativos de piso, pintura e cobertura
- Conferir prancha final em PDF
- Conferir assinatura do responsável técnico
```

Documentos modelo:

```txt
- Memorial padrão reforma escolar.docx
- Planilha orçamentária modelo.xlsx
- Relatório fotográfico modelo.docx
```

Projetos de referência:

```txt
- Reforma Escola Jardim Primavera
- Reforma EMEF Vila Aurora
```

Lições aprendidas:

```txt
- Sempre validar estado da cobertura antes de fechar orçamento.
- Fotos antigas devem ser vinculadas ao relatório inicial.
- Revisões de acessibilidade feitas tarde geram retrabalho no orçamento.
```

Esse exemplo mostra como um item da Knowledge Base pode conectar template, documentos, checklist, projetos antigos e lições aprendidas.

---

## 28. Critérios de sucesso do módulo

A Knowledge Base será bem-sucedida se conseguir:

- reduzir tempo para encontrar projetos antigos;
- reduzir retrabalho em projetos parecidos;
- facilitar padronização entre equipes;
- centralizar documentos modelo;
- preservar lições aprendidas;
- melhorar qualidade das revisões;
- ajudar novos colaboradores a entenderem como a empresa trabalha;
- transformar projetos finalizados em ativos reutilizáveis;
- criar base para IA futura;
- aumentar a percepção de valor da plataforma.

O objetivo não é apenas armazenar conhecimento.

O objetivo é fazer o conhecimento ser usado.

---

## 29. Resumo final

A Knowledge Base deve ser construída como o acervo técnico e operacional do tenant.

Ela deve armazenar:

- padrões técnicos;
- documentos modelo;
- projetos de referência;
- lições aprendidas;
- checklists de revisão;
- padrões de entrega;
- referências urbanísticas;
- vínculos com templates, projetos, entregáveis e documentos.

Ela deve permitir:

- criar conhecimento manualmente;
- publicar conhecimento oficial;
- arquivar conhecimento antigo;
- buscar referências;
- usar conhecimento em projetos;
- promover projetos finalizados para referência;
- criar uma memória organizacional reutilizável.

Sua essência é:

> Projetos geram conhecimento. Conhecimento gera projetos melhores.

Esse módulo é o que transforma a plataforma de um sistema de gestão de projetos em uma plataforma de inteligência operacional para empresas de engenharia.
