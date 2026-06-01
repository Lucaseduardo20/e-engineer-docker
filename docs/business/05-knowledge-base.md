# 05 — Base de Conhecimento

## 1. Visão geral

A Base de Conhecimento é um dos módulos mais estratégicos da plataforma. Ela não deve ser tratada como uma wiki genérica, uma pasta de arquivos ou um repositório passivo de documentos. Ela deve ser o acervo técnico vivo do tenant.

Sua função é capturar, organizar, publicar e reutilizar o conhecimento operacional da empresa de engenharia.

A Base de Conhecimento deve guardar:

- padrões técnicos;
- documentos modelo;
- projetos de referência;
- checklists de revisão;
- padrões de entrega;
- lições aprendidas;
- erros recorrentes;
- boas práticas internas;
- referências urbanísticas;
- templates e estruturas reutilizáveis;
- observações específicas de clientes, prefeituras ou tipos de projeto.

A frase que resume o módulo é:

> A Base de Conhecimento é o cérebro técnico do tenant.

## 2. Problema que o módulo resolve

Empresas de engenharia frequentemente dependem da memória dos colaboradores para saber:

- qual projeto antigo usar como base;
- qual memorial já foi aprovado antes;
- qual checklist aplicar;
- qual padrão de nome seguir;
- quais documentos são obrigatórios;
- que erro não pode se repetir;
- qual tipo de projeto exige quais entregáveis;
- que revisão costuma reprovar;
- qual planilha ou relatório usar como modelo.

Isso cria riscos:

- retrabalho;
- perda de tempo;
- erro de versão;
- falta de padronização;
- inconsistência entre equipes;
- dependência de pessoas específicas;
- perda de conhecimento quando alguém sai da empresa;
- dificuldade para treinar novos colaboradores;
- repetição de erros técnicos.

A Base de Conhecimento resolve isso transformando histórico técnico em ativo reutilizável.

## 3. O que a Base de Conhecimento não deve ser

Ela não deve ser:

- uma wiki genérica;
- uma pasta de arquivos;
- um Notion simplificado;
- uma lista solta de artigos;
- um repositório desconectado da operação;
- um lugar onde documentos são jogados sem contexto.

O diferencial é a conexão com os projetos.

Um item de conhecimento deve poder se relacionar com:

- projetos;
- entregáveis;
- documentos;
- versões oficiais;
- revisões;
- templates;
- estudos de viabilidade;
- tags e tipos de projeto.

## 4. Conceito principal: KnowledgeItem

O `KnowledgeItem` representa qualquer conhecimento reutilizável da organização.

Campos conceituais:

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
- metadata.

Todo item pertence a uma organização. Conhecimento é, por padrão, interno ao tenant.

## 5. Tipos de KnowledgeItem

## 5.1 Padrão técnico

Representa uma regra ou orientação interna sobre como a empresa faz determinada coisa.

Exemplos:

- padrão de nomenclatura de arquivos;
- padrão de revisão de projeto arquitetônico;
- padrão para memorial descritivo;
- padrão de organização por disciplina;
- padrão de cálculo de quantitativos;
- padrão de entrega para prefeitura;
- padrão de prancha final.

Pergunta que responde:

> Como fazemos isso aqui dentro?

## 5.2 Documento modelo

Representa um documento reutilizável como ponto de partida.

Exemplos:

- modelo de memorial descritivo;
- modelo de relatório técnico;
- modelo de relatório fotográfico;
- modelo de cronograma físico-financeiro;
- modelo de planilha orçamentária;
- modelo de checklist de fiscalização;
- modelo de termo de entrega.

Pergunta que responde:

> Qual arquivo usamos como base?

## 5.3 Projeto de referência

Representa um projeto antigo que foi considerado útil para novos projetos.

Exemplos:

- UBS Vila Esperança 2024;
- Reforma Escola Jardim Primavera;
- Pavimentação Rua das Acácias;
- Revitalização Praça Central.

Importante: nem todo projeto antigo deve virar referência automaticamente. O ideal é existir um fluxo de promoção.

Pergunta que responde:

> Que projeto parecido já fizemos?

## 5.4 Lição aprendida

Representa um aprendizado vindo de erro, revisão, atraso, retrabalho ou decisão importante.

Exemplos:

- em reformas escolares, sempre validar acessibilidade antes do orçamento;
- em pavimentação, revisar drenagem antes de fechar quantitativos;
- em UBS, compatibilizar hidráulica e arquitetura antes da revisão final;
- orçamento apresentou divergência entre memorial e planilha;
- prefeitura X costuma exigir documento complementar.

