# CLAUDE.md

**Purpose**: AI agent behavior contract and project memory for TaskFlow

**Last Updated**: 2025-01-15

---

## Session Protocols (MANDATORY)

### At the Start of Every Session

**ALWAYS execute this checklist before writing any code:**

1. **Read ARCHITECTURE.md** - Understand current architecture and technical decisions
2. **Read TASKS.md** - See what's completed and what's next
3. **Review recent session history below** - Understand what happened in previous sessions
4. **Ask clarifying questions** if requirements are ambiguous

### During Active Development

1. **Use TodoWrite tool** for tracking tasks within the current session
2. **Mark todos complete immediately** after finishing each task
3. **Update TASKS.md** when completing major milestones or discovering new work
4. **Document decisions** in real-time (add to this file or ARCHITECTURE.md)

### Before Ending a Session

**CRITICAL - This is how we maintain memory across sessions:**

1. **Update TASKS.md** - Mark completed tasks with date (e.g., `- [x] Task name (2025-01-15)`)
2. **Append session summary below** - Use the template in "Session History" section
3. **Update ARCHITECTURE.md** - If any architectural decisions or patterns changed
4. **Update this file** - If new conventions, patterns, or important context emerged

---

## Agent Behavior Rules

### Communication Style
- Be concise and direct
- No emojis unless explicitly requested
- Focus on technical accuracy over validation
- Ask clarifying questions when requirements are unclear

### Code References
- Use `file_path:line_number` format when referencing code
- Example: "The auth middleware is at server/middleware/auth.ts:15"

---

## Development Workflow

### Before Writing Code
1. Read relevant files to understand current implementation
2. Plan approach for complex tasks (use TodoWrite)
3. Ask questions if requirements are ambiguous

### When Writing Code
1. **Always prefer editing existing files** over creating new ones
2. Follow existing patterns (see Coding Standards below)
3. Consider security: SQL injection, XSS, auth checks, input validation
4. Write clear, maintainable code

### After Writing Code
1. Test the changes manually
2. Update CLAUDE.md if important patterns emerged
3. Mark related tasks complete in TASKS.md

---

## Tool Usage Guidelines

### File Operations
- Use Read, Edit, Write, Glob, Grep tools (not bash commands)

### Search Strategy
- Broad exploration: Task tool with subagent_type=Explore
- Specific files: Glob tool
- Known locations: Read tool
- Content search: Grep tool

### Bash Tool
- Only for git, npm, testing commands
- Never for file operations or communication

---

## Git Workflow

### Commit Guidelines
- Only commit when explicitly requested
- Clear, concise commit messages (focus on "why")
- End messages with Claude Code attribution
- Use HEREDOC format

---

## Project-Specific Configuration

### Technology Stack
- **Frontend**: React 18.2 + TypeScript + Vite + Tailwind CSS
- **Backend**: Node.js 20 + Express + TypeScript
- **Database**: PostgreSQL 15 (Prisma ORM)
- **Auth**: JWT in httpOnly cookies, bcrypt password hashing

### Development Environment

**Setup**:
```bash
npm install
cd server && npx prisma migrate dev
```

**Run Dev Servers**:
```bash
# Terminal 1 - Backend
cd server && npm run dev  # :5000

# Terminal 2 - Frontend
cd client && npm run dev  # :5173
```

**Tests**:
```bash
# Backend tests
cd server && npm test

# Frontend tests
cd client && npm test
```

**Linting**:
```bash
npm run lint  # Root runs both client and server
```

---

## Coding Standards & Conventions

### File Organization
- Backend: `/server/routes` → `/controllers` → `/services` → `/models` (Prisma)
- Frontend: `/client/src/pages` for routes, `/components` for reusable UI

### Naming Conventions
- Files: kebab-case (`task-card.tsx`, `auth-service.ts`)
- Functions: camelCase, verb-first (`getUserById`, `validateEmail`)
- Components: PascalCase (`TaskCard`, `ProjectList`)
- Constants: UPPER_SNAKE_CASE (`JWT_SECRET`, `TOKEN_EXPIRY`)

### Code Patterns

**Error Handling (Backend)**:
```typescript
try {
  // Operation
} catch (error) {
  return res.status(500).json({
    success: false,
    error: { code: 'INTERNAL_ERROR', message: 'Something went wrong' }
  });
}
```

**API Response Format**:
```typescript
// Success
{ success: true, data: {...} }

// Error
{ success: false, error: { code: 'ERROR_CODE', message: 'User-friendly message' } }
```

**React Query Usage (Frontend)**:
```typescript
const { data, isLoading, error } = useQuery({
  queryKey: ['tasks', 'today'],
  queryFn: () => fetchTodayTasks(),
  staleTime: 5 * 60 * 1000, // 5 minutes
});
```

**Form Handling**:
- Use react-hook-form with Zod validation
- Share Zod schemas between frontend and backend (create shared/ directory)

---

## Critical Requirements

- **All API endpoints** require authentication (except /auth/*)
- **All user inputs** must be validated server-side with Zod
- **All database queries** use Prisma (prevents SQL injection)
- **All passwords** hashed with bcrypt before storage
- **Access control**: Users can only access their own projects/tasks

---

## Key Decisions & Rationale

### 2025-01-09: Zustand for State Management
**Decision**: Use Zustand instead of Redux
**Rationale**: Simpler API, less boilerplate, sufficient for our state needs (user auth, simple UI state)
**Trade-offs**: Less ecosystem/middleware than Redux, but we don't need it

### 2025-01-10: Prisma for Database
**Decision**: Use Prisma ORM
**Rationale**: Type-safe queries, excellent migration system, great DX
**Trade-offs**: Adds abstraction layer, but worth it for type safety

### 2025-01-11: httpOnly Cookies for JWT
**Decision**: Store JWT in httpOnly cookies instead of localStorage
**Rationale**: Prevents XSS attacks from stealing tokens
**Trade-offs**: Can't access token from JavaScript, but that's a feature (security)

---

## Integration Points

- **Supabase PostgreSQL**: Database hosting (connection string in DATABASE_URL env var)
- **Vercel**: Frontend hosting (auto-deploy from main branch)
- **Railway**: Backend hosting (manual deploy initially)

---

## Known Issues & Workarounds

**Issue**: Prisma Client sometimes needs regeneration after schema changes
- **Workaround**: Run `npx prisma generate` after modifying schema.prisma
- **When**: If you see TypeScript errors about missing Prisma types

---

## Resources

- [Prisma Docs](https://www.prisma.io/docs)
- [React Query Docs](https://tanstack.com/query/latest)
- [Shadcn/ui Components](https://ui.shadcn.com/)

---

## Session History → Now in MEMORY.md

**Important**: Session history has been moved to **MEMORY.md** for better scalability.

**For this project**:
- 7 sessions completed (2025-01-09 through 2025-01-15)
- All session summaries are in MEMORY.md
- Backend authentication is complete, frontend UI is next

**Recent highlights**:
- ✅ Full authentication system (register, login, logout, JWT)
- ✅ Database models (User, Project, Task, TeamMember)
- ✅ Prisma ORM with PostgreSQL
- 🔄 Frontend UI implementation in progress

See MEMORY.md for complete session-by-session details.
