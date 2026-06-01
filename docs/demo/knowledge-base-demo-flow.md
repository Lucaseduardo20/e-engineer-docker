# Demo Flow — Knowledge Base

## Usuario e organizacao
- Usuario: `admin@engflow.local`
- Senha: `123123lucas`
- Organizacao: `Engenharia Horizonte Ltda`

## Preparar ambiente
No backend:

```bash
cd /home/lkt/work/e_engineer/e-engineer-backend
npm run db:seed
npm run start:dev
```

No frontend:

```bash
cd /home/lkt/work/e_engineer/e-engineer-frontend
npm run dev
```

## Historia da demo (5-8 minutos)
1. Abrir Dashboard e mostrar que a organizacao tem projetos tecnicos ativos e historico operacional.
2. Abrir projeto `Construcao da UBS Vila Esperanca`.
3. Mostrar a secao de conhecimento aplicado no projeto (padrao tecnico, checklist, licao aprendida, padrao de entrega).
4. Abrir item `Divergencia de quantitativos em orcamento de UBS`.
5. Mostrar origem da licao (revisao reprovada) e relacao com projeto.
6. Abrir Base de Conhecimento e filtrar por tipo `document_model`.
7. Abrir item `Memorial descritivo para reforma escolar`.
8. Mostrar origem em documento tecnico real.
9. Abrir item `Reforma da Escola Municipal Jardim Primavera`.
10. Mostrar que projeto finalizado virou referencia oficial.

## Itens-chave esperados na Base de Conhecimento
- `project_reference`: Reforma da Escola Municipal Jardim Primavera
- `project_reference`: Construcao da UBS Vila Esperanca
- `document_model`: Memorial descritivo para reforma escolar
- `lesson_learned`: Divergencia de quantitativos em orcamento de UBS
- `review_checklist`: Revisao de orcamento antes de envio ao cliente
- `technical_standard`: Organizacao de disciplinas em projetos de UBS
- `delivery_standard`: Pacote tecnico para prefeitura

## Mensagem de negocio para fechar a demo
`Projetos geram conhecimento. Conhecimento melhora novos projetos.`

