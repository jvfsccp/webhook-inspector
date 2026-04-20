# Webhook Inspector

Projeto full stack para captura e inspeção de webhooks.

## Tecnologias

- Monorepo com `pnpm workspaces`
- API: `Node.js`, `TypeScript`, `Fastify`, `Zod`, `Drizzle ORM`, `PostgreSQL`, `Swagger/Scalar`
- Web: `React`, `TypeScript`, `Vite`
- Infra local: `Docker Compose` (PostgreSQL)

## Estrutura

- `api/`: backend e banco de dados
- `web/`: frontend

## Pré-requisitos

- `Node.js` (recomendado: 20+)
- `pnpm` (recomendado: 10+)
- `Docker` e `Docker Compose`

## Instalação

1. Instale dependências do monorepo:

```bash
pnpm install
```

2. Suba o banco PostgreSQL:

```bash
cd api
docker compose up -d
```

3. Confira o arquivo de ambiente da API (`api/.env`):

```env
DATABASE_URL="postgresql://docker:docker@localhost:5432/webhooks"
```

4. Execute as migrações do banco:

```bash
pnpm --filter api db:migrate
```

## Como usar

### 1) Rodar a API (porta 3333)

```bash
pnpm --filter api dev
```

- API: `http://localhost:3333`
- Documentação: `http://localhost:3333/docs`

### 2) Rodar o Web (porta padrão do Vite)

Em outro terminal:

```bash
pnpm --filter web dev
```

- Web: normalmente em `http://localhost:5173`

### 3) Endpoint disponível

- `GET /api/webhooks?limit=20`

Exemplo:

```bash
curl "http://localhost:3333/api/webhooks?limit=20"
```

## Scripts úteis

### API

- `pnpm --filter api dev`: inicia API em modo desenvolvimento
- `pnpm --filter api db:generate`: gera arquivos de migração
- `pnpm --filter api db:migrate`: aplica migrações
- `pnpm --filter api db:studio`: abre Drizzle Studio

### Web

- `pnpm --filter web dev`: inicia frontend
- `pnpm --filter web build`: gera build de produção
- `pnpm --filter web preview`: serve build localmente

## Observações

- Para parar o banco:

```bash
cd api
docker compose down
```