Pergunta que responde:

> Que erro já cometemos e não queremos repetir?

## 5.5 Checklist de revisão

Representa uma lista de validações para revisar um entregável ou documento.

Exemplos:

- checklist de revisão de orçamento;
- checklist de revisão de projeto arquitetônico;
- checklist de compatibilização;
- checklist de entrega final para prefeitura;
- checklist de relatório fotográfico.

Pergunta que responde:

> O que precisa ser conferido antes de aprovar?

## 5.6 Padrão de entrega

Representa orientações para entrega final de um pacote técnico.

Exemplos:

- padrão de entrega para prefeitura;
- padrão de pacote de documentos;
- estrutura de pastas final;
- nomenclatura de arquivos finais;
- formatos aceitos.

Pergunta que responde:

> Como entregamos isso corretamente?

## 5.7 Referência urbanística

Tipo futuro para apoiar o módulo de viabilidade.

Exemplos:

- regras de zoneamento recorrentes;
- observações sobre ZM, ZEU, ZEIS;
- interpretação de parâmetros;
- links oficiais;
- anotações sobre consulta no GeoSampa/SISZON.

Pergunta que responde:

> Que regra ou fonte urbanística usamos neste contexto?

## 6. Status do KnowledgeItem

Status recomendados:

## Draft

Item em rascunho. Ainda não deve ser recomendado automaticamente.

## Published

Item oficial da organização. Pode aparecer em buscas, recomendações e uso em projetos.

## Archived

Item arquivado. Mantido para histórico, mas não recomendado.

## Deprecated

Item depreciado. Ainda visível, mas com aviso de que não deve ser usado como padrão atual.

## 7. Relações do conhecimento

Um item de conhecimento pode se relacionar com várias entidades.

### KnowledgeRelation

Campos conceituais:

- id;
- organizationId;
- knowledgeItemId;
- targetType;
- targetId;
- relationType;
- createdBy;
- createdAt.

Target types possíveis:

- project;
- deliverable;
- document;
- document_version;
- review;
- template;
- feasibility_study.

Relation types possíveis:

- generated_from;
- used_in;
- reference_for;
- model_for;
- standard_for;
- lesson_from;
- recommended_for.

## 8. Attachments

KnowledgeItem pode ter anexos.

Exemplos:

- arquivo modelo;
- PDF de referência;
- planilha;
- imagem;
- relatório;
- prancha;
- documento oficial.

Esses anexos devem ser tratados como metadados/documentos, não como arquivos soltos.

## 9. Tags

Tags são fundamentais para busca e recomendação.

Exemplos:

- UBS;
- escola;
- reforma;
- pavimentação;
- drenagem;
- orçamento;
- memorial;
- acessibilidade;
- prefeitura-sp;
- projeto-arquitetônico;
- relatório-fotográfico;
- quantitativos;
- revisão;
- urbanismo.

No MVP, tags podem ser array de strings. Futuramente, podem virar entidade própria.

## 10. Fluxo — Criar item manualmente

```text
1. Usuário acessa Base de Conhecimento.
2. Clica em Novo item.
3. Escolhe tipo.
4. Preenche título.
5. Preenche descrição.
6. Adiciona conteúdo estruturado.
7. Adiciona tags.
8. Vincula projetos/documentos/templates, se necessário.
9. Salva como rascunho ou publica.
```

## 11. Fluxo — Promover projeto para referência

```text
1. Usuário acessa projeto.
2. Clica em Adicionar à Base de Conhecimento.
3. Sistema cria item do tipo Projeto de referência.
4. Pré-preenche dados do projeto.
5. Usuário seleciona entregáveis úteis.
6. Usuário seleciona documentos reutilizáveis.
7. Usuário adiciona lições aprendidas.
8. Usuário adiciona tags.
9. Usuário publica ou salva como rascunho.
```

Esse é um dos fluxos mais importantes da plataforma.

## 12. Fluxo — Salvar documento oficial como modelo

```text
1. Usuário acessa documento oficial.
2. Clica em Salvar como modelo.
3. Sistema cria KnowledgeItem do tipo Documento modelo.
4. Vincula versão oficial.
5. Usuário adiciona descrição, quando usar e tags.
6. Usuário publica.
```

## 13. Fluxo — Registrar lição aprendida a partir de revisão

```text
1. Uma revisão é reprovada.
2. Sistema pergunta se deseja registrar lição aprendida.
3. Usuário confirma.
4. Sistema cria rascunho com contexto da revisão.
5. Usuário descreve problema, impacto e recomendação.
6. Usuário publica.
```

