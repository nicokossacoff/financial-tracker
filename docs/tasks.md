# Financial Tracker Task List

This list tracks our progress through the phases of building the application. Let me know when you are ready to begin Phase 1!

## Phase 1: Foundation (Local Setup & Database)
- [ ] **[USER]** Set up the `backend` directory and initialize FastAPI.
- [ ] **[USER]** Configure the PostgreSQL connection using SQLAlchemy.
- [ ] **[USER]** Set up basic Database Models (Tables) for Users and Expenses.
- [ ] **[USER]** Create `docker-compose.yml` for local PostgreSQL and FastAPI.
- [ ] **[AGENT]** Initialize the `frontend` directory using React/Vite.
- [ ] **[AGENT]** Set up the frontend design system (colors, typography, CSS).

## Phase 2: Authentication & Privacy
- [ ] **[USER]** Implement JWT authentication in FastAPI.
- [ ] **[USER]** Create `/register` and `/login` endpoints with password hashing.
- [ ] **[USER]** Secure API endpoints for logged-in users only.
- [ ] **[AGENT]** Build Login and Registration UI screens.
- [ ] **[AGENT]** Configure frontend to securely store and use JWT tokens.

## Phase 3: Core Features (Dashboard & Budgeting)
- [ ] **[USER]** Build CRUD endpoints for Expenses and Budget goals.
- [ ] **[USER]** Write SQL queries to group expenses by month.
- [ ] **[AGENT]** Build the Dashboard UI with interactive charts.
- [ ] **[AGENT]** Build the Budget Planning UI.

## Phase 4: LLM PDF Integration
- [ ] **[USER]** Create a FastAPI endpoint for PDF file uploads.
- [ ] **[AGENT]** Write Python backend service to extract text from PDFs.
- [ ] **[AGENT]** Integrate external LLM API to parse paystub data into JSON.
- [ ] **[AGENT]** Build frontend drag-and-drop file upload UI.

## Phase 5: Dockerization & Deployment
- [ ] **[USER]** Write production `Dockerfile` for the backend.
- [ ] **[USER]** Configure production environment variables.
- [ ] **[AGENT]** Write production `Dockerfile` for the frontend (Nginx).
- [ ] **[JOINT]** Deploy PostgreSQL database, Backend, and Frontend to Render.
