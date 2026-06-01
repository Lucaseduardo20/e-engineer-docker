# Dashboard

O Dashboard agora usa Vuetify no frontend e endpoints REST tenant-aware no backend.

## Como rodar

Stack completa via Docker Compose:

```bash
docker-compose up --build
```

O compose de desenvolvimento:

- espera o PostgreSQL ficar saudavel;
- roda migrations;
- roda seed idempotente;
- sobe o backend em watch mode;
- sobe o frontend em `http://localhost:5173`.

Backend local sem compose:

```bash
cd e-engineer-backend
npm run docker:up
npm run db:fresh
npm run start:dev
```

Frontend:

```bash
cd e-engineer-frontend
source ~/.nvm/nvm.sh
nvm use 22
npm run dev
```

Credencial local do seed:

```txt
Email: admin@engflow.local
Senha: 123456
```

Se quiser resetar tudo do zero:

```bash
docker-compose down -v
docker-compose up --build
```

## Funcionalidades

- AppShell responsivo com Vuetify, sidebar, topbar, seletor de organizacao e menu de usuario.
- Dashboard com indicadores, lista de projetos, eventos de auditoria, revisoes pendentes, busca de base de conhecimento e usuarios da equipe.
- Listagem `/projects` consumindo `GET /projects`.
- Detalhe `/projects/:id` consumindo projeto e entregaveis.
- Cliente API fortemente tipado em `src/shared/http/api-client.ts`.
- Stores Pinia para auth, projects e UI.

## Swagger

A documentacao Swagger fica em:

```txt
http://localhost:3000/docs/api
```

## Observacoes

O backend registra auditoria em `activity_logs` quando um projeto e criado via `POST /projects`. Os endpoints de atualizacao/exclusao ainda devem seguir o mesmo padrao quando forem expandidos.
