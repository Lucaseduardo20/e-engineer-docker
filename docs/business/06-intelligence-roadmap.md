# 06 — Roadmap de Inteligência

## 1. Objetivo deste documento

Este documento descreve como a plataforma deve evoluir de um MVP operacional para uma plataforma de inteligência técnica para empresas de engenharia.

A inteligência não precisa começar com IA generativa. Ela pode começar com regras simples, contexto, recomendações por tags, alertas e relações entre módulos.

A ideia central é:

> Antes de usar IA, a plataforma precisa organizar bem os dados, o contexto e o conhecimento do tenant.

## 2. Situação atual

A plataforma já possui módulos operacionais:

- dashboard;
- projetos;
- entregáveis;
- documentos;
- versões;
- revisões;
- organização;
- colaboradores;
- base de conhecimento inicial.

Ainda assim, a experiência pode parecer uma gerenciadora de projetos. Para se diferenciar, a plataforma deve passar a ajudar ativamente o usuário a tomar decisões, encontrar referências, evitar erros e reutilizar conhecimento.

## 3. Princípio de inteligência do produto

Inteligência significa o sistema ajudar o usuário a perceber algo que ele talvez não veria sozinho.

Exemplos:

- este projeto possui entregáveis bloqueados;
- este documento não possui versão oficial;
- esta revisão está atrasada;
- existe um projeto antigo parecido;
- existe um checklist aplicável;
- esta reprovação parece uma lição aprendida;
- este projeto está sem template;
- este orçamento tem histórico de divergência em projetos parecidos;
- este tipo de projeto exige documentos recorrentes.

## 4. Fase 1 — Inteligência contextual simples

Essa fase não precisa de IA.

### 4.1 Alertas no projeto

Exibir alertas como:

- entregáveis atrasados;
- documentos sem versão oficial;
- revisões pendentes;
- entregáveis bloqueados;
- projeto sem responsável;
- projeto sem template;
- projeto sem itens de conhecimento vinculados.

Exemplo:

```text
Atenção: este projeto possui 2 entregáveis bloqueados e 1 documento sem versão oficial.
```

### 4.2 Saúde técnica do projeto

Criar indicador:

- Boa;
- Atenção;
- Crítica.

Critérios:

- atraso;
- bloqueio;
- revisão vencida;
- ausência de versão oficial;
- ausência de responsável;
- ausência de template;
- reprovações recentes.

O sistema deve mostrar o motivo do score.

### 4.3 Recomendações por tags

Se projeto tem tags, recomendar KnowledgeItems com tags similares.

Exemplo:

```text
Projeto com tags: UBS, saúde, prefeitura

Recomendações:
- Template de UBS
- Checklist de revisão de UBS
- Projeto de referência UBS Vila Esperança
```

### 4.4 Sugestões pós-evento

Após eventos relevantes, sugerir ações.

Exemplos:

- revisão reprovada → criar lição aprendida;
- documento oficial → salvar como modelo;
- projeto concluído → promover como referência;
- novo projeto → aplicar template;
- entregável sem documento → criar documento.

## 5. Fase 2 — Base de Conhecimento operacional

A Base de Conhecimento passa a influenciar o fluxo.

### 5.1 Knowledge no projeto

Na tela do projeto, mostrar:

- itens vinculados;
- itens recomendados;
- projetos de referência;
- documentos modelo;
- padrões aplicáveis;
- lições aprendidas relacionadas.

### 5.2 Knowledge no entregável

No entregável, mostrar:

- documentos modelo daquele tipo;
- checklists de revisão;
- padrões técnicos;
- lições aprendidas.

### 5.3 Knowledge no documento

No documento, mostrar:

- modelos relacionados;
- versões oficiais anteriores;
- histórico de reprovações;
- padrões de nomenclatura;
- checklists.

## 6. Fase 3 — Templates inteligentes

Templates devem deixar de ser apenas listas fixas e passar a ser recomendados.

### 6.1 Recomendação de templates

Baseada em:

- tipo de projeto;
- tags;
- cliente;
- cidade;
- histórico da organização;
- itens da Base de Conhecimento.

### 6.2 Aplicação enriquecida

Ao aplicar template, o sistema pode:

- criar entregáveis;
- sugerir documentos modelo;
- vincular checklists;
- recomendar revisores;
- indicar projetos de referência.

## 7. Fase 4 — Estudos de Viabilidade Urbanística

Esse módulo pode ser um grande diferencial comercial.

### 7.1 Objetivo

