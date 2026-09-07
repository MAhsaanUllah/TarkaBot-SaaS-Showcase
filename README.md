<div align="center">
  <img src="assets/Title.png" alt="TarkaBot Banner" width="100%" />
  <h1>TarkaBot</h1>
  <p><strong>WhatsApp-Native AI Restaurant Operating System</strong></p>
  <p>AI ordering, kitchen workflow, and restaurant operations in one platform.</p>
  <p>
    <a href="https://tarkabot.online">Live Product</a> ·
    <a href="https://tarkabot.online/demo">Demo</a> ·
    <a href="https://tarkabot.online/help">Setup Guide</a>
  </p>
</div>

<p align="center">
  <img src="https://img.shields.io/badge/React-18-61DAFB?logo=react&logoColor=black" alt="React" />
  <img src="https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript&logoColor=white" alt="TypeScript" />
  <img src="https://img.shields.io/badge/Supabase-PostgreSQL-3ECF8E?logo=supabase&logoColor=white" alt="Supabase" />
  <img src="https://img.shields.io/badge/FastAPI-Python-3776AB?logo=python&logoColor=white" alt="FastAPI" />
  <img src="https://img.shields.io/badge/Status-Private%20Beta-orange" alt="Private Beta" />
</p>

## Product

TarkaBot helps restaurants turn WhatsApp into an ordering and operations channel. The product combines a restaurant-specific AI waiter, menu and delivery settings, kitchen order visibility, POS-style dashboard workflows, customer tracking, and notifications in a multi-tenant SaaS product.

## How it works

```text
Customer WhatsApp message
        ↓
Evolution API → Supabase WhatsApp webhook
        ↓                         ↓
DeepSeek restaurant persona   PostgreSQL + RLS
        ↓                         ↓
WhatsApp reply ← menu, offers, settings, and orders
                                  ↓
                       React dashboard and kitchen workflow
```

## Restaurant AI waiter

Each restaurant configures its own name, address, phone, timings, delivery areas, charges, minimum order, menu, deals, payment methods, and assistant persona. The AI uses that context to answer customers, guide them through an order, collect name, phone, delivery address, and payment method, and confirm the order before saving it.

## Product capabilities

- WhatsApp menu browsing and restaurant information.
- AI-guided order taking with delivery and payment questions.
- Restaurant catalog, categories, offers, inventory, and settings.
- Dashboard, POS-style order management, and kitchen display workflow.
- Order status updates and customer tracking links.
- Evolution API connection and webhook processing.
- DeepSeek-powered restaurant persona with server-side API secrets.
- Gmail transactional notifications through an email outbox with retries.
- Super-admin controls for tenants, plans, beta access, and manual payment status.

## Engineering showcase

- React, TypeScript, Vite, Tailwind CSS, responsive UI, and accessible navigation.
- Supabase Auth, PostgreSQL, Row Level Security, tenant isolation, SQL migrations, realtime data, and Edge Functions.
- Deno/TypeScript serverless functions for WhatsApp webhooks and notifications.
- FastAPI/Python services with JWT validation, tenant authorization, structured errors, and rate limiting.
- External API integration with Evolution API, DeepSeek, and Gmail API.
- Deployment across Vercel, Supabase, Render, and GitHub.

## Security and reliability

- Tenant-aware PostgreSQL access with RLS.
- Bearer-token validation for Evolution webhook callbacks.
- Restricted CORS, security headers, and Content Security Policy.
- Server-side secrets and generic public error responses.
- Trial/subscription guards, message limits, order tracking, and notification retries.
- Anonymous access to private demo orders and tenant data removed.

## Beta status

TarkaBot is currently in private beta with a seven-day trial. Manual bank-transfer payment is being used while automated payment gateway integration is prepared. Testimonials and results are presented as beta feedback until independently verified.

## Recruiter context

This project demonstrates end-to-end product engineering by a recent graduate: turning a business problem into a working SaaS workflow, designing the customer experience, building tenant-aware data models, integrating external APIs, and deploying frontend, backend, database, and serverless services.

The core production flow is:

**WhatsApp message → AI restaurant response → validated order → kitchen dashboard → customer status notification.**

No API keys, OAuth refresh tokens, or production secrets belong in this repository.

## Public links

- [Live product](https://tarkabot.online)
- [Privacy](https://tarkabot.online/privacy)
- [Terms](https://tarkabot.online/terms)
- [Help and setup](https://tarkabot.online/help)
- [Security](https://tarkabot.online/security)

## Local development

```bash
npm install
npm run dev
```

Configure server-side secrets only through Supabase, Render, or Vercel environment settings.

<div align="center">**TarkaBot — Modernizing the Restaurant Industry, One WhatsApp Message at a Time. 🇵🇰**</div>
