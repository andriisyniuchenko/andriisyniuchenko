# Hi, I'm Andrii 👋

Backend developer focused on Python (FastAPI/Django).  
Currently building real-world projects and improving my backend skills.

---

## 🚀 About Me

- 💻 Backend developer (Python / Go)
- 📍 Based in Seattle, Washington, USA
- 🔄 Actively improving skills and preparing for backend roles
- ⚙️ Focused on building practical backend systems (APIs, services, databases)

---

## 🛠 Tech Stack

- **Languages:** Python, Go
- **Backend:** FastAPI, Django
- **Database:** PostgreSQL, SQLAlchemy
- **Tools:** Docker, Git, Linux
- **Other:** REST APIs, JWT Authentication, OpenAPI (Swagger), Celery, Redis

---

## 📌 Projects


### 🚗 Auto Dealer CRM [Go to repository](https://github.com/andriisyniuchenko/auto_dealer_crm)

A backend system designed to simulate a real dealership workflow.  
The goal of this project is to model how leads are managed, assigned, and converted into deals inside a sales team.

The system includes:
- Role-based access (manager, salesperson)
- Lead distribution and shared ownership between salespeople
- Tracking active, sold, and inactive leads separately
- Authentication and protected endpoints (JWT)
- Structured architecture (services, routers, models)

This project focuses on backend design, data relationships, and real business logic rather than UI.

---

### 📬 Notification Service [Go to repository](https://github.com/andriisyniuchenko/notification-service)

A service responsible for sending notifications (email/SMS) using asynchronous processing.

Built as a separate system that mimics how real production services handle background jobs.

Key ideas behind this project:
- Decoupling request handling from execution (queue-based system)
- Using Celery + Redis for background task processing
- Ability to scale workers independently from the API
- Dockerized environment for easier deployment and consistency

The goal is to understand how real systems handle delayed and high-volume tasks.

---

### 💳 Subscription Tracker [Go to repository](https://github.com/andriisyniuchenko/subscription-tracker)

A simple backend application for managing user subscriptions and recurring payments.

This project focuses on clean API design and basic business logic.

Main features:
- CRUD operations for subscriptions
- Tracking active and expired subscriptions
- PostgreSQL database with structured models
- Clear and minimal architecture

Built to practice writing clean, maintainable backend code without unnecessary complexity.

---
