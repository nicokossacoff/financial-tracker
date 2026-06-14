# Financial Tracker Application Implementation Plan

This document outlines the architecture, tool selection, project structure, and a phased execution plan for building your financial tracker app. It reflects the finalized decisions regarding the technology stack.

## 1. Goal Description

Build a comprehensive financial tracker application that allows users to:
1. Manually add expenses and view spending dashboards grouped by time periods.
2. Plan monthly budgets, including saving goals, expected expenses, and earnings.
3. Upload paystub PDFs for automatic data extraction using an LLM.
4. Securely store and access data via an API, with a beautiful frontend UI.

You will focus on learning and building the **Backend (FastAPI)**, **Database (PostgreSQL)**, **Authentication**, and **Docker/Deployment**. The AI agents will focus on the **Frontend (UI/UX)** and the **LLM Integration** for PDF extraction.

## 2. Tool Selection (Finalized)

*   **Backend API:** FastAPI (Python)
*   **Database:** PostgreSQL (with SQLAlchemy ORM). We will use PostgreSQL for all data storage, leveraging its JSONB capabilities if unstructured data storage is needed for LLM outputs.
*   **Frontend Framework:** React (via Vite)
*   **LLM Integration:** External API (e.g., OpenAI's `gpt-4o-mini` or Anthropic's `claude-3-haiku`) for extracting text from uploaded PDFs.
*   **Deployment platform:** Render (with Docker containers for both backend and frontend).

## 3. Project Structure (Monorepo)

We will use a monorepo structure, meaning both frontend and backend live in the same Git repository. This makes Docker setup and local development much easier.

```text
financial-tracker/
├── backend/                <-- YOUR MAIN FOCUS
│   ├── app/
│   │   ├── api/            # FastAPI route definitions (Endpoints)
│   │   ├── core/           # Security, authentication, and configurations
│   │   ├── db/             # PostgreSQL database setup and SQLAlchemy models
│   │   ├── services/       # Business logic (Agent will build the LLM service here)
│   │   └── main.py         # FastAPI application entry point
│   ├── requirements.txt    # Python dependencies
│   └── Dockerfile          # Docker setup for the backend
├── frontend/               <-- AGENT'S MAIN FOCUS
│   ├── src/
│   │   ├── components/     # Reusable UI components (Buttons, Charts)
│   │   ├── pages/          # Dashboard, Budget, Upload pages
│   │   └── lib/            # API client to talk to the FastAPI backend
│   ├── package.json        # Node.js dependencies
│   └── Dockerfile          # Docker setup for the frontend
└── docker-compose.yml      <-- JOINT FOCUS (For running everything locally)
```

## 4. Division of Labor & Phased Plan

### Phase 1: Foundation (Local Setup & Database)
- **You:** Set up the `backend` directory, initialize FastAPI, and configure the PostgreSQL connection using SQLAlchemy. Set up the basic Database Models (Tables) for Users and Expenses.
- **You:** Create a `docker-compose.yml` to spin up a local PostgreSQL database and your FastAPI server.
- **Agent:** Initialize the `frontend` directory using React/Vite and set up a beautiful, modern design system (colors, typography, TailwindCSS/Vanilla CSS).

### Phase 2: Authentication & Privacy
- **You:** Implement JWT (JSON Web Token) authentication in FastAPI. Create `/register` and `/login` endpoints, and ensure passwords are securely hashed (using `passlib` and `bcrypt`). Secure the API endpoints so only logged-in users can access their own data.
- **Agent:** Build the Login and Registration UI screens. Set up the frontend to securely store the JWT token and attach it to API requests.

### Phase 3: Core Features (Dashboard & Budgeting)
- **You:** Build the FastAPI endpoints for creating, reading, updating, and deleting (CRUD) Expenses and Budget goals. Ensure SQL queries correctly group expenses by month.
- **Agent:** Build the Dashboard UI, incorporating interactive charts to visualize the spending data retrieved from your API. Build the Budget Planning UI.

### Phase 4: LLM PDF Integration
- **You:** Create a FastAPI endpoint that accepts file uploads (PDFs). 
- **Agent:** Write the Python service in the backend that takes the uploaded PDF, extracts the text (using tools like `PyPDF2` or `pdfplumber`), sends it to the chosen LLM API to parse the paystub data into JSON, and returns it. Build the frontend UI for drag-and-drop file uploads.

### Phase 5: Dockerization & Deployment
- **You:** Write the production `Dockerfile` for the backend. Configure environment variables for production.
- **Agent:** Write the production `Dockerfile` for the frontend (using Nginx to serve static files).
- **Together:** Deploy the PostgreSQL database, the Backend service, and the Frontend service to Render.

## 5. Verification Plan

*   **Automated/Manual Tests:** Testing will be done manually via the Swagger UI provided by FastAPI (`/docs`) for backend endpoints, and browser testing for the React frontend.
*   **Deployment Verification:** Verifying the live endpoints and hosted UI on Render once pushed.
