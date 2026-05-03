# Andrii Syniuchenko
 
Backend developer based in Seattle, WA.  
Focused on Python (FastAPI, Django) — building production-oriented backend systems with real business logic.
 
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/andrii-syniuchenko)
 
---
 
## Tech Stack
 
**Languages:** Python  
**Frameworks:** FastAPI · Django  
**Databases:** PostgreSQL · Redis · OpenSearch 
**Infrastructure:** Docker · Docker Compose · GitHub Actions · Linux  
**Tools & Patterns:** SQLAlchemy · Alembic · Celery · JWT · REST API · OpenAPI (Swagger) · httpx · Pydantic v2  
**AI / LLM:** LangChain · Ollama · RAG
 
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
> FastAPI · PostgreSQL 15 · SQLAlchemy 2.0 async · asyncpg · httpx · Jinja2 · Bootstrap 5 · ChromaDB · Alembic · Docker

[![CI](https://github.com/andriisyniuchenko/auto-dealer-conversation-service/actions/workflows/ci.yml/badge.svg)](https://github.com/andriisyniuchenko/auto-dealer-conversation-service/actions/workflows/ci.yml)
 
Full-stack customer-facing dealership website with a browsable inventory of 60 vehicles. Integrated with the CRM service — lead forms submit directly to the CRM via HTTP. AI chat assistant is in progress.
 
- Browse and filter 60 vehicles (30 new 2026 Subaru + 30 used) by make, year, mileage, price, condition
- Individual vehicle detail pages with specs, photos, and a lead submission form
- Lead form sends `POST` to the CRM service via `httpx.AsyncClient` with API key auth
- Fully async stack: `create_async_engine` + `asyncpg` throughout
- Conversation history schema in place: `chat_sessions` and `chat_messages` in PostgreSQL
- Containerized: FastAPI app + PostgreSQL + ChromaDB via Docker Compose
- 15 pytest tests covering inventory routes, filters, lead form validation, and CRM integration — GitHub Actions CI runs on every push
- **In progress:** AI chat assistant — semantic vehicle search via ChromaDB, LangChain orchestration, local LLM via Ollama (llama3.2)
---
 
### [Doc Helper](https://github.com/andriisyniuchenko/doc-helper)
> LangChain · OpenSearch · Ollama · Streamlit · Docker
 
A local RAG-based documentation assistant that answers questions about LangChain. Crawls the official docs, indexes them into a vector store, and uses a local LLM to generate answers — no OpenAI required, everything runs locally.
 
- Crawls `python.langchain.com` via Tavily, chunks with `RecursiveCharacterTextSplitter`
- Embeddings generated with Ollama (`nomic-embed-text`), stored in OpenSearch 3.6
- On each query: question embedded → kNN search returns top-5 chunks → passed to `llama3.2:3b` via Ollama
- Out-of-scope questions correctly refused
- Observability via LangSmith
- Fully containerized with Docker Compose; Makefile for one-command setup
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
---
 
### [Subscription Tracker](https://github.com/andriisyniuchenko/subscription-tracker)
> Django · PostgreSQL · Docker · GitHub Actions CI

[![CI](https://github.com/andriisyniuchenko/subscription-tracker/actions/workflows/ci.yml/badge.svg)](https://github.com/andriisyniuchenko/subscription-tracker/actions/workflows/ci.yml)
 
Django backend for tracking personal subscriptions and recurring expenses.
 
- User authentication and per-user data isolation
- Full CRUD for subscriptions with active/expired tracking
- Monthly cost dashboard
- Seed script for demo data
