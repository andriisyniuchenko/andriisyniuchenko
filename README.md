# Andrii Syniuchenko

Former CS teacher from Ukraine, now based in Seattle building backend systems. Regional chess champion — quit while ahead. Rollerblader. Undefeated — hills excluded. The worst tennis player you'll ever meet, but I still show up. TIME Person of the Year, 2006.

---

## Tech Stack

**Languages:** Python  
**Frameworks:** FastAPI · Django  
**Databases:** PostgreSQL · Redis · OpenSearch · MongoDB  
**Infrastructure:** Docker · Docker Compose · GitHub Actions · Linux  
**Tools & Patterns:** SQLAlchemy · Alembic · Celery · JWT · REST API · OpenAPI · httpx · Pydantic v2  
**AI / LLM:** LangChain · LangGraph · Ollama · RAG · OpenAI · Anthropic · Google · Groq

---

## Projects

### Auto Dealer Ecosystem

Two independently deployable services that communicate over HTTP. Built as a system, not two separate tutorials.

```
┌──────────────────────────────┐        ┌──────────────────────────────┐
│  Customer-facing Website     │        │  Auto Dealer CRM             │
│  auto-dealer-conversation-   │  HTTP  │  auto_dealer_crm             │
│  service · localhost:8001    │──POST──▶  localhost:8000              │
│                              │  Key   │                              │
│  Inventory browsing + chat   │        │  Internal lead & deal mgmt   │
└──────────────────────────────┘        └──────────────────────────────┘
```

---

#### [Auto Dealer CRM](https://github.com/andriisyniuchenko/auto_dealer_crm)
> FastAPI · PostgreSQL · SQLAlchemy · Alembic · JWT · Pydantic v2 · Docker · GitHub Actions · pytest

Most CRMs are cluttered with features nobody uses. This one isn't. Built to model how a real dealership sales team actually operates — lead intake, deal tracking, role-based access — without the noise.

- Role-based access control with per-role lead and deal visibility
- Lead assignment, shared ownership with 50/50 deal credit split, stale lead detection
- Full lead timeline: notes, calls, appointments, deal history
- JWT auth: cookie-based sessions for web UI, Bearer token for API
- Public lead intake API secured with `X-API-Key` — used by the conversation service
- 48 pytest tests across 4 modules; GitHub Actions CI on every push

📹 [Watch demo](https://youtu.be/8uaZtSdtifc)

---

#### [Auto Dealer Conversation Service](https://github.com/andriisyniuchenko/auto-dealer-conversation-service)
> FastAPI · PostgreSQL · SQLAlchemy async · asyncpg · LangGraph · LangChain · OpenSearch · Ollama · Docker

This is the kind of project that doesn't write itself. Not CRUD — actual engineering: state machines, hybrid search pipelines, streaming, an AI agent that has to behave reliably in production.

The first version used a single large prompt to handle everything. It worked most of the time. Most of the time isn't good enough when you're capturing sales leads. The current version moves all business logic into a deterministic LangGraph graph — the LLM handles conversation, Python handles everything else.

- AI assistant (Jessica) answers inventory questions, collects contact details, and books test drives
- Hybrid OpenSearch search: semantic KNN + BM25 keyword, 40/60 weighted
- SSE streaming — responses appear token by token in the browser
- LLM provider swappable via env vars — no code changes needed
- 52 pytest tests: 37 covering agent routing logic, 15 covering API and inventory
- Estimated cost: ~$1.50–$30 per 1,000 conversations depending on model

---

### [Notification Service](https://github.com/andriisyniuchenko/notification-service)
> FastAPI · Celery · Redis · PostgreSQL · Docker

Background job queue for async notification delivery. Built to understand how production systems handle retries, failure states, and worker scaling — not to add another project to a list.

- Status machine: `pending → retrying → sent / failed`
- Retry logic: 3 attempts, 5-second delay, intentional 10% failure rate
- Workers scale independently from the API layer

---

## Certifications

- [FastAPI — Udemy](https://www.udemy.com/certificate/UC-cc0e5848-595b-4f1c-8530-c3b82c7c94c8/)
- [Django — Udemy](https://www.udemy.com/certificate/UC-f68b5b64-eba9-4f0c-b2a7-f6054db803ee/)
- [LangChain & LangGraph — Udemy](https://www.udemy.com/certificate/UC-9065b9a9-9eb6-42e4-b4d0-659c42f9a4f5/)
- [Introduction to Model Context Protocol - Anthropic](https://verify.skilljar.com/c/vq5ozrabikbm)
