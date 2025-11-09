# TASKS.md

**Purpose**: Living checklist of work to be done, organized by milestones. This is the operational heart of the project.

**Last Updated**: [Date]

---

## How to Fill This Out

**Purpose**: This is your operational checklist. AI agents read this to know what to work on next.

**Initial setup** (15-30 minutes):
1. Break your project into 5-8 major milestones (Setup, Core Features, Polish, Testing, Deploy)
2. Under each milestone, list atomic tasks (completable in one session)
3. Use the milestone templates below as a starting point

**During development**:
- AI marks tasks complete with dates as it finishes them
- You can manually add new tasks as scope evolves
- Keep this file in sync with reality (don't let it get stale)

### Task Writing Guidelines
- **Atomic**: Each task = one focused session (30-90 minutes max)
- **Specific**: Bad: "Handle auth" → Good: "Implement JWT generation in auth/jwt.ts"
- **Actionable**: Start with verbs: Create, Implement, Add, Fix, Update, Test
- **Independent**: Should be doable without blocking on other tasks

### Status Format
- `- [ ]` = Not started
- `- [x]` = Completed (always add date)

**Example**:
```markdown
- [x] Initialize project repository (2025-01-09)
- [x] Set up React with TypeScript (2025-01-09 - created src/, tsconfig.json)
- [ ] Create login page component
```

### For AI Agents
- Read this file at session start
- Mark tasks complete immediately when done (with date)
- Add newly discovered tasks to appropriate milestone
- If a task is too big, break it into subtasks

---

## Project Milestones

### Milestone 1: Project Setup & Foundation
**Goal**: Get development environment working with basic structure

- [ ] Initialize git repository
- [ ] Set up frontend framework and build tools
- [ ] Set up backend framework and dependencies
- [ ] Configure database connection
- [ ] Create .env.example with required variables
- [ ] Set up linting and formatting (ESLint, Prettier, etc.)
- [ ] Create basic folder structure (following PLANNING.md)
- [ ] Add health check/ping endpoint
- [ ] Verify local development environment works end-to-end

---

### Milestone 2: Authentication & User Management
**Goal**: Users can register, log in, and manage sessions

- [ ] Design User data model (see PLANNING.md)
- [ ] Create database migration for users table
- [ ] Implement user registration endpoint
- [ ] Implement password hashing (bcrypt/argon2)
- [ ] Implement login endpoint with JWT generation
- [ ] Create authentication middleware for protected routes
- [ ] Implement token refresh mechanism (if applicable)
- [ ] Add logout functionality (token invalidation)
- [ ] Create registration page/form (frontend)
- [ ] Create login page/form (frontend)
- [ ] Add auth state management (frontend)
- [ ] Create protected route wrapper/guard (frontend)
- [ ] Test full authentication flow

---

### Milestone 3: Core Data Layer
**Goal**: Database models and API endpoints for core entities

**[Entity 1 - e.g., Invoices]**
- [ ] Design [Entity] data model
- [ ] Create database migration for [entity] table
- [ ] Implement GET /api/[entities] - list with pagination
- [ ] Implement POST /api/[entities] - create
- [ ] Implement GET /api/[entities]/:id - get single
- [ ] Implement PATCH /api/[entities]/:id - update
- [ ] Implement DELETE /api/[entities]/:id - delete
- [ ] Add input validation (Zod/Joi schemas)
- [ ] Add authorization checks (users can only access their own data)
- [ ] Write tests for [entity] endpoints

**[Entity 2 - e.g., Expenses]**
- [ ] Design [Entity] data model
- [ ] Create database migration for [entity] table
- [ ] Implement CRUD endpoints (list, create, get, update, delete)
- [ ] Add input validation
- [ ] Add authorization checks
- [ ] Write tests for [entity] endpoints

[Repeat for each core entity from PLANNING.md]

---

### Milestone 4: Frontend UI - Core Features
**Goal**: Users can interact with core functionality through UI

**[Feature 1 - e.g., Invoice Management]**
- [ ] Create [feature] list view component
- [ ] Create [feature] detail view component
- [ ] Create [feature] create/edit form component
- [ ] Implement form validation (client-side)
- [ ] Connect components to API endpoints
- [ ] Add loading states and error handling
- [ ] Add success/error notifications/toasts
- [ ] Test user flow end-to-end

**[Feature 2 - e.g., Dashboard]**
- [ ] Create dashboard layout
- [ ] Implement [metric 1] calculation and display
- [ ] Implement [metric 2] calculation and display
- [ ] Add data visualization (charts/graphs if needed)
- [ ] Connect to API endpoints
- [ ] Add loading and error states

[Add sections for each major UI feature]

---

### Milestone 5: Polish & User Experience
**Goal**: Make the app feel complete and pleasant to use

- [ ] Add loading skeletons for async operations
- [ ] Improve error messages (user-friendly, actionable)
- [ ] Add form field validation error messages
- [ ] Implement responsive design (mobile, tablet, desktop)
- [ ] Add empty states (e.g., "No invoices yet - create your first one")
- [ ] Add confirmation dialogs for destructive actions
- [ ] Implement keyboard shortcuts (if applicable)
- [ ] Add accessibility improvements (ARIA labels, focus management)
- [ ] Test on different browsers (Chrome, Firefox, Safari)
- [ ] Test on mobile devices

---

### Milestone 6: Testing & Quality Assurance
**Goal**: Ensure reliability and catch bugs before users do

**Backend Tests**:
- [ ] Write unit tests for authentication logic
- [ ] Write unit tests for [entity 1] business logic
- [ ] Write unit tests for [entity 2] business logic
- [ ] Write integration tests for API endpoints
- [ ] Test error handling (invalid inputs, auth failures)
- [ ] Test edge cases (empty data, malformed requests)

**Frontend Tests**:
- [ ] Write tests for critical user flows
- [ ] Test form validation logic
- [ ] Test error handling and display
- [ ] Test authentication flow (login, logout, protected routes)

**Manual Testing**:
- [ ] Test complete user registration and login flow
- [ ] Test [core feature 1] end-to-end
- [ ] Test [core feature 2] end-to-end
- [ ] Test on slow network (throttle to 3G)
- [ ] Test with screen reader (basic accessibility check)

---

### Milestone 7: Deployment & Launch Prep
**Goal**: Get the app running in production

- [ ] Set up production database (provision and configure)
- [ ] Configure environment variables in hosting platforms
- [ ] Set up frontend hosting (Vercel, Netlify, etc.)
- [ ] Set up backend hosting (Railway, Heroku, AWS, etc.)
- [ ] Configure custom domain (if applicable)
- [ ] Set up SSL/HTTPS
- [ ] Run database migrations in production
- [ ] Deploy backend to production
- [ ] Deploy frontend to production
- [ ] Verify production deployment (health checks)
- [ ] Test production environment end-to-end
- [ ] Set up error monitoring (Sentry, LogRocket, etc.) (optional)
- [ ] Set up basic analytics (optional)
- [ ] Create backup strategy for production database

---

## Backlog (Future / Nice-to-Have)

Tasks that are out of scope for MVP but worth tracking:

- [ ] Add email verification for new users
- [ ] Implement password reset flow
- [ ] Add social login (Google, GitHub, etc.)
- [ ] Implement file upload for receipts/attachments
- [ ] Add export to CSV/PDF functionality
- [ ] Implement real-time notifications
- [ ] Add dark mode
- [ ] Implement search and filtering
- [ ] Add data visualization dashboard
- [ ] Performance optimization (caching, lazy loading)

---

## Blocked / Waiting

Tasks that can't proceed yet due to dependencies or external blockers:

[Move tasks here if they're blocked, note what they're waiting for]

**Example**:
- [ ] Integrate payment processing - Waiting for Stripe API keys from client
- [ ] Deploy to production - Waiting for DNS configuration

---

## Notes & Decisions

[Use this space to capture important decisions made during task execution]

**Example**:
```
### 2025-01-09
- Decided to use Zod for validation on both frontend and backend (share schemas)
- Chose JWT with 7-day expiration, no refresh token for MVP (simpler)
- Postponing soft-deletes to post-MVP - using hard deletes for now
```

---

## Tips for AI Agents

- **At session start**: Read this file to understand what's done and what's next
- **During session**: Update status in real-time (mark tasks complete immediately)
- **If task is too big**: Break it down into smaller subtasks
- **If new work discovered**: Add it to the appropriate milestone
- **Before session end**: Ensure all completed tasks are marked with dates
- **Keep it current**: This file should always reflect reality, not aspirations
