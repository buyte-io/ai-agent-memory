# MEMORY.md

**Purpose**: Rolling memory of recent work sessions for TaskFlow project.

**Last Updated**: 2025-01-15
**Last Archived**: Never (initial file)

---

## Active Session History

### Session: 2025-01-09

**Completed Tasks**:
- Initialized git repository
- Set up React + TypeScript frontend with Vite
- Set up Express + TypeScript backend
- Created basic folder structure

**Files Created**:
- `client/` - Frontend app with Vite config
- `server/` - Backend app with Express setup
- `.gitignore`, `package.json` (root, client, server)

**Key Decisions**:
- Using monorepo structure (client + server in one repo)
- Chose Zustand over Redux for state management (simpler)
- Decided on Vite for frontend build tool (faster than CRA)

**Next Steps**:
- Set up Prisma and database schema
- Add ESLint and Prettier

---

### Session: 2025-01-10

**Completed Tasks**:
- Configured Prisma with PostgreSQL
- Created initial database schema (User, Project, Task models)
- Set up ESLint and Prettier for both frontend and backend
- Created .env.example files

**Files Created/Modified**:
- `server/prisma/schema.prisma` - Database schema
- `server/prisma/migrations/` - Initial migration
- `.eslintrc.js`, `.prettierrc` - Linting configs

**Key Decisions**:
- Using UUIDs for primary keys (better for distributed systems)
- Tasks belong to projects, projects belong to users
- Added TeamMember model for project collaboration

**Next Steps**:
- Implement authentication endpoints (register, login)
- Set up JWT middleware

---

### Session: 2025-01-11

**Completed Tasks**:
- Created database migrations for User table
- Added health check endpoint (GET /api/health)
- Verified local development environment works
- Added database indexes on User.email

**Files Created/Modified**:
- `server/routes/health.ts` - Health check endpoint
- `server/index.ts` - Express server setup
- Database migration for users table

**Key Decisions**:
- JWT expiration set to 7 days (no refresh tokens for MVP)
- Unique index on User.email for faster login lookups
- Health endpoint returns { status: 'ok', timestamp } for monitoring

**Problems Encountered**:
- Initial Prisma connection failed due to incorrect DATABASE_URL format
- Resolved by using correct PostgreSQL connection string format

**Next Steps**:
- Implement user registration endpoint
- Implement password hashing with bcrypt

---

### Session: 2025-01-12

**Completed Tasks**:
- Implemented POST /api/v1/auth/register endpoint
- Added password hashing with bcrypt (12 rounds)
- Created Zod validation schemas for registration
- Added user service layer for business logic

**Files Created/Modified**:
- `server/routes/auth.ts` - Auth routes
- `server/controllers/auth-controller.ts` - Request handlers
- `server/services/user-service.ts` - User business logic
- `server/schemas/auth-schemas.ts` - Zod validation

**Key Decisions**:
- Separated controllers (HTTP handling) from services (business logic)
- Using Zod for validation (type-safe, composable)
- Password requirements: min 8 chars, no complexity requirements for MVP

**Next Steps**:
- Implement login endpoint with JWT generation
- Create auth middleware for protected routes

---

### Session: 2025-01-13

**Completed Tasks**:
- Implemented POST /api/v1/auth/login endpoint
- Created JWT token generation logic
- Built authentication middleware for protected routes
- Added GET /api/v1/auth/me endpoint to get current user

**Files Created/Modified**:
- `server/controllers/auth-controller.ts` - Added login handler
- `server/middleware/auth.ts` - JWT verification middleware
- `server/utils/jwt.ts` - Token generation/verification utilities

**Key Decisions**:
- JWT stored in httpOnly cookie (name: 'token', SameSite: Strict)
- Auth middleware attaches user object to req.user for easy access
- Token payload contains: userId, email, issued timestamp

**Problems Encountered**:
- Initially used localStorage for tokens, switched to httpOnly cookies for security
- Had to configure CORS to allow credentials (credentials: true)

**Next Steps**:
- Implement logout endpoint (clear cookie)
- Build frontend login/register pages

---

### Session: 2025-01-14

**Completed Tasks**:
- Implemented POST /api/v1/auth/logout endpoint
- Finalized auth flow testing (register, login, protected routes, logout)
- Created Project and Task database models
- Ran migrations for projects and tasks tables

**Files Created/Modified**:
- `server/controllers/auth-controller.ts` - Added logout handler
- `server/prisma/schema.prisma` - Added Project and Task models
- Database migrations for projects and tasks

**Key Decisions**:
- Logout simply clears the httpOnly cookie (stateless JWT, can't revoke)
- Project deletion cascades to tasks and team members (ON DELETE CASCADE)
- Task assigned_to set to null on user deletion (preserve task history)

**Next Steps**:
- Implement project CRUD endpoints
- Implement task CRUD endpoints
- Start building frontend login/register UI

---

### Session: 2025-01-15

**Completed Tasks**:
- Code review of authentication implementation
- Updated documentation (ARCHITECTURE.md, TASKS.md)
- Verified all completed tasks are marked in TASKS.md

**Key Decisions**:
- Ready to start frontend UI implementation next
- Backend auth and models are solid foundation

**Next Steps**:
- Build frontend registration and login pages
- Set up Zustand store for auth state
- Create protected route wrapper component

---

**Note**: This file contains the last 7 sessions. When it reaches 15+ sessions, the oldest ones will be moved to `docs/memory-archive/2025-01.md`.
