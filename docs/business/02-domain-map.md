# 02 — Mapa de Domínio

## 1. Objetivo deste documento

Este documento descreve os principais conceitos de negócio da plataforma, suas responsabilidades, relações e papel dentro da visão do produto.

A intenção é evitar que a plataforma seja modelada como um CRUD genérico. O domínio precisa falar a linguagem da engenharia: projeto técnico, entregável, documento, versão oficial, revisão, padrão, referência, lição aprendida e estudo de viabilidade.

Este mapa deve orientar implementação, criação de tarefas, desenho de telas, APIs, entidades, casos de uso e documentação futura.

## 2. Visão geral do domínio

A plataforma é um SaaS B2B multi-tenant. Cada tenant representa uma organização, normalmente uma empresa de engenharia, arquitetura ou consultoria técnica.

O domínio pode ser resumido assim:

```text
Organization
→ Users/Memberships
→ Projects
→ Deliverables
→ Documents
→ DocumentVersions
→ Reviews
→ ActivityLogs
→ KnowledgeBase
→ FeasibilityStudies (futuro)
```

A entidade central operacional é o **Project**.

A entidade central de padronização e inteligência é o **KnowledgeItem**.

A entidade central de controle documental é o **DocumentVersion**.

A entidade central de qualidade técnica é o **Review**.

## 3. Bounded Contexts recomendados

### 3.1 Identity & Access

Responsável por autenticação, usuários, acesso, papéis, permissões e sessões.

Conceitos:

- User;
- AuthSession;
- Credentials;
- Role;
- Permission.

Responsabilidades:

- login;
- geração e validação de JWT;
- identificação do usuário atual;
- proteção de rotas;
- controle de acesso por papel.

### 3.2 Organizations

Responsável pelo tenant.

Conceitos:

- Organization;
- Membership;
- OrganizationRole;
- OrganizationProfile;
- OperationalPriority.

Responsabilidades:

- gerenciar empresa ativa;
- controlar colaboradores;
- definir papéis;
- manter isolamento multi-tenant;
- centralizar configuração da organização.

### 3.3 Projects

Responsável pela carteira técnica de projetos.

Conceitos:

- Project;
- ProjectStatus;
- ProjectType;
- ProjectProgress;
- ProjectTeam;
- ProjectTag;
- ProjectClient.

Responsabilidades:

- criar projeto técnico;
- acompanhar status e progresso;
- vincular responsáveis;
- organizar entregáveis;
- conectar documentos, revisões e conhecimento;
- futuramente nascer a partir de estudo de viabilidade.

### 3.4 Deliverables

Responsável por tudo que precisa ser produzido, validado e entregue dentro do projeto.

Conceitos:

- Deliverable;
- DeliverableStatus;
- DeliverableType;
- DeliverableDeadline;
- DeliverableResponsible;
- DeliverableBlockReason.

Responsabilidades:

- controlar pacote técnico;
- organizar produção;
- relacionar documentos;
- indicar pendências;
- servir de ponte entre projeto, documento e revisão.

### 3.5 Documents & Versions

Responsável por documentos técnicos, arquivos, versões e versão oficial.

Conceitos:

- Document;
- DocumentVersion;
- FileMetadata;
- OfficialVersion;
- DocumentStatus;
- RevisionCode.

Responsabilidades:

- armazenar metadados dos documentos;
- controlar versões;
- marcar versão oficial;
- relacionar documento a projeto e entregável;
- manter rastreabilidade documental.

### 3.6 Reviews

Responsável por decisões técnicas, aprovação, reprovação e pendências.

Conceitos:

- Review;
- ReviewStatus;
- ReviewDecision;
- ReviewComment;
- Reviewer;
- ReviewTarget.

Responsabilidades:

- solicitar revisão;
- aprovar;
- reprovar;
- registrar motivo;
- vincular decisão a documento, versão, entregável ou projeto;
- gerar aprendizado futuro.

### 3.7 Knowledge Base

Responsável pelo acervo técnico reutilizável da organização.

Conceitos:

- KnowledgeItem;
- KnowledgeItemType;
- KnowledgeItemStatus;
- KnowledgeRelation;
- KnowledgeAttachment;
- KnowledgeUsage;
- KnowledgeTag.

Responsabilidades:

- registrar padrões técnicos;
- registrar documentos modelo;
- promover projetos como referência;
- registrar lições aprendidas;
- vincular conhecimento a projetos;
- recomendar conhecimento por contexto;
- criar base para inteligência futura.

### 3.8 Activity/Audit

Responsável por histórico operacional.

Conceitos:

- ActivityLog;
- Actor;
- Target;
- ActionType;
- OccurredAt.

Responsabilidades:

