# ARCHITECTURE.md

**Purpose**: Technical implementation plan for TaskFlow

**Last Updated**: 2025-01-09

---

## Project Vision (From PROJECT.md)

A lightweight task management app that helps solo founders and small teams stay focused on their most important work without overwhelming complexity.

---

## Architecture Overview

### High-Level Architecture

```
Three-tier web application:
- Frontend: React SPA with TypeScript (deployed to Vercel)
- Backend: Node.js REST API with Express (deployed to Railway)
- Database: PostgreSQL (hosted on Supabase free tier)

User Browser → Vercel CDN (React App) → Railway (API Server) → Supabase (PostgreSQL)
```

### Component Separation

**Frontend** (`/client`):
- Pages organized by route (Today, Projects, Settings)
- Shared components in `/components` (TaskCard, ProjectList, etc.)
- State managed with Zustand (lightweight, simple stores)
- API client with fetch + React Query for caching

**Backend** (`/server`):
- `/routes` - Express route definitions
- `/controllers` - Request/response handling
- `/services` - Business logic
- `/models` - Database queries (Prisma ORM)
- `/middleware` - Auth, error handling

**Database**:
- Normalized relational schema
- Users, Projects, Tasks, TeamMembers tables
- Foreign key constraints for data integrity

---

## Technology Stack

### Core Technologies

**Frontend**:
- Framework: React 18.2
- Language: TypeScript 5.0
- Routing: React Router v6
- State Management: Zustand (simpler than Redux)
- UI Components: Shadcn/ui (accessible, customizable)
- Styling: Tailwind CSS
- Data Fetching: React Query (caching, optimistic updates)

**Backend**:
- Runtime: Node.js 20
- Framework: Express 4.18
- Language: TypeScript 5.0
- API Style: REST (simple, standard)
- Validation: Zod (type-safe validation)
- ORM: Prisma (type-safe queries, great migrations)

**Database**:
- Primary: PostgreSQL 15 (Supabase hosted)
- ORM: Prisma
- Migrations: Prisma Migrate

**Authentication**:
- Strategy: JWT tokens (7-day expiration)
- Password hashing: bcrypt (12 rounds)
- Tokens stored in httpOnly cookies

**Infrastructure**:
- Frontend Hosting: Vercel (auto-deploy from main branch)
- Backend Hosting: Railway (manual deploys initially)
- Database: Supabase free tier
- CI/CD: GitHub Actions (linting + tests on PR)
- Monitoring: None for MVP (add Sentry post-launch)

### Key Dependencies

**Frontend**:
- `react-query` - Server state management, automatic refetching
- `react-hook-form` - Form handling with validation
- `date-fns` - Date manipulation (lighter than moment)
- `lucide-react` - Icon library

**Backend**:
- `express` - Web framework
- `prisma` - Database ORM
- `bcrypt` - Password hashing
- `jsonwebtoken` - JWT creation/verification
- `zod` - Runtime validation

---

## Data Models

### Core Entities

**User**
```
Fields:
- id: UUID (primary key)
- email: string (unique, indexed)
- password_hash: string
- name: string
- created_at: timestamp
- updated_at: timestamp

Relations:
- Has many: Projects (created_by)
- Has many: TeamMembers (user_id)
- Has many: Tasks (assigned_to)
```

**Project**
```
Fields:
- id: UUID (primary key)
- name: string
- description: string (nullable)
- created_by: UUID (foreign key → User)
- created_at: timestamp
- updated_at: timestamp

Relations:
- Belongs to: User (creator)
- Has many: Tasks
- Has many: TeamMembers (access control)
```

**Task**
```
Fields:
- id: UUID (primary key)
- title: string
- description: text (nullable)
- project_id: UUID (foreign key → Project)
- assigned_to: UUID (foreign key → User, nullable)
- priority: enum (high, medium, low)
- status: enum (todo, completed)
- due_date: date (nullable)
- completed_at: timestamp (nullable)
- created_at: timestamp
- updated_at: timestamp

Relations:
- Belongs to: Project
- Belongs to: User (assignee)
```

**TeamMember**
```
Fields:
- id: UUID (primary key)
- project_id: UUID (foreign key → Project)
- user_id: UUID (foreign key → User)
- role: enum (owner, member)
- joined_at: timestamp

Relations:
- Belongs to: Project
- Belongs to: User

Unique constraint: (project_id, user_id)
```

### Database Schema Notes

