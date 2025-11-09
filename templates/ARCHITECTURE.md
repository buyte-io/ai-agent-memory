# ARCHITECTURE.md

**Purpose**: Technical implementation plan, architecture decisions, and current system design.

**Last Updated**: [Date]

---

## How to Fill This Out

**Purpose**: This file defines HOW your system is built. It's the technical truth that AI agents reference when writing code.

**Time needed**: 30-45 minutes for new projects, update as architecture evolves

**Priority sections for MVP**:
1. Technology Stack (essential)
2. Data Models (essential)
3. API Design (essential)
4. Architecture Overview (important)
5. Development Environment Setup (important)

**Can skip initially**: Performance considerations, deployment details (add these as you scale)

**Critical rule**: Keep this file current. Stale architecture docs cause AI confusion and bugs.

---

## Project Vision (From PROJECT.md)

[One-sentence summary from PROJECT.md to anchor technical decisions]

**Example**: "A personal finance tracker for freelancers with variable income"

---

## Architecture Overview

### High-Level Architecture

[Describe the system architecture in text form. Can reference diagrams if they exist.]

**Example**:
```
Three-tier architecture:
- Frontend: React SPA (served via CDN)
- Backend: Node.js REST API (hosted on Railway)
- Database: PostgreSQL (hosted on Supabase)
- File Storage: AWS S3 for receipts/attachments

User → CDN (Frontend) → API Server → Database
                              ↓
                          S3 Storage
```

### Component Separation

**Frontend**:
- [How is the frontend organized? Pages, components, state management]

**Backend**:
- [How is the backend organized? Routes, controllers, services, models]

**Database**:
- [Schema design philosophy, normalization approach]

---

## Technology Stack

### Core Technologies

**Frontend**:
- Framework: [e.g., React 18.2, Vue 3, Svelte]
- Language: [e.g., TypeScript 5.0]
- Routing: [e.g., React Router v6]
- State Management: [e.g., Zustand, Redux Toolkit, Context API]
- UI Components: [e.g., Shadcn/ui, Material-UI, custom]
- Styling: [e.g., Tailwind CSS, CSS Modules, styled-components]

**Backend**:
- Runtime: [e.g., Node.js 20, Python 3.11, Go 1.21]
- Framework: [e.g., Express, FastAPI, Gin]
- Language: [e.g., TypeScript, Python, Go]
- API Style: [e.g., REST, GraphQL, tRPC]
- Validation: [e.g., Zod, Joi, Pydantic]

**Database**:
- Primary: [e.g., PostgreSQL 15]
- ORM/Query Builder: [e.g., Prisma, TypeORM, raw SQL]
- Migrations: [e.g., Prisma Migrate, Alembic, custom scripts]
- Cache Layer: [e.g., Redis, none for MVP]

**Authentication**:
- Strategy: [e.g., JWT tokens, session cookies, OAuth]
- Provider: [e.g., custom, Auth0, Supabase Auth]

**Infrastructure**:
- Hosting: [e.g., Vercel, Railway, AWS, self-hosted]
- CI/CD: [e.g., GitHub Actions, none for MVP]
- Monitoring: [e.g., Sentry, LogRocket, none for MVP]

### Key Dependencies

[List critical dependencies and why they were chosen:]

**Example**:
- `date-fns` - Date manipulation (lighter than moment.js)
- `react-query` - Server state management and caching
- `zod` - Runtime type validation for API boundaries

---

## Data Models

### Core Entities

**[Entity Name 1]** (e.g., User)
```
Fields:
- id: UUID (primary key)
- email: string (unique, indexed)
- password_hash: string
- created_at: timestamp
- updated_at: timestamp

Relations:
- Has many: Invoices, Expenses
```

**[Entity Name 2]** (e.g., Invoice)
```
Fields:
- id: UUID (primary key)
- user_id: UUID (foreign key → User)
- amount: decimal
- description: string
- due_date: date
- status: enum (pending, paid, overdue)
- created_at: timestamp

Relations:
- Belongs to: User
```

[Add 3-6 core entities that define your domain model]

### Database Schema Notes

