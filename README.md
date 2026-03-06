# Projeto Fullstack com Prisma ORM

![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=node.js&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=flat&logo=typescript&logoColor=white)
![Prisma](https://img.shields.io/badge/Prisma-2D3748?style=flat&logo=prisma&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=flat&logo=postgresql&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=flat&logo=express&logoColor=white)

## Visão Geral do Projeto

Este projeto é um template fullstack desenvolvido para praticar os conceitos do **Prisma ORM** em um ambiente Node.js. Ele demonstra operações CRUD básicas para usuários e perguntas, incluindo relacionamentos de banco de dados, seeding e desenvolvimento de APIs. O foco está em aprender a integração do Prisma com PostgreSQL, roteamento Express e TypeScript, destacando habilidades em ORM, APIs REST e desenvolvimento backend.

## Tecnologias

- **Node.js**: Ambiente de execução para o servidor.
- **TypeScript**: Desenvolvimento com tipagem segura, com aliases de caminho (`@/*` mapeados para `./src/*`).
- **Prisma**: ORM para gerenciamento de banco de dados, incluindo definição de schema, migrações e geração de cliente. Usa PostgreSQL como provedor.
- **Express**: Framework web para construção da API REST, com middleware para parsing JSON e tratamento de erros assíncronos.

## Pré-requisitos

- Node.js (versão 18 ou superior)
- npm ou yarn
- PostgreSQL instalado e rodando
- Variável de ambiente `DATABASE_URL` configurada (ex.: `postgresql://user:password@localhost:5432/dbname`)

## Instalação

Clone o repositório e instale as dependências:

```bash
npm install
```

## Configuração do Banco

1. Execute as migrações para criar as tabelas:

```bash
npx prisma migrate dev
```

2. Execute o seeding para popular o banco com dados de exemplo:

```bash
npx prisma db seed
```

3. Gere o cliente Prisma (se necessário):

```bash
npx prisma generate
```

## Executando a Aplicação

Para rodar em modo desenvolvimento:

```bash
npm run dev
```

O servidor iniciará em `http://localhost:3333` e logará consultas do Prisma.

## Endpoints da API

### Usuários

- `GET /users`: Lista todos os usuários.
- `POST /users`: Cria um usuário (corpo: `{ "name": "string", "email": "string" }`).
- `GET /users/:id`: Busca um usuário por ID.

### Perguntas

- `GET /questions`: Lista perguntas (parâmetro opcional `title` para filtro insensível a maiúsculas, ordenado por título).
- `POST /questions`: Cria uma pergunta (corpo: `{ "title": "string", "content": "string", "userId": "uuid" }`).
- `PUT /questions/:id`: Atualiza uma pergunta (corpo: `{ "title": "string", "content": "string" }`).
- `DELETE /questions/:id`: Deleta uma pergunta por ID.

## Testando com Insomnia

Para testar as rotas, exporte o arquivo `routes-insomnia.json` para dentro do Insomnia. Ele contém uma coleção pré-configurada com todas as requisições para usuários e perguntas, permitindo testar operações CRUD diretamente contra o servidor em execução.

## Estrutura do Projeto

```
src/
├── controllers/
│   ├── questions-controller.ts
│   └── users-controller.ts
├── routes/
│   ├── index.ts
│   ├── questions-routes.ts
│   └── users-routes.ts
├── prisma.ts
└── server.ts
prisma/
├── schema.prisma
├── seed.ts
└── migrations/
```

## Visão Geral do Schema

- **Provedor**: PostgreSQL.
- **Modelos**:
  - `User`: Campos `id` (UUID, chave primária), `name` (string), `email` (string, único). Relação um-para-muitos com `Question`.
  - `Question`: Campos `id` (UUID, chave primária), `title` (string), `content` (string), `createdAt`/`updatedAt` (timestamps), `userId` (chave estrangeira para `User`). Pertence a `User`.
- **Relações**: Usuários podem ter múltiplas perguntas; perguntas estão vinculadas a um usuário.
