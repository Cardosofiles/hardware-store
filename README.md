<div align="center">

# 🛒 Hardware Store — E-commerce Full Stack

**Plataforma de e-commerce de hardware construída com Next.js 16, React 19 e TypeScript.**
Catálogo, carrinho persistente, checkout autenticado e e-mails transacionais — pronta para produção.

[![Acessar Demo](https://img.shields.io/badge/▶_Acessar_Demo-Online-22c55e?style=for-the-badge)](https://e.commerce.cardosofiles.com.br/)
&nbsp;
[![Portfólio](https://img.shields.io/badge/Portfólio-cardosofiles.com.br-0ea5e9?style=for-the-badge)](https://www.cardosofiles.com.br/)
&nbsp;
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Conectar-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/Cardosofiles)

<br/>

![Next.js](https://img.shields.io/badge/Next.js_16-000000?style=flat&logo=nextdotjs&logoColor=white)
![React](https://img.shields.io/badge/React_19-20232A?style=flat&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_4-06B6D4?style=flat&logo=tailwindcss&logoColor=white)
![Prisma](https://img.shields.io/badge/Prisma_7-2D3748?style=flat&logo=prisma&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat&logo=postgresql&logoColor=white)
![Zustand](https://img.shields.io/badge/Zustand-443e38?style=flat)
![React Query](https://img.shields.io/badge/React_Query-FF4154?style=flat&logo=reactquery&logoColor=white)

</div>

---

> **TL;DR para recrutadores** — Aplicação full stack real, em produção, que demonstra domínio de **React 19 / Next.js 16 (App Router)**, **TypeScript** ponta a ponta, autenticação OAuth + verificação de e-mail, modelagem de dados relacional e padrões de arquitetura escaláveis. Não é um CRUD de tutorial: tem fluxo de compra completo, sincronização de carrinho cliente↔servidor e e-mails transacionais.

## 🔗 Links rápidos

|                         |                                                                |
| ----------------------- | -------------------------------------------------------------- |
| 🌐 **Demo em produção** | **https://e.commerce.cardosofiles.com.br/**                    |
| 💼 **Autor**            | João Batista Cardoso Miranda — Desenvolvedor Web React/Next.js |
| 📍 **Localização**      | Uberlândia, MG — Brasil (aberto a remoto)                      |
| 🧑‍💻 **GitHub**           | [@Cardosofiles](https://github.com/Cardosofiles)               |

---

## 🎯 O que este projeto resolve

Uma loja de hardware completa do ponto de vista do usuário e do negócio:

- **Descoberta de produtos** — catálogo com categorias hierárquicas, marcas, busca por slug e produtos em destaque, indexados no banco para performance.
- **Compra sem fricção** — carrinho persistente que sobrevive ao reload e **sincroniza com o servidor** quando o usuário autentica, evitando perda de itens entre dispositivos.
- **Checkout confiável** — fluxo autenticado com validação de endereço de entrega, criação de pedido transacional e **e-mail de confirmação** disparado automaticamente.
- **Confiança e prova social** — sistema de avaliações (rating + reviews verificadas) e perfil de usuário com dados de entrega reutilizáveis.
- **Conta segura** — login com **GitHub e Google OAuth**, registro com **verificação de e-mail** e recuperação/redefinição de senha.

## ✨ Principais funcionalidades

- 🔐 **Autenticação completa** — OAuth (GitHub/Google), verificação de e-mail, forgot/reset password via Better Auth
- 🛍️ **Catálogo de produtos** — categorias, marcas, destaque e página de detalhe com **Intercepting Routes** (modal sem perder a rota)
- 🛒 **Carrinho híbrido** — estado global com Zustand + `persist`, sincronizado com o banco para usuários logados
- 💳 **Checkout & Pedidos** — validação, criação de `Order`/`OrderItem` e status de pedido (`PENDING → DELIVERED`)
- ⭐ **Avaliações** — reviews com nota de 1 a 5 e selo de compra verificada
- 👤 **Dashboard do usuário** — perfil, endereço e histórico
- ✉️ **E-mails transacionais** — confirmação de pedido e verificação via Postmark
- 🌗 **Dark mode** e UI acessível com shadcn/ui + Radix
- 🧪 **Testes E2E** com Playwright

## 🏗️ Arquitetura & decisões técnicas

```
React Query (hooks)  →  Axios  →  Next.js API Routes  →  Prisma  →  PostgreSQL (Neon)
       ↑
   Zustand (carrinho, client state)
```

- **App Router (Next.js 16)** com **Route Groups** (`(auth)/`) e **Parallel + Intercepting Routes** (`@modal/`) para abrir o detalhe do produto como modal preservando a URL compartilhável.
- **Separação de estado**: React Query para _server state_ (cache, revalidação) e Zustand para _client state_ (carrinho) — cada ferramenta no seu papel.
- **Arquitetura por features** (`src/features/`) e camadas explícitas (`lib/`, `hooks/`, `stores/`, `components/`) para escalar sem virar espaguete.
- **TypeScript + Zod** validando da fronteira da API até os formulários (React Hook Form), eliminando classes inteiras de bugs em runtime.
- **Prisma 7** com adapter `pg`, índices estratégicos (`slug`, `categoryId`, `brand`, `featured`) e modelagem relacional limpa (User, Product, Order, Review, Cart, Profile).
- **React Compiler** habilitado para otimização automática de re-renderizações.

### 📁 Estrutura

```
src/
├── app/                 # App Router: páginas, layouts, API routes
│   ├── (auth)/          # Route group de autenticação
│   ├── products/@modal/ # Intercepting route (modal de produto)
│   ├── api/             # Endpoints: products, checkout, user, auth
│   └── dashboard/
├── features/            # Módulos por domínio (auth, ...)
├── components/          # UI (shadcn), cart, products, orders, profile
├── hooks/               # React Query hooks
├── stores/              # Zustand (cart-store)
├── lib/                 # auth, prisma, axios, validations (Zod)
└── emails/              # Templates transacionais (Postmark)
```

## 🧰 Stack técnica

| Camada             | Tecnologias                                                                                 |
| ------------------ | ------------------------------------------------------------------------------------------- |
| **Linguagem**      | TypeScript                                                                                  |
| **Front-end**      | React 19, Next.js 16 (App Router), Tailwind CSS 4, shadcn/ui, Radix UI, Motion, next-themes |
| **Estado & Dados** | TanStack React Query, Zustand, Axios                                                        |
| **Formulários**    | React Hook Form + Zod                                                                       |
| **Back-end**       | Next.js API Routes, Better Auth, Prisma 7                                                   |
| **Banco**          | PostgreSQL (Neon)                                                                           |
| **E-mail**         | Postmark                                                                                    |
| **Qualidade**      | ESLint, Prettier, Playwright (E2E)                                                          |

## 🔒 Acesso ao código-fonte

> O repositório oficial é **privado** — este README é a vitrine pública do projeto.

O código está fechado por se tratar de uma aplicação real em produção. Mas você não precisa do código para avaliar o trabalho:

- ▶️ **Veja funcionando agora** — explore a aplicação completa em produção:
  **[e.commerce.cardosofiles.com.br](https://e.commerce.cardosofiles.com.br/)**
- 🧑‍💻 **Recrutador ou tech lead?** Posso fazer um **code walkthrough** ao vivo (arquitetura, decisões técnicas e trechos do código) ou liberar acesso ao repositório mediante contato.
- 🌐 **Conheça meu portfólio** — outros projetos e formas de contato:
  **[cardosofiles.com.br](https://www.cardosofiles.com.br/)**

<div align="center">

[![Solicitar acesso / Walkthrough](https://img.shields.io/badge/📩_Solicitar_acesso_ao_código-Falar_comigo-22c55e?style=for-the-badge)](https://www.cardosofiles.com.br/pt/contact)

</div>

## 🧑‍💼 Sobre o autor

**João Batista Cardoso Miranda** — Desenvolvedor Web focado em **React, Next.js e TypeScript**, com olhar de produto (background em marketing) e atenção a **UX, Core Web Vitals e SEO**.

- 🌐 Portfólio: [cardosofiles.com.br](https://www.cardosofiles.com.br/)
- 💼 LinkedIn: [in/Cardosofiles](https://www.linkedin.com/in/Cardosofiles)
- 🐙 GitHub: [@Cardosofiles](https://github.com/Cardosofiles)

> 💬 Aberto a oportunidades como **Desenvolvedor Web / Front-end Engineer (React.js)** — presencial em Uberlândia/MG ou remoto.

<div align="center">

⭐ **Se este projeto te ajudou ou te interessou, deixe uma estrela!**

</div>
