# TASKS.md

**Purpose**: Work checklist for TaskFlow project

**Last Updated**: 2025-01-15

---

## Project Milestones

### Milestone 1: Project Setup & Foundation ✅
**Goal**: Get development environment working with basic structure

- [x] Initialize git repository (2025-01-09)
- [x] Set up React with TypeScript and Vite (2025-01-09 - client/ directory)
- [x] Set up Express backend with TypeScript (2025-01-09 - server/ directory)
- [x] Configure Prisma with PostgreSQL (2025-01-10 - schema.prisma created)
- [x] Create .env.example with required variables (2025-01-10)
- [x] Set up ESLint and Prettier for both frontend and backend (2025-01-10)
- [x] Create folder structure following ARCHITECTURE.md (2025-01-10)
- [x] Add health check endpoint GET /api/health (2025-01-11 - server/routes/health.ts)
- [x] Verify local dev environment works end-to-end (2025-01-11)

---

### Milestone 2: Authentication & User Management 🔄
**Goal**: Users can register, log in, and manage sessions

- [x] Design User data model in Prisma schema (2025-01-11)
- [x] Create database migration for users table (2025-01-11)
- [x] Implement user registration endpoint (2025-01-12 - POST /api/v1/auth/register)
- [x] Implement password hashing with bcrypt (2025-01-12)
- [x] Implement login endpoint with JWT generation (2025-01-13 - POST /api/v1/auth/login)
- [x] Create authentication middleware for protected routes (2025-01-13 - middleware/auth.ts)
- [x] Implement logout functionality (2025-01-14 - POST /api/v1/auth/logout)
- [x] Add GET /api/v1/auth/me endpoint (2025-01-14)
- [ ] Create registration page/form (frontend)
- [ ] Create login page/form (frontend)
- [ ] Add auth state management with Zustand (frontend)
- [ ] Create protected route wrapper (frontend)
- [ ] Test full authentication flow end-to-end

---

### Milestone 3: Core Data Layer
**Goal**: Database models and API endpoints for core entities

**Projects**
- [x] Design Project data model in Prisma (2025-01-14)
- [x] Create database migration for projects table (2025-01-14)
- [ ] Implement GET /api/v1/projects - list user's projects
- [ ] Implement POST /api/v1/projects - create project
- [ ] Implement GET /api/v1/projects/:id - get single project
- [ ] Implement PATCH /api/v1/projects/:id - update project
- [ ] Implement DELETE /api/v1/projects/:id - delete project
- [ ] Add input validation with Zod schemas
- [ ] Add authorization checks (user access to project)
- [ ] Write tests for project endpoints

**Tasks**
- [x] Design Task data model in Prisma (2025-01-14)
- [x] Create database migration for tasks table (2025-01-14)
- [ ] Implement GET /api/v1/tasks/today - today's tasks
- [ ] Implement GET /api/v1/projects/:projectId/tasks - project tasks
- [ ] Implement POST /api/v1/projects/:projectId/tasks - create task
- [ ] Implement GET /api/v1/tasks/:id - get single task
- [ ] Implement PATCH /api/v1/tasks/:id - update task
- [ ] Implement POST /api/v1/tasks/:id/complete - mark complete
- [ ] Implement DELETE /api/v1/tasks/:id - delete task
- [ ] Add input validation with Zod schemas
- [ ] Add authorization checks
- [ ] Write tests for task endpoints

**Team Members**
- [ ] Design TeamMember data model in Prisma
- [ ] Create database migration for team_members table
- [ ] Implement POST /api/v1/projects/:projectId/invite - invite user
- [ ] Implement GET /api/v1/projects/:projectId/members - list members
- [ ] Implement DELETE /api/v1/projects/:projectId/members/:userId - remove member
- [ ] Add authorization (only owners can invite/remove)
- [ ] Write tests for team endpoints

---

### Milestone 4: Frontend UI - Core Features
**Goal**: Users can interact with core functionality through UI

**Authentication UI**
- [ ] Create registration page with form
- [ ] Create login page with form
- [ ] Implement form validation (Zod + react-hook-form)
- [ ] Connect to API endpoints (register, login)
- [ ] Add loading states and error handling
- [ ] Add success/error toast notifications

**Today View**
- [ ] Create /today route and page component
- [ ] Create TaskCard component
- [ ] Fetch today's tasks from API (React Query)
- [ ] Display tasks grouped by project
- [ ] Add task completion toggle
- [ ] Add loading skeletons
- [ ] Add empty state ("No tasks for today!")

**Projects View**
- [ ] Create /projects route and page component
- [ ] Create ProjectList component
- [ ] Create ProjectCard component
- [ ] Fetch projects from API (React Query)
- [ ] Add "Create Project" button and modal
- [ ] Create ProjectForm component
- [ ] Connect create project to API
- [ ] Add project click → navigate to project detail

