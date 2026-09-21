# NewsPulse

Aplicação full stack para publicação e consumo de notícias com categorias personalizadas e notificações push web.

## Funcionalidades

- cadastro e login de usuários;
- autenticação com JWT em cookie HTTP-only;
- seleção de categorias de interesse;
- feed de notícias filtrado por preferências;
- notificações push no navegador;
- publicação de notícias via CLI administrativa.

## Arquitetura

- **frontend**: Vue 3 + Vite
- **backend**: Node.js + Express + MongoDB
- **persistência**: MongoDB
- **notificações**: Web Push + Service Worker

Documentação detalhada: [`docs/DOCUMENTACAO.md`](./docs/DOCUMENTACAO.md)

## Pré-requisitos

- Node.js 18+
- npm
- Docker e Docker Compose

## Configuração

### 1) Banco de dados (MongoDB)

Na raiz do projeto:

```bash
docker compose up -d
```

Isso inicia:

- MongoDB em `localhost:27017`
- mongo-express em `localhost:8081`

### 2) Variáveis de ambiente (backend)

Crie/ajuste `backend/.env` com:

```env
DB_HOST=localhost
DB_USER=<seu_usuario_mongo>
DB_PASS=<sua_senha_mongo>
DB_NAME=<nome_do_banco>
DB_PORT=27017

SERVER_PORT=4000
NODE_ENV=development

DB_TOKEN_SECRET=<seu_token_secret>

VAPID_PUBLIC_KEY=<sua_vapid_public_key>
VAPID_PRIVATE_KEY=<sua_vapid_private_key>
MAILTO=mailto:seu-email@dominio.com

ADMIN_SECRET=<segredo_admin>
```

## Instalação

### Backend

```bash
cd /home/runner/work/WebDev-Node-T3/WebDev-Node-T3/backend
npm install
```

### Frontend

```bash
cd /home/runner/work/WebDev-Node-T3/WebDev-Node-T3/frontend
npm install
```

### Admin CLI

```bash
cd /home/runner/work/WebDev-Node-T3/WebDev-Node-T3/admin-cli
npm install
```

## Execução

### Subir backend

```bash
cd /home/runner/work/WebDev-Node-T3/WebDev-Node-T3/backend
node app.js
```

### Subir frontend (desenvolvimento)

```bash
cd /home/runner/work/WebDev-Node-T3/WebDev-Node-T3/frontend
npm run dev
```

Frontend em: `http://localhost:5173`  
Backend em: `http://localhost:4000`

## Publicação de notícias via CLI

Com backend em execução:

```bash
cd /home/runner/work/WebDev-Node-T3/WebDev-Node-T3/admin-cli
node index.js tecnologia "Novo processador lançado" "Tecnologia em alta"
```

Formato:

```bash
node index.js <categoria> <conteudo> [titulo_opcional]
```

Categorias válidas:

- tecnologia
- saude
- negocios
- natureza
- politica

## Rotas principais da API

- `POST /api/auth/signup`
- `POST /api/auth/login`
- `GET /api/auth/logoff`
- `PUT /api/user/preferences`
- `POST /api/news/publish`
- `GET /api/news`

## Melhorias sugeridas

- adicionar suíte de testes automatizados;
- remover segredos hardcoded no frontend e externalizar configuração;
- padronizar scripts (`start`, `dev`, `test`) para backend e CLI;
- incluir `.env.example` para setup seguro.