## 14. Fluxo — Usar item em projeto

```text
1. Usuário acessa projeto.
2. Sistema recomenda itens relacionados.
3. Usuário abre item.
4. Clica em Usar neste projeto.
5. Sistema cria relação KnowledgeUsage.
6. Se for documento modelo, permite criar documento a partir dele.
7. Se for checklist, aplica checklist.
8. Se for projeto de referência, vincula como referência.
```

## 15. Recomendações iniciais sem IA

No MVP, recomendações podem ser baseadas em:

- tags do projeto;
- tipo do projeto;
- tipo do entregável;
- cliente/prefeitura;
- documento em revisão;
- histórico de uso.

Exemplo:

```text
Projeto: Construção da UBS Vila Esperança
Tags: UBS, saúde, prefeitura

Recomendações:
- Template de UBS
- Checklist de revisão para UBS
- Projeto de referência UBS 2024
- Documento modelo de memorial descritivo para UBS
```

## 16. Busca

A busca inicial deve permitir:

- busca por título;
- busca por descrição;
- filtro por tipo;
- filtro por status;
- filtro por tags;
- filtro por projeto relacionado;
- filtro por autor;
- filtro por data.

Futuro:

- busca semântica;
- embeddings;
- perguntas em linguagem natural;
- respostas com fontes internas.

## 17. Tela de listagem

A listagem deve mostrar:

- título;
- tipo;
- status;
- tags;
- descrição curta;
- última atualização;
- criado por;
- quantidade de usos;
- projetos relacionados.

Empty state deve explicar valor:

> Sua Base de Conhecimento ainda está vazia. Comece criando um padrão técnico, documento modelo, lição aprendida ou promova um projeto finalizado como referência.

## 18. Tela de detalhe

Deve conter:

- título;
- tipo;
- status;
- descrição;
- conteúdo;
- tags;
- quando usar;
- quando não usar;
- arquivos vinculados;
- projetos relacionados;
- documentos relacionados;
- histórico;
- ações.

Ações:

- editar;
- publicar;
- arquivar;
- depreciar;
- usar em projeto;
- duplicar;
- vincular documento;
- vincular projeto.

## 19. Como a Base de Conhecimento torna o produto inteligente

A inteligência inicial não precisa vir de IA. Ela pode vir de contexto.

Exemplos:

- recomendar padrão com base no tipo do projeto;
- sugerir documento modelo para entregável;
- sugerir lição aprendida após reprovação;
- sugerir projeto de referência na criação de projeto;
- alertar quando projeto não tem conhecimento vinculado;
- mostrar itens mais usados pela equipe;
- mostrar itens depreciados.

## 20. Roadmap da Knowledge Base

### Fase 1 — CRUD estruturado

- criar item;
- editar item;
- publicar;
- arquivar;
- listar;
- detalhar;
- filtrar;
- tags.

### Fase 2 — Relações

- vincular a projeto;
- vincular a documento;
- vincular a versão oficial;
- vincular a entregável;
- registrar uso.

### Fase 3 — Geração a partir da operação

- promover projeto;
- salvar documento oficial como modelo;
- criar lição aprendida a partir de revisão;
- criar checklist a partir de padrão.

### Fase 4 — Recomendações

- recomendações por tags;
- recomendações por tipo;
- recomendações no projeto;
- recomendações no entregável;
- recomendações no documento.

### Fase 5 — IA/Busca semântica

- embeddings;
- busca por similaridade;
- chat interno do tenant;
- respostas com fontes;
- sugestões automáticas de conhecimento.

## 21. Regra de ouro

A Base de Conhecimento só tem valor se for usada no fluxo real.

Ela deve sempre se conectar com:

```text
Projeto → Documento → Revisão → Aprendizado → Conhecimento → Novo Projeto
```

Se ela virar apenas um local de cadastro manual, perderá força.

## Estado implementado (pos-epico)

Implementado no codigo:
- CRUD funcional orientado a fluxo: criar/listar/buscar/detalhar/editar/publicar/arquivar/depreciar.
- Relacoes de conhecimento com projeto e fluxos derivados.
- Fluxos derivados: promover projeto, salvar documento como modelo, registrar revisao como licao aprendida.
- Auditoria de eventos integrada.
- Permissoes minimas com enforcement backend e tratamento visual no frontend.

Referencia tecnica detalhada:
- `docs/modules/knowledge-base.md`
- `docs/modules/knowledge-base-api.md`
- `docs/modules/knowledge-base-permissions.md`
- `docs/modules/knowledge-base-test-scenarios.md`