- registrar eventos relevantes;
- alimentar dashboard;
- dar rastreabilidade;
- permitir auditoria.

### 3.9 Urban Feasibility (futuro)

Responsável por estudos de viabilidade urbanística.

Conceitos:

- FeasibilityStudy;
- Address;
- GeoCoordinate;
- UrbanZone;
- ZoningRule;
- UrbanParameter;
- SourceReference;
- FeasibilityReport.

Responsabilidades:

- consultar dados urbanísticos;
- gerar estudo preliminar;
- salvar fonte e data;
- criar projeto técnico a partir do estudo;
- conectar viabilidade com entregáveis e documentos.

## 4. Entidades principais

## 4.1 Organization

Representa uma empresa de engenharia dentro da plataforma.

A organização é o tenant. Todos os dados de negócio devem pertencer a uma organização.

Atributos típicos:

- id;
- name;
- legalName;
- slug;
- status;
- createdAt;
- updatedAt.

Relações:

- possui usuários via Membership;
- possui projetos;
- possui documentos;
- possui revisões;
- possui base de conhecimento;
- possui configurações.

Regras:

- toda entidade de negócio deve respeitar organizationId;
- usuários só podem acessar dados da organização atual;
- troca de tenant deve alterar todo o contexto da aplicação.

## 4.2 User

Representa uma pessoa que acessa a plataforma.

Atributos típicos:

- id;
- name;
- email;
- passwordHash;
- avatar;
- status;
- createdAt;
- updatedAt.

Relações:

- pode pertencer a várias organizações;
- possui uma ou mais Memberships;
- pode criar projetos, documentos, revisões e itens de conhecimento.

## 4.3 Membership

Representa a relação entre User e Organization.

Atributos típicos:

- id;
- organizationId;
- userId;
- role;
- status;
- joinedAt.

Papéis iniciais:

- owner;
- admin;
- coordinator;
- engineer;
- designer;
- viewer.

Regras:

- apenas membros ativos acessam a organização;
- permissões devem ser derivadas do papel;
- publicar conhecimento pode exigir papel de coordinator/admin/owner.

## 4.4 Project

Representa um projeto técnico de engenharia.

Exemplos:

- Construção da UBS Vila Esperança;
- Reforma da Escola Municipal Jardim Primavera;
- Projeto de Pavimentação da Rua das Acácias;
- Sistema de Drenagem do Bairro São Lucas;
- Revitalização da Praça Central.

Atributos típicos:

- id;
- organizationId;
- name;
- clientName;
- type;
- status;
- progress;
- responsibleId;
- description;
- tags;
- deadline;
- createdAt;
- updatedAt.

Relações:

- pertence a uma Organization;
- possui Deliverables;
- possui Documents;
- possui Reviews;
- possui ActivityLogs;
- pode usar KnowledgeItems;
- pode ser promovido para KnowledgeItem;
- futuramente pode nascer de FeasibilityStudy.

Status possíveis:

- draft;
- active;
- planning;
- in_progress;
- in_review;
- waiting_approval;
- blocked;
- overdue;
- completed;
- archived.

Regras:

- projeto deve ter organizationId;
- projeto deve ter nome;
- projeto deve ter status;
- progresso pode ser calculado a partir dos entregáveis;
- projeto concluído pode ser promovido para referência.

## 4.5 Deliverable

Representa um item técnico que precisa ser produzido.

Exemplos:

- Projeto arquitetônico;
- Projeto estrutural;
- Projeto elétrico;
- Projeto hidráulico;
- Memorial descritivo;
- Orçamento;
- Cronograma físico-financeiro;
- ART/RRT;
- Relatório fotográfico;
- Cálculo de materiais.

Atributos típicos:

- id;
- organizationId;
- projectId;
- title;
- description;
- type;
- status;
- responsibleId;
- dueDate;
- order;
- createdAt;
- updatedAt.

Relações:

- pertence a um Project;
- possui Documents;
- pode ter Reviews;
- pode ser gerado por Template;
- pode usar KnowledgeItems.

Status possíveis:

- to_produce;
- in_production;
- blocked;
- completed;
- pending_review;
- approved;
- rejected;
- overdue.

Regras:

- entregável precisa pertencer a um projeto;
- entregável deve ter responsável idealmente;
- entregável bloqueado deve possuir motivo;
- entregável concluído idealmente deve possuir documento oficial ou revisão aprovada.

## 4.6 Document

Representa um documento técnico dentro do projeto.

Atributos típicos:

- id;
- organizationId;
- projectId;
- deliverableId;
- title;
- description;
- type;
- status;
- createdBy;
- createdAt;
- updatedAt.

Tipos comuns:

