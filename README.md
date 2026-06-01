# 🍽️ TARKABOT — AI-Powered WhatsApp Restaurant Operating System (SaaS)

<div align="center">

[![Live Demo](https://img.shields.io/badge/🌐_Live_Demo-tarkabot.online-brightgreen?style=for-the-badge)](https://tarkabot.online)
[![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com)
[![React](https://img.shields.io/badge/React_18-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)](https://react.dev)
[![Supabase](https://img.shields.io/badge/Supabase_PostgreSQL-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white)](https://supabase.com)
[![DigitalOcean](https://img.shields.io/badge/DigitalOcean-0080FF?style=for-the-badge&logo=digitalocean&logoColor=white)](https://digitalocean.com)
[![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://docker.com)
[![WhatsApp](https://img.shields.io/badge/WhatsApp_Cloud_API-25D366?style=for-the-badge&logo=whatsapp&logoColor=white)](https://developers.facebook.com/docs/whatsapp)

</div>

TarkaBot is a production-grade, multi-tenant B2B SaaS built to automate restaurant operations in Pakistan. It intercepts orders directly from WhatsApp via natural language (Roman Urdu/English), processes them using a custom AI/NLP engine, and beams them in real-time to a digital Kitchen Display System (KDS) and POS dashboard.

🌐 **Live Production:** [tarkabot.online](https://tarkabot.online)

---

## 🎯 Engineering Highlights & Achievements

Built over 3 months, this project evolved from a simple chatbot into a highly secure, distributed Restaurant OS handling full order lifecycles.

- **Custom NLP Pipeline:** Developed a highly optimized, dual-layer AI parser. It uses `RapidFuzz` for lightning-fast tokenization and exact/fuzzy menu matching (≥60% confidence), drastically reducing LLM latency and costs. It gracefully falls back to a **DeepSeek AI LLM** for complex, multi-item, or ambiguous natural language queries.
- **True Multi-Tenancy:** Engineered strict data isolation using **PostgreSQL Row Level Security (RLS)** across 11 relational tables. Tenants cannot cross-pollinate data, even at the raw database query level.
- **Real-Time Distributed State:** Implemented **Supabase Realtime (WebSockets)** to instantly push confirmed WhatsApp orders to the React frontend (Kanban Kitchen Board) without manual polling, reducing database load.
- **Enterprise-Grade Webhook Security:** Meta Cloud API webhooks are secured using **HMAC-SHA256 signature verification**. Replay attacks and DDoS vectors are mitigated via a **Redis** cache layer deployed securely via Docker internal networks on a DigitalOcean Droplet.
- **POS & Thermal Printing:** Integrated `jsPDF` and `jspdf-autotable` to dynamically generate and print 80mm POS thermal receipts directly from the browser without dedicated driver installations.

---

## 🏗️ System Architecture

```text
┌─────────────────────────────────────────────────────────┐
│                    CUSTOMER (WhatsApp)                   │
└──────────────────────┬──────────────────────────────────┘
                       │ Meta Cloud API Webhook
                       ▼
┌─────────────────────────────────────────────────────────┐
│        DigitalOcean Droplet (Dockerized Backend)         │
│  ┌─────────────┐  ┌──────────────┐  ┌───────────────┐  │
│  │ Webhook API │  │  Roman Urdu  │  │   DeepSeek    │  │
│  │ HMAC-SHA256 │  │  RapidFuzz   │  │  AI Fallback  │  │
│  └─────────────┘  └──────────────┘  └───────────────┘  │
│  ┌─────────────┐  ┌──────────────┐                      │
│  │ Redis Cache │  │  Supabase    │                      │
│  │ Rate Limits │  │ REST Client  │                      │
│  │ Anti-Replay │  │              │                      │
│  └─────────────┘  └──────────────┘                      │
└──────────────────────┬──────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────┐
│              Supabase (PostgreSQL + Realtime)            │
│   11 tables · 33 migrations · Row Level Security (RLS)  │
│   RPC stored procedures · PostgreSQL triggers           │
└──────────────────────┬──────────────────────────────────┘
                       │ Supabase Realtime (WebSocket)
                       ▼
┌─────────────────────────────────────────────────────────┐
│              React 18 Dashboard (Vercel)                 │
│  Kitchen Kanban · POS Terminal · Sales Analytics        │
│  Dynamic PDF Receipts · Tenant Admin Console            │
└─────────────────────────────────────────────────────────┘
```

---

## 📸 Platform Interface

*Updated Production Screenshots Coming Soon!*

<div align="center">

| Landing Page | Dashboard |
|:---:|:---:|
| Coming Soon | Coming Soon |

| POS Terminal | Menu Catalog |
|:---:|:---:|
| Coming Soon | Coming Soon |

| Print Settings | Sales Report |
|:---:|:---:|
| Coming Soon | Coming Soon |

</div>

---

## 🛠️ Deep Dive: The Tech Stack

### 🚀 Backend Engine (Python / FastAPI)
- **Framework:** `FastAPI` + `Uvicorn` for high-throughput, async webhook processing.
- **NLP & AI:** `RapidFuzz` for rapid string matching, `DeepSeek API` for intelligent conversational fallback.
- **Security & Caching:** `Redis` (containerized, UFW secured) for request rate limiting and idempotency keys to prevent webhook replays.
- **Deployment:** Containerized via Docker (`docker-compose`) and hosted on a **DigitalOcean Droplet**.

### 💻 Frontend Application (React 18)
- **Framework:** React 18, fully strictly typed with **TypeScript 5.6**.
- **State Management:** `TanStack React Query v5` for server state caching and optimistic UI updates.
- **Styling:** `Tailwind CSS 3.4` + `Framer Motion 12` for fluid micro-interactions and dark/light mode architectures.
- **Realtime:** `@supabase/supabase-js` for WebSockets subscription to Postgres changes.
- **Deployment:** CI/CD pipeline integrated directly with **Vercel**.

### 🗄️ Database (Supabase PostgreSQL)
- **Schema:** 11 core tables (`tenants`, `orders`, `items`, `staff`, etc.) with strict foreign key constraints.
- **Security:** Extensive Row Level Security (RLS) policies mapping JWT claims to tenant IDs.
- **Performance:** B-Tree Indexes on high-cardinality columns (`tenant_id`, `created_at`, `phone`).
- **Atomic Operations:** Supabase RPC stored procedures handle multi-table transactions safely.

---

## 🔒 Security & Privacy Notice

> **Note:** TarkaBot is a closed-source commercial SaaS product operating in production. The proprietary source code, internal logic, API keys, and customer data are maintained in a secure private repository.
>
> This showcase repository exists strictly for architectural documentation, technical deep-dives, and portfolio demonstration for engineering roles.

---

## 👨‍💻 Engineering Lead

**Muhammad Ahsaan Ullah**  
*AI Automation & Full-Stack Engineer*  
Architecting and scaling production-ready systems for modern businesses.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=flat&logo=linkedin)](https://linkedin.com/in/mahsaanullah)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black?style=flat&logo=github)](https://github.com/MAhsaanUllah)

---

<div align="center">

**TarkaBot — Modernizing the Restaurant Industry, One WhatsApp Message at a Time. 🇵🇰**

</div>