[Any important notes about schema design:]
- Indexes: [What's indexed and why]
- Constraints: [Important constraints or validations]
- Cascading rules: [What happens on delete, etc.]

---

## API Design

### Endpoint Structure

[Document your API conventions:]

**Example**:
```
Base URL: /api/v1

Authentication:
- All endpoints except /auth/* require Bearer token
- Token in Authorization header: "Bearer {token}"

Response Format:
- Success: { success: true, data: {...} }
- Error: { success: false, error: { code: "...", message: "..." } }
```

### Key Endpoints

[Document critical endpoints:]

**Authentication**:
- `POST /api/v1/auth/register` - Create new user
- `POST /api/v1/auth/login` - Login, returns JWT token
- `POST /api/v1/auth/logout` - Invalidate token (if applicable)

**[Resource 1]**:
- `GET /api/v1/invoices` - List user's invoices (paginated)
- `POST /api/v1/invoices` - Create new invoice
- `GET /api/v1/invoices/:id` - Get single invoice
- `PATCH /api/v1/invoices/:id` - Update invoice
- `DELETE /api/v1/invoices/:id` - Delete invoice

[Add key endpoint groups]

---

## Request/Response Flows

### Critical User Flows

**[Flow Name 1]**: User Login
```
1. User submits email/password
2. Frontend: POST /api/v1/auth/login
3. Backend: Validate credentials, hash password check
4. Backend: Generate JWT token (expires 7 days)
5. Backend: Return { token, user: {...} }
6. Frontend: Store token in localStorage
7. Frontend: Redirect to dashboard
```

**[Flow Name 2]**: Creating an Invoice
```
1. User fills invoice form
2. Frontend: Validate with Zod schema
3. Frontend: POST /api/v1/invoices with data
4. Backend: Authenticate request (verify JWT)
5. Backend: Validate data (Zod/Joi)
6. Backend: Create database record
7. Backend: Return created invoice
8. Frontend: Update local state, show success
```

[Add 3-5 critical flows that define your application]

---

## Security Considerations

**Authentication & Authorization**:
- [How are passwords stored? e.g., bcrypt with 12 rounds]
- [Token expiration strategy]
- [How are protected routes guarded?]

**Input Validation**:
- [Client-side and server-side validation strategy]
- [How are you preventing injection attacks?]

**Data Protection**:
- [Are sensitive fields encrypted at rest?]
- [What data is logged? Any PII concerns?]

**API Security**:
- [CORS configuration]
- [Rate limiting strategy (if any)]
- [CSRF protection (if using cookies)]

---

## Performance Considerations

**Target Metrics**:
- Page load time: [e.g., <3s on 3G]
- API response time: [e.g., <200ms for read operations]
- Database query time: [e.g., <50ms for primary queries]

**Optimization Strategies**:
- [Caching strategy, if any]
- [Pagination approach for large lists]
- [Image optimization approach]
- [Code splitting strategy]

---

## Development Environment Setup

### Prerequisites
```bash
# List required software and versions
- Node.js 20+
- PostgreSQL 15+
- npm or yarn
```

### Initial Setup
```bash
# Clone and install
git clone [repo-url]
cd [project-name]
npm install

# Environment configuration
cp .env.example .env
# Edit .env with local values

# Database setup
npm run db:migrate
npm run db:seed  # if you have seed data
```

### Running Locally
```bash
# Start database (if using Docker)
docker-compose up -d postgres

# Start backend
npm run dev:backend  # typically on :3000 or :5000

# Start frontend (in another terminal)
npm run dev:frontend  # typically on :5173 or :3000
```

---

## Testing Strategy

**Unit Tests**:
- [What gets unit tested? e.g., "All business logic in services/"]
- [Testing framework: e.g., Jest, Vitest, pytest]

**Integration Tests**:
- [What integration points are tested? e.g., "API endpoints"]
- [Tools: e.g., Supertest, Playwright API testing]

**E2E Tests** (if applicable):
- [Critical user flows to test]
- [Tools: e.g., Playwright, Cypress]

**Test Coverage Goals**:
- [Coverage target, e.g., "80% for business logic, not required for UI components"]

---

## Deployment Architecture

**Hosting**:
- Frontend: [Where and how? e.g., "Vercel, auto-deploys from main branch"]
- Backend: [Where and how? e.g., "Railway, manual deploys"]
- Database: [Where? e.g., "Supabase managed PostgreSQL"]

**Environment Variables**:
- [List critical env vars and where they're configured]
- DATABASE_URL
- JWT_SECRET
- API_BASE_URL
- [etc.]

**Build Process**:
```bash
# Frontend build
npm run build:frontend  # outputs to dist/

# Backend build (if TypeScript)
npm run build:backend   # outputs to dist/
```

**Deployment Steps**:
1. [Step-by-step deployment process]
2. [Any manual steps required]
3. [How to verify deployment success]

---

## Open Technical Questions

[Track technical decisions that need to be made:]

1. **[Question 1]**: Should we implement soft deletes or hard deletes for user data?
   - **Options**: Soft delete (add deleted_at field) vs hard delete
   - **Trade-offs**: [List trade-offs]
   - **Decision needed by**: [Date or milestone]

2. **[Question 2]**: What's the pagination strategy for large invoice lists?
   - **Options**: Offset-based vs cursor-based
   - **Trade-offs**: [List trade-offs]

[When resolved, move the decision to "Key Decisions" section in CLAUDE.md]

---

## Future Considerations (Post-MVP)

[Technical improvements or features deferred for later:]

- **Caching layer**: Add Redis for frequently accessed data
- **Real-time updates**: WebSocket support for live notifications
- **File processing**: Background job queue for large file uploads
- **Monitoring**: Sentry for error tracking, DataDog for metrics
- **Search**: Elasticsearch for full-text search across invoices

---

## Changelog

Track significant architectural changes over time.

### [Date] - [Change Summary]
**Changed**: [What changed in architecture/design]
**Rationale**: [Why]
**Impact**: [Files/systems affected]

**Example**:
```
### 2025-01-15 - Migrated from REST to tRPC
**Changed**: Replaced Express REST API with tRPC endpoints
**Rationale**: End-to-end type safety, better DX, reduced boilerplate
**Impact**: All API endpoints rewritten, frontend API client updated
```
