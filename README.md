# Acme Dashboard (Next.js App Router)

Aplicação full‑stack construída seguindo o tutorial oficial do Next.js (App Router). Ela simula o painel financeiro da Acme, com autenticação, tabela de faturas, formulários de criação/edição, gráficos e proteção de rotas – tudo usando os recursos modernos do App Router (server components, server actions, NextAuth, middleware etc.).

## Demo
![Gravação do painel](public/nextjs-dashboard-kkf1.vercel.app-Google-Chrome-2025-11-19-11-01-53.gif)

## Principais etapas do projeto
1. **Bootstrap do App Router** – iniciado o template oficial e configurado Tailwind, ícones e fontes utilizadas em todo o painel.
2. **Camada de dados** – criação das funções em `app/lib/data.ts` para consultar métricas, receitas e faturas a partir do Postgres (Neon/Vercel Postgres).
3. **Componentização do dashboard** – montagem de cards, tabela responsiva (`app/ui/invoices/table.tsx`), gráfico de receitas, busca paginada e botões de ação.
4. **CRUD com Server Actions** – formulários de criação/edição/deleção (`app/ui/invoices/*`) enviando dados diretamente para `app/lib/actions.ts`, com validação e revalidação automática do cache.
5. **Autenticação** – implementação do NextAuth com provider de credenciais (`auth.ts`), hashing via bcrypt, leitura de usuários no banco e formulário customizado em `app/login/page.tsx`.
6. **Proteção de rotas** – middleware (`middleware.ts`) conectado ao `authConfig` para redirecionar visitantes não autenticados para `/login` e impedir acesso indevido ao `/dashboard`.
7. **Deploy** – ajustes de variáveis de ambiente e publicação no Vercel, unindo front e back em um único projeto Next.js.

## Como rodar localmente
1. Instale dependências: `pnpm install` (ou `npm install`).
2. Defina as variáveis no `.env`:
   - `POSTGRES_URL` (ou `DATABASE_URL`) apontando para o Postgres com `sslmode=require`.
   - `AUTH_SECRET` gerado pelo `openssl rand -hex 32` (ou pelo utilitário do NextAuth).
   - Outras chaves públicas/privadas usadas pelo provedor de autenticação (por exemplo, `NEXT_PUBLIC_STACK_*`, `STACK_SECRET_SERVER_KEY`).
3. Execute `pnpm dev` e acesse `http://localhost:3000`.

## Tecnologias
- Next.js 14 (App Router, Server Components, Server Actions)
- NextAuth (middleware + credenciais customizadas)
- Postgres (Neon/Vercel Postgres) com o client `postgres`
- Tailwind CSS e Heroicons
- Vercel (deploy e variáveis de ambiente)

## Deploy no Vercel
- https://nextjs-dashboard-kkf1.vercel.app/

## Credenciais do app (Acessar)
- Email: user@nextmail.com
- Password: 123456


> Referência: [Next.js App Router Course](https://nextjs.org/learn). Este repositório serve como base/documentação do passo a passo realizado no curso.
