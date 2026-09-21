# Documentação do Projeto

## Visão geral

Este projeto implementa uma plataforma de notícias com:

- autenticação de usuários;
- feed personalizado por categorias;
- envio de notificações push web;
- ferramenta de linha de comando para publicação de notícias (admin-cli).

Stack principal:

- **Frontend**: Vue 3 + Vite + Vue Router
- **Backend**: Node.js + Express + MongoDB + JWT + Web Push
- **Banco**: MongoDB (via Docker Compose)

---

## Estrutura do repositório

```text
WebDev-Node-T3/
├── admin-cli/                 # CLI para publicar notícias
├── backend/                   # API, autenticação e notificações
│   ├── app.js
│   └── src/
│       ├── api/
│       │   ├── controllers/
│       │   ├── middleware/
│       │   └── routes/
│       ├── config/
│       └── models/
├── frontend/                  # Aplicação Vue
│   ├── public/sw.js
│   └── src/
│       ├── router/
│       ├── services/
│       └── views/
└── docker-compose.yaml        # MongoDB + mongo-express
```

---

## Fluxo funcional

1. Usuário cria conta e faz login.
2. Backend gera JWT e salva em cookie HTTP-only.
3. No feed, usuário escolhe categorias de interesse.
4. Frontend registra Service Worker e inscrição de push.
5. Preferências e inscrição são salvas no backend.
6. Admin publica notícia por categoria via `admin-cli`.
7. Backend salva a notícia e envia push para usuários inscritos naquela categoria.
8. Usuário recebe notificação e acessa o feed filtrado.

---

## Categorias suportadas

- tecnologia
- saude
- negocios
- natureza
- politica

---

## Variáveis de ambiente (backend)

Configurar em `backend/.env`:

- `DB_HOST`
- `DB_USER`
- `DB_PASS`
- `DB_NAME`
- `DB_PORT`
- `SERVER_PORT`
- `NODE_ENV`
- `DB_TOKEN_SECRET`
- `VAPID_PUBLIC_KEY`
- `VAPID_PRIVATE_KEY`
- `MAILTO`
- `ADMIN_SECRET`

> Recomendação: use chaves e segredos próprios em cada ambiente.

---

## Rotas da API

### Autenticação

- `POST /api/auth/signup`  
  Cria usuário.
- `POST /api/auth/login`  
  Faz login e define cookie `token`.
- `GET /api/auth/logoff`  
  Remove cookie de sessão (rota protegida).

### Usuário

- `PUT /api/user/preferences`  
  Salva categorias e subscription de push (rota protegida).

### Notícias

- `POST /api/news/publish`  
  Publica notícia (protegida por header `x-admin-secret`).
- `GET /api/news`  
  Lista notícias conforme categorias do usuário (rota protegida).

---

## Service Worker e Push

- Arquivo: `frontend/public/sw.js`
- Eventos implementados:
  - `install`
  - `activate`
  - `push` (exibição de notificação)
  - `notificationclick` (abre URL da notificação)

---

## Observações técnicas

- O backend também serve o frontend buildado em `frontend/dist`.
- O CORS está configurado para `http://localhost:5173`.
- Não há suíte de testes automatizados configurada no projeto atualmente.
