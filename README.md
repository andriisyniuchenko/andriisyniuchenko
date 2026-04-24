# Andrii Syniuchenko

Backend developer based in Seattle, WA.  
Focused on Python (FastAPI, Django) — building production-oriented backend systems with real business logic.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/andrii-syniuchenko)

---

## Tech Stack

**Languages:** Python  
**Frameworks:** FastAPI · Django  
**Databases:** PostgreSQL · Redis  
**Infrastructure:** Docker · Docker Compose · Linux  
**Tools & Patterns:** SQLAlchemy · Alembic · Celery · JWT · REST API · OpenAPI (Swagger)

---

## Projects

### [Auto Dealer CRM](https://github.com/andriisyniuchenko/auto_dealer_crm)
> FastAPI · PostgreSQL · SQLAlchemy · Alembic · JWT

Backend CRM system that models how a real dealership sales team operates — from lead intake to closed deals.

📹 [Watch demo video](https://youtu.be/8uaZtSdtifc)
- Role-based access control (General Manager, Manager, Finance Manager, Salesperson)
- Lead assignment, shared ownership (50/50 split), and stale lead detection
- Full lead timeline: notes, activities, appointments, deal history
- Split deal credit system with per-salesperson statistics
- Manager-controlled user registration — no public sign-up
- Structured architecture: routers / services / models / schemas
- 43 pytest tests covering auth, RBAC, and business logic — GitHub Actions CI runs on every push

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
> Django · PostgreSQL · Docker

Django backend for tracking personal subscriptions and recurring expenses.

- User authentication and per-user data isolation
- Full CRUD for subscriptions with active/expired tracking
- Monthly cost dashboard
- Seed script for demo data
