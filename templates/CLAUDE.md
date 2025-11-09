# CLAUDE.md

**Purpose**: This file defines AI agent behavior, workflow protocols, and serves as the living memory of this project across sessions.

**Last Updated**: [Date]

---

## How to Fill This Out

**Purpose**: This file defines how AI agents should behave in this project. It contains stable rules and conventions.

**Initial setup** (20-30 minutes):
1. Fill in "Project-Specific Configuration" section (tech stack, commands)
2. Fill in "Coding Standards & Conventions" section
3. Customize behavior rules if needed for your project

**Note on Memory**: Session history is now stored in MEMORY.md (separate file). This keeps CLAUDE.md focused on behavior rules and conventions that don't change often.

**Keep it current**: Update when coding standards, tech stack, or workflows change. This file should be relatively stable once initially configured.

---

## Session Protocols (MANDATORY)

### At the Start of Every Session

**ALWAYS execute this checklist before writing any code:**

1. **Read ARCHITECTURE.md** - Understand current architecture and technical decisions
2. **Read this file (CLAUDE.md)** - Understand behavior rules and coding conventions
3. **Read MEMORY.md** - Review recent session history to understand what happened recently
4. **Read TASKS.md** - See what's completed and what's next
5. **Ask clarifying questions** if requirements are ambiguous

### During Active Development

1. **Use TodoWrite tool** for tracking tasks within the current session
2. **Mark todos complete immediately** after finishing each task
3. **Update TASKS.md** when completing major milestones or discovering new work
4. **Document decisions** in real-time (add to ARCHITECTURE.md or this file)

### Before Ending a Session

**CRITICAL - This is how we maintain memory across sessions:**

1. **Update TASKS.md** - Mark completed tasks with date (e.g., `- [x] Task name (2025-01-09)`)
2. **Append session summary to MEMORY.md** - Use the template format provided in MEMORY.md
3. **Update ARCHITECTURE.md** - If any architectural decisions or patterns changed
4. **Update this file (CLAUDE.md)** - Only if coding standards, conventions, or behavior rules changed
5. **Check if MEMORY.md needs archiving** - If >15 sessions, suggest moving oldest to archive

---

## Agent Behavior Rules

### Communication Style
- Be concise and direct
- No emojis unless explicitly requested by user
- Focus on technical accuracy over validation
- Provide objective guidance even if it contradicts user assumptions
- Ask clarifying questions when requirements are unclear

### Code References
- Use `file_path:line_number` format when referencing code
- Example: "The authentication logic is at src/auth/login.ts:142"

---

## Development Workflow

### Before Writing Code
1. Read relevant files to understand current implementation
2. Use Task tool with subagent_type=Explore for broad codebase exploration
3. Plan approach for complex tasks (use TodoWrite for multi-step work)
4. Ask questions if requirements are ambiguous

### When Writing Code
1. **Always prefer editing existing files** over creating new ones
2. Follow existing patterns and conventions in the codebase
3. Consider security implications:
   - SQL injection, XSS, command injection
   - Authentication and authorization
   - Input validation and sanitization
   - Secure credential handling
4. Write clear, maintainable code matching project style
5. Avoid premature optimization - prioritize readability

### After Writing Code
1. Test the changes (run relevant tests)
2. Update documentation if APIs or behaviors changed
3. Update CLAUDE.md if important patterns or decisions emerged
4. Mark related tasks complete in TASKS.md

---

## Tool Usage Guidelines

### File Operations (Use Specialized Tools)
- **Read** tool for viewing files (NOT `cat`)
- **Edit** tool for modifying files (NOT `sed`/`awk`)
- **Write** tool for creating new files (NOT `echo >` or heredoc)
- **Glob** tool for finding files by pattern (NOT `find`/`ls`)
- **Grep** tool for searching file contents (NOT `grep`/`rg`)

### Search Strategy
- **Broad exploration**: Task tool with subagent_type=Explore
- **Specific file patterns**: Glob tool
- **Known file locations**: Read tool directly
- **Content searches**: Grep tool or Task tool

### Bash Tool (Terminal Operations Only)
- Use for git, npm, docker, build commands, etc.
- **Never** use for file operations (use dedicated tools)
- **Never** use for communication (output text directly in responses)
- Quote file paths with spaces: `cd "path with spaces/file.txt"`

---

## Git Workflow