**Indexes**:
- User.email (unique, for login lookups)
- Task.project_id (for project task queries)
- Task.assigned_to (for "my tasks" queries)
- Task.due_date (for "today" view queries)

**Constraints**:
- Task.project_id must reference valid Project
- Task.assigned_to must reference valid User (if not null)
- TeamMember unique on (project_id, user_id) - can't join project twice

**Cascading**:
- Delete Project → cascade delete Tasks and TeamMembers
- Delete User → set Tasks.assigned_to to null (preserve task)

---

## API Design

### Endpoint Structure

```
Base URL: /api/v1

Authentication:
- JWT token in httpOnly cookie (set on login)
- All endpoints except /auth/* require valid token
- Middleware validates token and attaches user to req.user

Response Format:
Success: { success: true, data: {...} }
Error: { success: false, error: { code: "INVALID_INPUT", message: "..." } }
```

### Key Endpoints

**Authentication**:
- `POST /api/v1/auth/register` - Create account (email, password, name)
- `POST /api/v1/auth/login` - Login (email, password) → sets httpOnly cookie
- `POST /api/v1/auth/logout` - Clear auth cookie
- `GET /api/v1/auth/me` - Get current user info

**Projects**:
- `GET /api/v1/projects` - List user's projects (owned + member of)
- `POST /api/v1/projects` - Create new project
- `GET /api/v1/projects/:id` - Get single project with tasks
- `PATCH /api/v1/projects/:id` - Update project name/description
- `DELETE /api/v1/projects/:id` - Delete project (owner only)

**Tasks**:
- `GET /api/v1/tasks/today` - Tasks due today or overdue (across all projects)
- `GET /api/v1/projects/:projectId/tasks` - All tasks in project
- `POST /api/v1/projects/:projectId/tasks` - Create task in project
- `GET /api/v1/tasks/:id` - Get single task
- `PATCH /api/v1/tasks/:id` - Update task (title, description, due date, priority, assigned_to)
- `POST /api/v1/tasks/:id/complete` - Mark task complete
- `DELETE /api/v1/tasks/:id` - Delete task

**Team**:
- `POST /api/v1/projects/:projectId/invite` - Invite user to project by email
- `GET /api/v1/projects/:projectId/members` - List project members
- `DELETE /api/v1/projects/:projectId/members/:userId` - Remove member (owner only)

---

## Request/Response Flows

### Critical User Flows

**User Login**:
```
1. User submits email/password on login page
2. Frontend: POST /api/v1/auth/login with credentials
3. Backend: Validate email format (Zod)
4. Backend: Find user by email in database
5. Backend: Compare password with bcrypt.compare()
6. Backend: Generate JWT token (expires 7 days, contains user.id)
7. Backend: Set httpOnly cookie with token
8. Backend: Return { success: true, data: { user: { id, email, name } } }
9. Frontend: Store user in Zustand state
10. Frontend: Redirect to /today
```

**Creating a Task**:
```
1. User fills out task form (title, description, due date, priority)
2. Frontend: Validate with react-hook-form + Zod schema
3. Frontend: POST /api/v1/projects/:projectId/tasks
4. Backend: Auth middleware verifies JWT cookie
5. Backend: Validate request body with Zod
6. Backend: Check user has access to project (TeamMember record exists)
7. Backend: Create task in database via Prisma
8. Backend: Return created task
9. Frontend: React Query updates cache (optimistic update)
10. Frontend: Show success toast, close form
```

**Loading Today View**:
```
1. User navigates to /today page
2. Frontend: GET /api/v1/tasks/today (React Query)
3. Backend: Auth middleware verifies JWT cookie
4. Backend: Query tasks WHERE assigned_to = user.id AND (due_date = today OR due_date < today) AND status != completed
5. Backend: Return array of tasks with project info (join)
6. Frontend: Render task list grouped by project
7. Frontend: React Query caches result (5 min stale time)
```

---

## Security Considerations

**Authentication & Authorization**:
- Passwords hashed with bcrypt, 12 rounds (secure, industry standard)
- JWT tokens in httpOnly cookies (prevents XSS token theft)
- Tokens expire in 7 days (re-login required)
- All API endpoints verify token and user access

**Input Validation**:
- Client-side: React Hook Form with Zod schemas (UX, immediate feedback)
- Server-side: Zod validation on all request bodies (security, never trust client)
- SQL injection prevented by Prisma parameterized queries

**Data Protection**:
- Passwords never stored in plain text (bcrypt hash only)
- User can only access their own projects/tasks (middleware checks)
- Team member checks before allowing project/task operations