- memorial_descritivo;
- projeto_arquitetonico;
- projeto_estrutural;
- projeto_eletrico;
- projeto_hidraulico;
- orcamento;
- cronograma;
- art_rrt;
- relatorio_tecnico;
- relatorio_fotografico;
- calculo_materiais;
- estudo_viabilidade.

Status possíveis:

- draft;
- under_review;
- official;
- rejected;
- archived.

Regras:

- documento deve pertencer a uma organização;
- documento deve pertencer a um projeto;
- documento deve possuir pelo menos uma versão para ser útil;
- status oficial deve estar ligado a uma versão oficial.

## 4.7 DocumentVersion

Representa uma versão específica de um documento.

Atributos típicos:

- id;
- organizationId;
- documentId;
- revisionCode;
- fileName;
- filePath;
- fileSize;
- mimeType;
- uploadedBy;
- uploadedAt;
- notes;
- isOfficial;
- status.

Exemplos de revisionCode:

- R00;
- R01;
- R02;
- V1;
- V2.

Regras:

- documento pode ter várias versões;
- idealmente apenas uma versão oficial por documento;
- ao marcar nova versão como oficial, a versão anterior deixa de ser oficial;
- versão oficial deve ter rastreabilidade de quem marcou e quando;
- versão pode estar vinculada a revisão.

## 4.8 Review

Representa uma revisão técnica.

Atributos típicos:

- id;
- organizationId;
- projectId;
- deliverableId nullable;
- documentId nullable;
- documentVersionId nullable;
- title;
- description;
- reviewerId;
- requestedBy;
- status;
- decision;
- dueDate;
- decidedAt;
- decisionComment;
- createdAt;
- updatedAt.

Status possíveis:

- pending;
- approved;
- rejected;
- overdue;
- canceled.

Regras:

- revisão precisa ter alvo claro;
- revisão pode aprovar ou reprovar;
- reprovação deve possuir comentário/motivo;
- revisão reprovada pode sugerir criação de lição aprendida;
- revisão aprovada pode permitir marcar documento como oficial.

## 4.9 KnowledgeItem

Representa um item reutilizável da base de conhecimento da organização.

Tipos recomendados:

- technical_standard;
- document_model;
- project_reference;
- lesson_learned;
- review_checklist;
- delivery_standard;
- zoning_rule_reference;
- project_template_reference.

Atributos típicos:

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
- archivedAt.

Status possíveis:

- draft;
- published;
- archived;
- deprecated.

Relações:

- pode se vincular a Projects;
- pode se vincular a Documents;
- pode se vincular a DocumentVersions;
- pode se vincular a Templates;
- pode se vincular a Deliverables;
- pode registrar usos.

## 4.10 ActivityLog

Representa um evento relevante ocorrido no sistema.

Exemplos:

- projeto criado;
- template aplicado;
- documento enviado;
- nova versão marcada como oficial;
- revisão solicitada;
- revisão aprovada;
- revisão reprovada;
- item de conhecimento publicado;
- projeto promovido como referência.

Atributos típicos:

- id;
- organizationId;
- actorId;
- action;
- targetType;
- targetId;
- metadata;
- occurredAt.

## 5. Relações centrais

```text
Organization 1:N Project
Organization 1:N KnowledgeItem
Organization 1:N Membership
Project 1:N Deliverable
Project 1:N Document
Deliverable 1:N Document
Document 1:N DocumentVersion
Project 1:N Review
DocumentVersion 1:N Review
Project N:N KnowledgeItem
KnowledgeItem N:N Document
KnowledgeItem N:N ProjectTemplate
Project 1:N ActivityLog
```

## 6. Modelo mental do produto

A plataforma deve ser modelada em torno destes eixos:

### Operação

Projetos, entregáveis, documentos, revisões.

### Rastreabilidade

Versões, histórico, eventos, decisões.

### Padronização

Templates, padrões, checklists, documentos modelo.

### Reutilização

Base de conhecimento, projetos de referência, lições aprendidas.

### Inteligência futura

Recomendações, estudos de viabilidade, busca semântica, alertas, saúde técnica.

## 7. Diretriz de modelagem

Sempre que surgir uma nova feature, ela deve ser encaixada no domínio correto.

Exemplos:

- “subir arquivo” pertence a Documents;
- “marcar versão oficial” pertence a DocumentVersion;
- “aprovar orçamento” pertence a Reviews;
- “criar padrão de orçamento” pertence a Knowledge Base;
- “gerar entregáveis a partir de modelo” pertence a Templates;
- “indicar projeto antigo como base” pertence a Knowledge Base/Projects;
- “calcular regras do endereço” pertence a Urban Feasibility.

Evitar entidades genéricas como Task, Card, Board e List como centro do produto. Elas podem existir como abstrações auxiliares, mas a linguagem principal deve ser a do domínio de engenharia.
