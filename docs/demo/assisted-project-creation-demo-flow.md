# Demo Flow — Criacao assistida de projeto

## Credenciais

- URL frontend: `http://localhost:5173`
- Usuario: `admin@engflow.local`
- Senha: `123123lucas`
- Tenant: `Engenharia Horizonte Ltda`

## Preparacao

Backend:

```bash
cd /home/lkt/work/e_engineer/e-engineer-backend
npm run db:migration:run
npm run db:seed
npm run start:dev
```

Frontend:

```bash
cd /home/lkt/work/e_engineer/e-engineer-frontend
npm run dev
```

## Narrativa recomendada

### 1. Abrir novo projeto

Ir para `/projects` e clicar em `Novo projeto`.

Criar:

- Nome: `Nova UBS Jardim Aurora`
- Tipo tecnico: `unidade de saude`

### 2. Selecionar tags governadas

Selecionar:

- `UBS`
- `Prefeitura SP`
- `Orgao publico`
- `Obra publica`
- `Projeto basico`

Mensagem para a demo:

> A plataforma entende o contexto tecnico antes de criar a estrutura.

### 3. Ver sugestoes

Resultado esperado:

- `Construcao da UBS Vila Esperanca` aparece como projeto base forte.
- A UI mostra `Aderencia N`.
- A reforma escolar pode aparecer como contraste, mas deve ter menor aderencia quando as tags de UBS sao selecionadas.

### 4. Usar como base

Selecionar `Construcao da UBS Vila Esperanca`.

Revisar entregaveis herdados:

- Projeto arquitetonico
- Projeto estrutural
- Projeto eletrico
- Projeto hidraulico
- Memorial descritivo
- Orcamento
- Cronograma fisico-financeiro
- ART/RRT

Confirmar criacao.

### 5. Cockpit pos-criacao

Resultado esperado:

- Redirecionamento para `/projects/:id`.
- Contexto tecnico mostra tags como UBS, Prefeitura SP, Obra publica.
- Banner de revisao de entregaveis herdados aparece.
- Entregaveis herdados podem ser marcados como revisados.
- Recomendacoes contextuais aparecem com:
  - `Forca N`
  - tags combinadas
  - motivo (`reason`)
  - acao `Aplicar ao projeto`

### 6. Aplicar conhecimento

Aplicar uma recomendacao, por exemplo:

- `Revisao de orcamento antes de envio ao cliente`
- `Organizacao de disciplinas em projetos de UBS`

Resultado esperado:

- Item passa a aparecer como aplicado.
- Cockpit continua mostrando o contexto tecnico.

## Dados demo envolvidos

Projetos:

- `Construcao da UBS Vila Esperanca`
- `Reforma da Escola Municipal Jardim Primavera`
- `Projeto de Pavimentacao da Rua das Acacias`

KnowledgeItems:

- `Construcao da UBS Vila Esperanca`
- `Organizacao de disciplinas em projetos de UBS`
- `Divergencia de quantitativos em orcamento de UBS`
- `Revisao de orcamento antes de envio ao cliente`
- `Memorial descritivo para reforma escolar`

## Frase de fechamento

> A e-engineer nao comeca um projeto do zero. Ela comeca com a inteligencia acumulada da empresa.