**API Security**:
- CORS configured to allow only frontend domain
- Rate limiting: 100 requests per minute per IP (express-rate-limit)
- No CSRF protection needed (using httpOnly cookies + SameSite=Strict)

---

## Performance Considerations

**Target Metrics**:
- Initial page load: <2s on 3G
- Task list render: <200ms
- Task create/complete: <300ms perceived (optimistic updates)

**Optimization Strategies**:
- React Query caching (5 min stale time for task lists)
- Optimistic updates for task complete (instant UI feedback)
- Pagination for task lists (50 tasks per page, load more)
- Database indexes on frequently queried fields
- Code splitting: lazy load settings page, project detail pages

---

## Development Environment Setup

### Prerequisites
```bash
- Node.js 20+
- PostgreSQL 15+ (or use Docker)
- npm or yarn
```

### Initial Setup
```bash
# Clone repo
git clone https://github.com/yourorg/taskflow.git
cd taskflow

# Install dependencies (root, server, client)
npm install

# Set up environment variables
cp .env.example .env
# Edit .env with local DATABASE_URL, JWT_SECRET

# Database setup
cd server
npx prisma migrate dev  # Run migrations
npx prisma db seed      # Seed with sample data (optional)

cd ..
```

### Running Locally
```bash
# Terminal 1: Start backend (from /server)
cd server
npm run dev  # Runs on :5000

# Terminal 2: Start frontend (from /client)
cd client
npm run dev  # Runs on :5173
```

Open browser to http://localhost:5173

---

## Testing Strategy

**Unit Tests**:
- Business logic in `/server/services` - Jest tests
- Validation schemas (Zod) - Test edge cases
- Utility functions - date formatting, etc.

**Integration Tests**:
- API endpoints - Supertest with test database
- Test auth flow (register, login, protected routes)
- Test CRUD operations for tasks/projects

**E2E Tests** (Post-MVP):
- Critical user flows with Playwright
- Login → create project → add task → complete task

**Test Coverage Goals**:
- 70% for backend services and controllers
- Frontend component testing not required for MVP (manual testing)

---

## Deployment Architecture

**Hosting**:
- Frontend: Vercel (connected to GitHub main branch, auto-deploy)
- Backend: Railway (manual deploy via CLI initially)
- Database: Supabase free tier (PostgreSQL managed)

**Environment Variables**:
- `DATABASE_URL` - PostgreSQL connection string (Supabase)
- `JWT_SECRET` - Secret for signing JWT tokens (generate random)
- `FRONTEND_URL` - For CORS configuration
- `NODE_ENV` - production/development

**Build Process**:
```bash
# Frontend (client/)
npm run build  # Outputs to dist/ (Vite)

# Backend (server/)
npm run build  # TypeScript → dist/ (tsc)
```

**Deployment Steps**:
1. Push to main branch
2. Vercel auto-deploys frontend (builds, deploys to CDN)
3. Backend: `railway up` (manual for MVP, CI/CD later)
4. Run migrations: `npx prisma migrate deploy` on Railway
5. Verify: Check health endpoint /api/v1/health

---

## Open Technical Questions

1. **Session management**: Should we add refresh tokens for better security?
   - **Options**: Current (7-day JWT) vs refresh token pattern
   - **Trade-offs**: Simplicity vs security
   - **Decision needed by**: Before launch
   - **Current approach**: 7-day JWT for MVP simplicity

2. **Task ordering**: How should tasks be ordered within projects?
   - **Options**: Manual drag-drop order vs auto-sort by due date/priority
   - **Trade-offs**: Flexibility vs complexity
   - **Decision needed by**: Week 3
   - **Leaning toward**: Auto-sort for MVP (less state to manage)

---

## Future Considerations (Post-MVP)

- **Caching**: Add Redis for session storage and frequently accessed data
- **Real-time updates**: WebSocket for live task updates when team members make changes
- **Background jobs**: Bull queue for email sending, recurring task creation
- **Monitoring**: Sentry for error tracking, LogRocket for user sessions
- **Search**: Add full-text search across tasks (PostgreSQL tsvector or Algolia)
- **Mobile apps**: React Native apps if web traction is good

---

## Changelog

### 2025-01-09 - Initial Architecture
**Created**: Initial technical planning document
**Decisions**:
- Chose Zustand over Redux (simpler for small state)
- Chose Prisma over raw SQL (type safety, migrations)
- Chose httpOnly cookies over localStorage for tokens (XSS protection)
**Next**: Begin implementation with Milestone 1 (setup)
