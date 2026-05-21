# Andrii Syniuchenko
 
Backend developer based in Seattle, WA.  
Focused on Python (FastAPI, Django) — building production-oriented backend systems with real business logic.
 
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/andrii-syniuchenko)
 
---
 
## Tech Stack
 
**Languages:** Python  
**Frameworks:** FastAPI · Django  
**Databases:** PostgreSQL · Redis · OpenSearch · MongoDB  
**Infrastructure:** Docker · Docker Compose · GitHub Actions · Linux  
**Tools & Patterns:** SQLAlchemy · Alembic · Celery · JWT · REST API · OpenAPI (Swagger) · httpx · Pydantic v2  
**AI / LLM:** LangChain · LangGraph · Ollama · Groq · OpenAI · Anthropic · RAG
 
---
 
## Projects
 
### Auto Dealer Ecosystem
 
A two-service microservice system for a fictional dealership. The website and CRM are independently deployable and communicate over HTTP with API key authentication.
 
```
┌──────────────────────────────┐        ┌──────────────────────────────┐
│  Customer-facing Website     │        │  Auto Dealer CRM             │
│  auto-dealer-conversation-   │  HTTP  │  auto_dealer_crm             │
│  service · localhost:8001    │──POST──▶  localhost:8000              │
│                              │  Key   │                              │
│  Inventory browsing + forms  │        │  Internal lead & deal mgmt   │
└──────────────────────────────┘        └──────────────────────────────┘
```
 
---
 
#### [Auto Dealer CRM](https://github.com/andriisyniuchenko/auto_dealer_crm)
> FastAPI · PostgreSQL 16 · SQLAlchemy 2.0 · Alembic · JWT · Pydantic v2 · Docker · GitHub Actions CI · pytest
 
[![CI](https://github.com/andriisyniuchenko/auto_dealer_crm/actions/workflows/ci.yml/badge.svg)](https://github.com/andriisyniuchenko/auto_dealer_crm/actions/workflows/ci.yml)
 
Backend CRM system that models how a real dealership sales team operates — from lead intake to closed deals. Ships with both a web UI and a REST API, fully containerized, one-command startup.
 
📹 [Watch demo video](https://youtu.be/8uaZtSdtifc)
 
- Role-based access control (General Manager, Manager, Finance Manager, Salesperson)
- Lead assignment, shared ownership (50/50 split), and stale lead detection (7+ days no contact)
- Full lead timeline: notes, activities, appointments, deal history
- Split deal credit system with per-salesperson leaderboard
- Public lead intake API — `POST /api/v1/leads/public` secured with `X-API-Key`, used by the website service
- JWT cookie-based sessions for web UI + Bearer token support for API
- Manager-controlled user registration — no public sign-up
- Structured architecture: routers / services / models / schemas
- 48 pytest tests covering auth, RBAC, leads, appointments, and deals — GitHub Actions CI runs on every push
---
 
#### [Auto Dealer Conversation Service](https://github.com/andriisyniuchenko/auto-dealer-conversation-service)
> FastAPI · PostgreSQL 15 · SQLAlchemy 2.0 async · asyncpg · LangGraph · LangChain · Groq · OpenSearch · Ollama · httpx · Jinja2 · Bootstrap 5 · Alembic · Docker
 
[![CI](https://github.com/andriisyniuchenko/auto-dealer-conversation-service/actions/workflows/ci.yml/badge.svg)](https://github.com/andriisyniuchenko/auto-dealer-conversation-service/actions/workflows/ci.yml)
 
Full-stack customer-facing dealership website with a browsable inventory of 60 vehicles and an AI chat assistant (Jessica) powered by LangGraph and RAG. Integrated with the CRM service — lead forms and chat transcripts submit directly to the CRM via HTTP.
 
- Browse and filter 60 vehicles by make, year, mileage, price, and condition
- Individual vehicle detail pages with specs, photos, and a lead submission form
- **AI chat assistant (Jessica)** — ReAct-style LangGraph agent with RAG: embeds queries via Ollama (`nomic-embed-text`), runs hybrid KNN + BM25 search on OpenSearch, streams responses token by token via SSE; LLM provider swappable via env vars (Groq, OpenAI, Anthropic)
- Agent tools: `search_vehicles` (semantic + keyword search) and `submit_lead` (sends contact details to CRM)
- Chat transcript automatically saved to CRM when a lead is collected, displayed as chat bubbles on the lead detail page
- Fully async stack: `create_async_engine` + `asyncpg` throughout
- Containerized via Docker Compose; 15 pytest tests — GitHub Actions CI runs on every push
---
 
### [Notification Service](https://github.com/andriisyniuchenko/notification-service)
> FastAPI · Celery · Redis · PostgreSQL · Docker
 
Standalone async notification service for email, SMS, and push delivery — built to mirror how real production systems handle background job queues.
 
- API accepts a request, saves it as `pending`, and immediately returns — Celery worker processes it asynchronously
- Notification status machine: `pending → retrying → sent / failed`
- Retry logic: up to 3 attempts with 5-second delay; intentional 10% failure rate to demonstrate retry behavior
- Workers scale independently from the API layer
- Minimal live UI that polls status updates every 3 seconds without page reload
- Fully containerized with Docker Compose (web, worker, db, redis)