Permitir que o usuário inicie um projeto com uma análise preliminar do endereço/lote.

### 7.2 Fluxo ideal

```text
Endereço/SQL/IPTU/coordenada
→ localização geográfica
→ consulta de zoneamento
→ regras urbanísticas
→ relatório preliminar
→ criação de projeto técnico
→ aplicação de template
→ recomendações da Base de Conhecimento
```

### 7.3 Dados esperados

- endereço;
- coordenadas;
- zona;
- macrozona;
- parâmetros urbanísticos;
- fontes oficiais;
- data da consulta;
- alertas;
- relatório.

### 7.4 Cuidados

- sempre preservar fonte;
- mostrar data de consulta;
- avisar que é apoio técnico;
- permitir validação manual;
- evitar resposta sem rastreabilidade.

## 8. Fase 5 — Busca semântica

Com a Base de Conhecimento estruturada, entra busca semântica.

### 8.1 Casos de uso

Usuário pergunta:

> Temos algum projeto parecido com UBS em terreno pequeno?

> Qual checklist usamos para orçamento de pavimentação?

> Quais erros já ocorreram em reforma escolar?

> Existe modelo de memorial para drenagem?

### 8.2 Arquitetura conceitual

```text
KnowledgeItem
→ chunks de conteúdo
→ embeddings
→ busca vetorial
→ resposta com fontes internas
```

### 8.3 Regras

- resposta deve citar itens usados;
- não inventar conhecimento;
- respeitar tenant;
- não misturar dados entre organizações;
- diferenciar item publicado de rascunho.

## 9. Fase 6 — Assistente técnico do tenant

Após busca semântica, pode existir um assistente interno.

### 9.1 Funções possíveis

- encontrar projetos parecidos;
- resumir histórico de um projeto;
- sugerir entregáveis;
- sugerir checklist;
- comparar documentos;
- apontar pendências;
- gerar rascunho de relatório;
- sugerir lições aprendidas.

### 9.2 Limites

O assistente deve ser apoio, não autoridade técnica final.

Sempre deve mostrar fontes, contexto e permitir validação profissional.

## 10. Fase 7 — Inteligência de operação

Com dados suficientes, o sistema pode identificar padrões:

- tipos de projeto que mais atrasam;
- entregáveis mais reprovados;
- responsáveis mais sobrecarregados;
- documentos mais refeitos;
- templates mais usados;
- knowledge items mais úteis;
- causas recorrentes de bloqueio.

Isso pode alimentar dashboards executivos.

## 11. Roadmap sugerido de implementação

### Etapa 1 — Agora

- Base de Conhecimento funcional;
- relações com projetos;
- criar/editar/publicar/arquivar;
- tags;
- listagem e detalhe.

### Etapa 2

- promover projeto para referência;
- salvar documento oficial como modelo;
- criar lição aprendida a partir de revisão.

### Etapa 3

- recomendações por tags;
- knowledge recomendada no projeto;
- knowledge recomendada no entregável;
- knowledge recomendada no documento.

### Etapa 4

- saúde técnica do projeto;
- alertas contextuais no dashboard;
- motivos da saúde.

### Etapa 5

- estudo de viabilidade mockado;
- fluxo endereço → relatório fake realista → projeto;
- validação com Leo/Rafael.

### Etapa 6

- integração real com dados oficiais;
- PostGIS;
- importadores;
- fontes e relatórios.

### Etapa 7

- busca semântica;
- embeddings;
- assistente técnico.

## 12. O que não fazer agora

Não começar por:

- IA generativa complexa;
- scraping frágil;
- robô de navegador;
- ERP financeiro;
- compras;
- estoque;
- BIM;
- suporte a todas as cidades;
- automações avançadas sem dados.

O foco deve ser:

```text
Organizar bem o domínio
→ conectar operação com conhecimento
→ criar recomendações simples
→ validar valor
→ só então automatizar com IA/dados externos
```

## 13. Definição de plataforma inteligente

A plataforma será considerada inteligente quando conseguir:

- recomendar conhecimento no contexto certo;
- alertar riscos técnicos;
- reduzir erro de versão;
- sugerir reaproveitamento;
- capturar aprendizado automaticamente;
- gerar novos projetos mais padronizados;
- transformar histórico em vantagem operacional.

## 14. Frase norteadora

> Inteligência não é o sistema responder bonito. Inteligência é o sistema fazer a empresa repetir menos erro e reaproveitar melhor o que já sabe.