### Commit Guidelines
- **Only create commits when explicitly requested**
- Write clear, concise commit messages focused on "why" not "what"
- Use HEREDOC format for commit messages
- Always end commits with:
  ```
  🤖 Generated with [Claude Code](https://claude.com/claude-code)

  Co-Authored-By: Claude <noreply@anthropic.com>
  ```
- Never skip hooks (--no-verify) unless explicitly requested
- Never force push to main/master without explicit confirmation

### Pre-commit Hook Handling
- If hooks modify files, check authorship before amending
- Only amend if: (1) user requested it, OR (2) adding hook edits to your own commit
- Never amend other developers' commits

### Pull Request Creation
- Use `gh` CLI for all GitHub operations
- Analyze ALL commits in the branch (not just latest)
- Include comprehensive PR description:
  - Summary (1-3 bullet points)
  - Test plan (bulleted checklist)
  - Claude Code attribution footer
- Use HEREDOC format for PR body

---

## Project-Specific Configuration

### Technology Stack
- **Language/Framework**: [e.g., Python/FastAPI, Node.js/React, PHP/Laravel]
- **Database**: [e.g., PostgreSQL, MySQL, MongoDB]
- **Key Libraries**: [List important dependencies]
- **Build Tools**: [e.g., webpack, vite, make, docker]

### Development Environment

**Setup**:
```bash
# Add setup commands (e.g., npm install, pip install -r requirements.txt)
```

**Run Development Server**:
```bash
# Add dev server command (e.g., npm run dev, python manage.py runserver)
```

**Build**:
```bash
# Add build commands (e.g., npm run build, make build)
```

**Tests**:
```bash
# Run all tests
# Run specific test file
# Run tests in watch mode
```

**Lint/Format**:
```bash
# Linting command
# Formatting command
```

---

## Coding Standards & Conventions

### File Organization
[Describe directory structure conventions, e.g., "Components in src/components/, utilities in src/lib/"]

### Naming Conventions
- **Files**: [e.g., kebab-case for components, camelCase for utilities]
- **Functions**: [e.g., camelCase, verb-first like getUserData]
- **Classes**: [e.g., PascalCase]
- **Constants**: [e.g., UPPER_SNAKE_CASE]

### Code Patterns
[Document important patterns, e.g.:]
- Error handling approach (try/catch, error boundaries, etc.)
- State management patterns
- API call conventions
- Testing patterns

### Module Boundaries
[Describe separation of concerns, e.g.:]
- Business logic in services/
- UI logic in components/
- Shared utilities in lib/
- Types/interfaces in types/

---

## Critical Requirements & Constraints

[Document must-follow rules specific to this project:]

**Example**:
- All API responses must include error codes
- All database queries must use parameterized statements
- All user inputs must be validated server-side
- All external API calls must have timeouts and retry logic

---

## Key Decisions & Rationale

[Document important technical decisions and why they were made:]

**Example**:
```
### 2025-01-09: Chose PostgreSQL over MongoDB
**Decision**: Use PostgreSQL for primary database
**Rationale**: Need for complex relational queries, ACID compliance, and strong community support
**Trade-offs**: Slightly more complex schema migrations, but better data integrity guarantees
```

---

## Integration Points

[Document external APIs, services, or systems:]

**Example**:
- **Stripe API**: Payment processing (uses v3 API, webhooks for async events)
- **SendGrid**: Email notifications (rate limited to 100/hour on free tier)
- **AWS S3**: File storage (bucket: project-uploads-prod)

---

## Known Issues & Workarounds

[Document quirks, gotchas, or temporary workarounds:]

**Example**:
- **Issue**: Library X has memory leak in version 2.3.x
  - **Workaround**: Pinned to version 2.2.5 until upstream fix
  - **Tracking**: GitHub issue #123

---

## Resources & Documentation

- [Link to API documentation]
- [Link to design system/UI kit]
- [Link to architecture diagrams]
- [Link to deployment docs]

---

## Session History → Now in MEMORY.md

**Important Change**: Session history is now stored in a separate file called **MEMORY.md**.

**Why the change?**
- Separates stable behavior rules (this file) from growing session history (MEMORY.md)
- Keeps CLAUDE.md lean and focused on conventions
- MEMORY.md uses a rolling window (last 10-15 sessions) with archiving
- Better scalability for long-running projects

**For AI Agents**:
- Session summaries should be appended to MEMORY.md, not this file
- Read MEMORY.md at session start for recent project context
- See MEMORY.md for the session summary template format
- This file (CLAUDE.md) should only be updated when behavior rules or conventions change