**Project Detail View**
- [ ] Create /projects/:id route and page component
- [ ] Fetch project with tasks from API
- [ ] Display project info (name, description)
- [ ] Display task list for project
- [ ] Add "Create Task" button and modal
- [ ] Create TaskForm component
- [ ] Connect create task to API
- [ ] Add task filtering (priority, assignee)
- [ ] Add edit/delete project actions (owner only)

**Navigation & Layout**
- [ ] Create main layout component with nav
- [ ] Add navigation links (Today, Projects, Settings)
- [ ] Add current user display in nav
- [ ] Add logout button
- [ ] Make nav responsive for mobile

---

### Milestone 5: Polish & User Experience
**Goal**: Make the app feel complete and pleasant to use

- [ ] Add loading skeletons for all async operations
- [ ] Improve error messages (user-friendly, actionable)
- [ ] Add field-level validation errors in forms
- [ ] Implement responsive design (test mobile, tablet, desktop)
- [ ] Add empty states (no projects, no tasks, etc.)
- [ ] Add confirmation dialog for delete actions
- [ ] Add keyboard shortcuts (Ctrl+K for quick task create)
- [ ] Improve accessibility (ARIA labels, focus management, keyboard nav)
- [ ] Test on Chrome, Firefox, Safari
- [ ] Test on mobile devices (iOS Safari, Android Chrome)

---

### Milestone 6: Testing & Quality Assurance
**Goal**: Ensure reliability and catch bugs before users do

**Backend Tests**:
- [ ] Write unit tests for auth service (register, login, token validation)
- [ ] Write unit tests for project service (create, update, access checks)
- [ ] Write unit tests for task service (create, complete, filter logic)
- [ ] Write integration tests for auth endpoints
- [ ] Write integration tests for project CRUD
- [ ] Write integration tests for task CRUD
- [ ] Test error handling (invalid inputs, auth failures, not found)
- [ ] Test edge cases (empty strings, malformed data, SQL injection attempts)

**Frontend Tests**:
- [ ] Test login flow (valid credentials, invalid credentials, error handling)
- [ ] Test registration flow (validation, duplicate email)
- [ ] Test task creation and completion
- [ ] Test project creation
- [ ] Test protected route redirects (unauthenticated user)

**Manual Testing**:
- [ ] Complete user journey: register → create project → add tasks → complete tasks
- [ ] Test today view updates when completing tasks
- [ ] Test team invite flow (invite user, accept invite, see shared project)
- [ ] Test on throttled 3G connection (Chrome DevTools network throttle)
- [ ] Basic accessibility check with screen reader (VoiceOver on Mac)

---

### Milestone 7: Deployment & Launch Prep
**Goal**: Get the app running in production

- [ ] Set up Supabase project and provision PostgreSQL database
- [ ] Configure environment variables in Railway (backend)
- [ ] Configure environment variables in Vercel (frontend)
- [ ] Set up Vercel deployment (connect GitHub repo)
- [ ] Set up Railway deployment (connect GitHub repo)
- [ ] Run database migrations in production (prisma migrate deploy)
- [ ] Deploy backend to Railway
- [ ] Deploy frontend to Vercel
- [ ] Configure custom domain (optional for MVP)
- [ ] Set up SSL/HTTPS (automatic with Vercel/Railway)
- [ ] Verify production health endpoint
- [ ] Test production environment end-to-end (register, login, create tasks)
- [ ] Set up error monitoring with Sentry (optional)
- [ ] Set up basic analytics (Plausible or Simple Analytics)
- [ ] Create database backup schedule (Supabase automatic backups)

---

## Backlog (Future / Nice-to-Have)

- [ ] Email verification for new users
- [ ] Password reset flow (forgot password)
- [ ] Social login (Google, GitHub OAuth)
- [ ] File attachments on tasks (image upload to S3)
- [ ] Export tasks to CSV
- [ ] Real-time notifications (WebSocket)
- [ ] Dark mode toggle
- [ ] Advanced search and filtering (full-text search)
- [ ] Task due date reminders (email notifications)
- [ ] Recurring tasks (daily, weekly, monthly)
- [ ] Subtasks (nested task lists)
- [ ] Task comments/discussions
- [ ] Activity feed (who did what)
- [ ] Mobile app (React Native)

---

## Blocked / Waiting

[No blocked tasks currently]

---

## Notes & Decisions

### 2025-01-09
- Decided on Zustand for state management (simpler than Redux, no boilerplate)
- Chose bcrypt over argon2 (wider compatibility, well-tested)
- Using httpOnly cookies for JWT (XSS protection)

### 2025-01-11
- Added unique index on User.email for faster login lookups
- Decided on 7-day JWT expiration (re-login required, no refresh tokens for MVP)

### 2025-01-13
- Auth middleware extracts user from JWT and attaches to req.user
- All protected endpoints can access req.user.id directly
- Token validation happens once per request (middleware)

### 2025-01-14
- Added TeamMember model for project access control
- Decided on cascade delete: deleting project removes all tasks and team members
- Tasks keep assigned_to when user is deleted (set to null, preserve history)
