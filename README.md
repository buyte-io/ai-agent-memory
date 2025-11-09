# AI Agent Memory SOP

A simple, battle-tested framework for giving AI coding agents (Claude, ChatGPT, Cursor, etc.) persistent memory and context across sessions.

---

## TL;DR

**The Problem**: AI agents forget everything between sessions.

**The Solution**: 5 markdown files in your repo that create persistent memory:
- `PROJECT.md` - What you're building
- `ARCHITECTURE.md` - How it's built
- `CLAUDE.md` - AI behavior rules
- `MEMORY.md` - Session history (the memory)
- `TASKS.md` - What's next

**The Magic**: Append session summaries to MEMORY.md after each work session. Next session, the AI reads them and remembers everything.

**Time Investment**: 15 min setup (with bootstrap), 2 min per session to maintain.

---

## Table of Contents

- [The Problem](#the-problem)
- [The Solution](#the-solution)
- [Quick Start](#quick-start)
  - [Bootstrap Approach (15 min)](#bootstrap-approach-recommended)
  - [Manual Approach (60 min)](#manual-approach-for-learning)
- [The 5 Files Explained](#the-5-files-explained)
- [Daily Workflow](#daily-workflow)
- [Key Principles](#key-principles)
- [Common Mistakes & Pro Tips](#common-mistakes--pro-tips)
- [Advanced Tips](#advanced-tips)
- [Troubleshooting](#troubleshooting)
- [For Existing Projects](#for-existing-projects)
- [Template Structure](#template-structure)
- [Why This Works](#why-this-works)
- [Credits](#credits--further-reading)

---

## The Problem

AI coding assistants are stateless. Every new session starts from zero:
- You re-explain your project architecture
- The AI forgets what you built yesterday
- Context is lost when conversations get long
- You waste time repeating yourself
- Inconsistent coding patterns emerge

## The Solution

**Five markdown files** that live in your repo root. The AI reads these at the start of every session:

1. **PROJECT.md** - What you're building and why (strategy layer)
2. **ARCHITECTURE.md** - Technical architecture and decisions (technical layer)
3. **CLAUDE.md** - How the AI should behave (behavior layer)
4. **MEMORY.md** - Recent session history (memory layer)
5. **TASKS.md** - What's done and what's next (operational layer)

These files give AI agents:
- Persistent memory via rolling session history
- Clear context without re-explaining
- Consistent behavior and coding standards
- Institutional knowledge that accumulates
- Scalability through memory archiving

---

## Quick Start

### Two Ways to Start

**🤖 Bootstrap Approach (Recommended)** - 15 minutes total
- Gather client briefs, requirements, or notes
- Feed to AI with bootstrap prompt
- AI generates all 5 docs from your content
- Review and refine
- Start coding

**✋ Manual Approach** - 60 minutes total
- Copy templates to your project
- Fill out each file manually
- Good for learning the structure first

**Most people should use Bootstrap.** Manual is only if you want to understand the structure deeply first.

---

## Bootstrap Approach (Recommended)

**The Real-World Workflow**: Don't manually fill out docs. Let AI generate them from your existing content (briefs, notes, requirements).

### The Bootstrap Process

Instead of spending 60 minutes manually filling out 5 files, spend 10 minutes gathering content and let AI generate structured docs in 5 minutes.

**Typical Flow:**
1. **Gather** - Collect client briefs, requirements, notes, ideas (5 min)
2. **Bootstrap** - Feed to AI with generation prompt (2 min)
3. **Review** - Check generated docs, iterate if needed (5-10 min)
4. **Code** - Start development with perfect context (immediate)

**Total time**: 15-20 minutes vs 60 minutes manual

---

### Step 1: Choose Your Scenario (2 min)

Pick the scenario that matches your situation and use the copy-paste prompt below.

#### Scenario A: Client Brief + Your Notes

**You have**: Client brief, your technical notes, maybe some architecture ideas

**Copy-paste this prompt:**

```
I'm starting a new project and need to generate the 5 core documentation files
for AI agent memory (PROJECT.md, ARCHITECTURE.md, CLAUDE.md, MEMORY.md, TASKS.md).

I'll provide you with all the raw content I have. Please generate structured,
professional documentation following the templates in this repository.

=== CLIENT BRIEF ===
[Paste client brief here]

=== MY TECHNICAL NOTES ===
[Paste your technical thoughts, architecture ideas, stack preferences]

=== ADDITIONAL CONTEXT ===
[Any other relevant info - timeline, constraints, team size, etc.]

Please generate:
1. PROJECT.md - Extract vision, problem, users, stories, success criteria
2. ARCHITECTURE.md - Propose tech stack, data models, API design based on requirements
3. CLAUDE.md - Fill in with the proposed stack and standard conventions
4. MEMORY.md - Leave empty (will populate during work sessions)
5. TASKS.md - Break down the work into milestones and atomic tasks

Use the templates from this repository as the format guide. Be specific and
actionable - these docs will guide the entire development process.
```

---

#### Scenario B: Existing Draft Documents

**You have**: Rough docs you've started, need them structured properly

**Copy-paste this prompt:**

```
I have draft documentation for a project that needs to be structured into
the 5-file AI agent memory system (PROJECT.md, ARCHITECTURE.md, CLAUDE.md,
MEMORY.md, TASKS.md).

Please restructure my existing content into the proper format using the
templates from this repository.

=== MY DRAFT CONTENT ===
[Paste your existing docs, notes, outlines - all together or separately]

Please:
1. Extract strategic content → PROJECT.md
2. Extract technical details → ARCHITECTURE.md
3. Create behavior/convention rules → CLAUDE.md
4. Leave MEMORY.md empty (for future sessions)
5. Break work into milestones → TASKS.md

Fill in any gaps with reasonable assumptions (I'll refine them next).
```

---

#### Scenario C: Starting from Scratch

**You have**: Just an idea and maybe some rough notes

**Copy-paste this prompt:**

```
I'm starting a new project from scratch and need help generating the 5 core
documentation files (PROJECT.md, ARCHITECTURE.md, CLAUDE.md, MEMORY.md, TASKS.md).

=== PROJECT IDEA ===
[Describe what you want to build - 2-3 paragraphs minimum]

=== CONSTRAINTS/PREFERENCES ===
- Timeline: [e.g., "MVP in 4 weeks"]
- Tech preferences: [e.g., "React + Node.js, prefer TypeScript"]
- Team: [e.g., "Solo developer"]
- Deployment: [e.g., "Vercel for frontend, Railway for backend"]

=== TARGET USERS ===
[Who will use this? What problems do they have?]

Please generate all 5 documentation files using the templates in this repository.
Make reasonable technical choices based on the requirements, and I'll refine them.

Be specific about:
- Tech stack and why
- Data models
- API design
- Milestones and tasks
```

---

#### Scenario D: Client Requirements Document

**You have**: Formal requirements doc, spec, or RFP

**Copy-paste this prompt:**

```
I have a client requirements document that needs to be transformed into the
5-file AI agent memory system for development.

=== REQUIREMENTS DOCUMENT ===
[Paste the entire requirements doc, spec, or RFP]

=== MY TECHNICAL APPROACH ===
[Optional: Add your technical preferences, stack choices, architecture ideas]

Please generate:
1. PROJECT.md - Extract and structure the requirements professionally
2. ARCHITECTURE.md - Propose a complete technical architecture
3. CLAUDE.md - Standard setup with the proposed tech stack
4. MEMORY.md - Leave empty
5. TASKS.md - Break requirements into development milestones and atomic tasks

Use the templates from this repository. Flag any ambiguities or missing
information that I need to clarify with the client.
```

---

### Step 2: Review & Refine (5-10 min)

After AI generates the docs, review each one. Use these prompts to refine:

#### Refining PROJECT.md

```
Review PROJECT.md and improve it:

1. Is the vision clear and compelling?
2. Are user personas specific enough?
3. Are user stories actionable?
4. Are success metrics measurable?
5. Is scope clearly defined?

Suggest improvements or ask me clarifying questions.
```

#### Refining ARCHITECTURE.md

```
Review ARCHITECTURE.md and validate technical choices:

1. Is the tech stack appropriate for this project?
2. Are data models complete and normalized?
3. Are API endpoints well-designed?
4. Are security considerations addressed?
5. Is the development setup clear?

Flag any technical risks or alternative approaches I should consider.
```

#### Refining TASKS.md

```
Review TASKS.md and check:

1. Are tasks atomic (completable in one session)?
2. Are milestones logical and value-focused?
3. Is anything missing from the breakdown?
4. Are task descriptions specific enough?

Suggest improvements to the task breakdown.
```

#### Common Refinement Iterations

**"The docs are too generic"**
```
These docs feel generic. Let me provide more context:

[Add specific details about your domain, users, technical environment]

Please make the docs more specific to this particular project.
```

**"The tech stack doesn't feel right"**
```
I'm not confident about the proposed tech stack. Let's discuss:

- Concerns: [What worries you?]
- Alternatives: [What are you considering?]
- Constraints: [What limitations do you have?]

Help me choose the right stack for this specific project.
```

**"The tasks are too vague"**
```
The tasks in TASKS.md are too high-level. Please break them down further.

For example, instead of "Implement authentication", I need:
- Create user registration endpoint
- Add password hashing with bcrypt
- Create login endpoint with JWT
- etc.

Apply this level of detail to all milestones.
```

---

### Step 3: Finalize & Save (2 min)

Once you're happy with the docs:

#### Finalization Prompt

```
The documentation looks good. Please:

1. Do a final consistency check across all 5 files
2. Ensure terminology is consistent
3. Verify all cross-references are correct
4. Confirm no contradictions between files
5. Make sure CLAUDE.md has all necessary project-specific info

Then create the 5 final .md files ready to save.
```

#### Output Files Prompt

```
Please output each file in a code block so I can copy-paste them:

1. PROJECT.md - the complete file
2. ARCHITECTURE.md - the complete file
3. CLAUDE.md - the complete file
4. MEMORY.md - the empty template
5. TASKS.md - the complete file

Format each as a markdown code block with the filename.
```

#### Bootstrap Checklist

Before starting your first coding session, verify:

- [ ] PROJECT.md clearly defines what and why
- [ ] ARCHITECTURE.md has specific tech stack and data models
- [ ] CLAUDE.md has project-specific commands (how to run locally, test, etc.)
- [ ] TASKS.md has atomic tasks (completable in one session)
- [ ] All files are consistent with each other
- [ ] No placeholder text like "TODO" or "TBD"
- [ ] You understand and agree with all technical choices

**If any checkbox fails, refine that file before coding.**

---

### Step 4: Start Coding (immediate)

After docs are saved to your repo:

```
Great! The documentation is now in place. Let's start development.

Read PROJECT.md, ARCHITECTURE.md, CLAUDE.md, and TASKS.md to understand
the project. Then complete the first uncompleted task in TASKS.md.

Follow all protocols in CLAUDE.md and update TASKS.md as you complete tasks.
```

---

### Complete Bootstrap Example

#### 1. You Prepare (5 minutes)

```
Client Email:
"We need a tool for our sales team to track leads. Currently using
spreadsheets. Need something simple - add leads, track status, see
pipeline. 20 users max. Budget-conscious."

Your Notes:
- Simple CRM, not complex
- Tech: React + Node probably
- Use Supabase (free tier works for 20 users)
- MVP: 3-4 weeks
- Must have: lead list, status updates, basic pipeline view
```

#### 2. You Run Bootstrap Prompt (2 minutes)

```
I'm starting a new project and need to generate the 5 core documentation files.

=== CLIENT BRIEF ===
Client needs a simple CRM for their sales team (20 users). Currently using
spreadsheets. Need to track leads, update status, view pipeline. Budget-conscious.

=== MY TECHNICAL NOTES ===
- Keep it simple - not a full CRM, just lead tracking
- Tech stack: React + TypeScript, Node.js backend, Supabase (free tier)
- Must be responsive (sales team on mobile)
- MVP timeline: 3-4 weeks
- Core features: add leads, edit status, pipeline view, simple search
- No integrations needed (at least not for MVP)

Please generate all 5 documentation files (PROJECT.md, ARCHITECTURE.md,
CLAUDE.md, MEMORY.md, TASKS.md) using the templates in this repository.
```

#### 3. AI Generates Docs (2 minutes)

AI creates structured, professional documentation.

#### 4. You Review & Refine (5 minutes)

```
Review PROJECT.md - are the user personas realistic for a sales team?
```

```
Check ARCHITECTURE.md - is Supabase the right choice here? What about
scaling beyond 20 users later?
```

#### 5. Finalize & Save (2 minutes)

```
Looks good! Output all 5 files in markdown code blocks so I can save them.
```

#### 6. Start Coding (immediate)

```
Read PROJECT.md, ARCHITECTURE.md, CLAUDE.md, and TASKS.md.
Then complete the first uncompleted task in TASKS.md.
```

---

### Bootstrap Pro Tips

#### For Client Projects

**Before the bootstrap prompt:**
1. Clarify any ambiguities with the client first
2. Gather all relevant documents (briefs, mockups, existing specs)
3. Note any technical constraints (must use X, can't use Y)

**Include in prompt:**
- Client industry/context
- Compliance requirements (HIPAA, GDPR, etc.)
- Integration needs
- Timeline and budget constraints

#### For Personal Projects

**Be specific about:**
- What problem you're solving (even if just for yourself)
- Minimum viable features (resist feature creep in docs)
- Time you can realistically commit
- Learning goals (trying new tech?)

#### For Team Projects

**Include:**
- Team size and skill levels
- Existing codebase (if adding to existing project)
- Team coding standards and preferences
- Deployment infrastructure already in place

---

## Manual Approach (For Learning)

If you prefer to fill out templates manually to understand the structure deeply:

### Step 1: Copy Templates

```bash
# Navigate to your project directory
cd /path/to/your-project

# Copy all template files from this repo
cp /path/to/AgentDocsSOP/templates/*.md .

# Or download from GitHub
# wget https://raw.githubusercontent.com/.../templates/PROJECT.md
# (repeat for all 5 files)
```

You should now have 5 files in your project root:
- `PROJECT.md`
- `ARCHITECTURE.md`
- `CLAUDE.md`
- `MEMORY.md`
- `TASKS.md`

---

### Step 2: Fill Out the 5 Files (30-60 min)

#### PROJECT.md (20 min)
1. Write your one-sentence vision
2. Describe the problem you're solving
3. List 2-3 user personas
4. Write 5-8 user stories
5. Define success criteria

**Tip**: Keep it focused on MVP. Don't dream big yet.

#### ARCHITECTURE.md (30 min)
1. List your tech stack (frontend, backend, database)
2. Describe your data models (users, main entities)
3. List key API endpoints
4. Add development setup commands

**Tip**: Fill out the "essential" sections first, skip optional ones.

#### CLAUDE.md (15 min)
1. Fill in "Technology Stack" section (copy from ARCHITECTURE.md)
2. Fill in "Development Environment" commands (how to run locally)
3. Fill in "Coding Standards" (file naming, patterns, etc.)

**Tip**: This file stays relatively stable once configured.

#### MEMORY.md (skip for now)
- Leave this file empty initially
- It will grow as you complete work sessions
- AI appends session summaries here automatically

**Tip**: This is your rolling memory - starts empty, grows over time.

#### TASKS.md (15 min)
1. Break work into 5-8 milestones
2. List 5-10 atomic tasks per milestone
3. Mark any completed tasks with dates

**Tip**: Use the milestone templates provided as a starting point.

---

### Step 3: Start Your First AI Session

Copy-paste this prompt to your AI agent:

```
Read ARCHITECTURE.md, CLAUDE.md, and TASKS.md to understand the project,
then complete the first uncompleted task in TASKS.md.
```

The AI will:
1. Read all files (MEMORY.md is empty, so skips it)
2. Understand your project context
3. See what task to work on
4. Start coding with full context

---

### Step 4: End Your First Session

Before closing the conversation, copy-paste:

```
Add a session summary to MEMORY.md documenting what we completed today,
files modified, key decisions, and next steps.
```

The AI will append a summary to MEMORY.md using the template format.

**This is the magic step.** The session summary creates persistent memory.

---

### Step 5: Start Your Next Session (Days/Weeks Later)

Copy-paste this prompt:

```
Read ARCHITECTURE.md, CLAUDE.md, MEMORY.md, and TASKS.md to understand the project,
then continue with the next uncompleted task.
```

Watch the AI:
1. Read recent session history from MEMORY.md
2. Remember what happened last time
3. Pick up exactly where you left off
4. Continue coding with zero re-explanation

---

## The 5 Files Explained

### 1. PROJECT.md (Project Overview)

**Purpose**: Strategic anchor - the "why" and "what"

**Contents**:
- Vision (one sentence)
- Problem statement
- Target users (2-3 personas)
- User stories
- Success criteria
- Scope boundaries

**Update frequency**: Rarely (only when scope or vision changes)

**Why it matters**: Keeps technical decisions aligned with product goals. When you're unsure about implementation choices, refer back to PROJECT.md.

### 2. ARCHITECTURE.md (Technical Architecture)

**Purpose**: Current technical reality - the "how it's built"

**Contents**:
- Architecture overview
- Technology stack with rationale
- Data models and database schema
- API design and key endpoints
- Request/response flows
- Security and performance considerations
- Development environment setup
- Testing strategy
- Deployment architecture

**Update frequency**: When architecture changes or major technical decisions are made

**Why it matters**: Single source of truth for how the system works. Prevents the AI from making assumptions or inventing architecture.

### 3. CLAUDE.md (AI Behavior Contract)

**Purpose**: Defines HOW the AI should behave

**Contents**:
- Session protocols (what to read at start, what to update at end)
- Behavior rules and communication style
- Tool usage guidelines
- Git workflow and commit standards
- Project-specific configuration (tech stack, dev commands)
- Coding standards and conventions

**Update frequency**: Rarely (only when behavior rules or conventions change)

**Why it matters**: Ensures consistent AI behavior and coding standards. This file stays relatively stable once configured.

### 4. MEMORY.md (Session History)

**Purpose**: Rolling window of recent work sessions

**Contents**:
- Last 10-15 session summaries
- What was completed, files changed, decisions made
- Problems encountered and solutions
- Next steps from each session

**Update frequency**: Every session (append new summary, archive when >15 sessions)

**Why it matters**: This is your persistent memory. Session summaries accumulate here. The AI reads this at session start and picks up exactly where you left off. Old sessions get archived to keep the file manageable.

### 5. TASKS.md (Work Checklist)

**Purpose**: Operational momentum - what's done and what's next

**Contents**:
- Milestone-organized task list
- Atomic, actionable tasks
- Completed tasks with dates
- Backlog for future work
- Blocked/waiting tasks

**Update frequency**: Constantly (mark complete, add new tasks as discovered)

**Why it matters**: The AI knows exactly what to work on next. Creates visible progress. Completed tasks with dates build a historical record.

---

## Daily Workflow

### Starting a Session

```
Read ARCHITECTURE.md, CLAUDE.md, MEMORY.md, and TASKS.md to understand the project.
Then work on [specific task or "the next uncompleted task"].
```

The AI will:
1. Load architectural context from ARCHITECTURE.md
2. Read behavior rules and conventions from CLAUDE.md
3. Review recent session history in MEMORY.md
4. Check TASKS.md for progress and next steps
5. Start working with full context

### During Development

- AI tracks progress using its TodoWrite tool
- When tasks complete, AI marks them in TASKS.md with dates
- Important decisions get documented in real-time
- New tasks get added to TASKS.md as discovered

### Ending a Session

```
Add a session summary to MEMORY.md with what we completed,
files modified, key decisions, and next steps.
```

The AI appends a structured summary to MEMORY.md:
- Completed tasks
- Files created/modified
- Key decisions and rationale
- Problems encountered and solutions
- Next steps

**This session summary is what creates memory.** The next session starts by reading MEMORY.md and remembers everything.

### Memory Archiving

When MEMORY.md gets >15 sessions:

```
Move the oldest 10 sessions from MEMORY.md to docs/memory-archive/YYYY-MM.md
and keep the most recent 5-10 in MEMORY.md.
```

---

## Key Principles

### 1. Separation of Concerns

Each file has a distinct purpose:
- **PROJECT** = Strategy (why/what)
- **ARCHITECTURE** = Technical Reality (how it's built)
- **CLAUDE** = Behavior (how to work)
- **MEMORY** = History (what happened)
- **TASKS** = Operations (what's next)

No overlap, no confusion.

### 2. Session History as Memory

MEMORY.md is the magic:
- Rolling window of last 10-15 sessions
- Appended chronologically after each session
- New sessions start by reading recent history
- Old sessions archived monthly to keep file manageable
- Captures decisions, problems, and context that would otherwise be lost

### 3. Living Documents

These aren't write-once files:
- MEMORY.md updates every session (append summary)
- TASKS.md updates constantly (mark complete, add new)
- ARCHITECTURE.md updates when architecture evolves
- PROJECT.md updates when scope changes (with dated changelog)
- CLAUDE.md rarely updates (only when conventions change)

### 4. Atomic Tasks

Tasks in TASKS.md must be:
- Completable in one focused session (30-90 min)
- Specific and actionable (start with verbs)
- Independent when possible
- Marked complete immediately with dates

### 5. Works with Any AI

This framework isn't Claude-specific:
- ChatGPT can read these files
- Cursor/Copilot can use them as context
- Human developers benefit from the documentation
- The protocol is universal

---

## Common Mistakes & Pro Tips

### ❌ Mistakes to Avoid

**1. Forgetting to append session summaries**
- Most common mistake: ending sessions without updating MEMORY.md
- Result: Memory doesn't persist, defeats the purpose
- Fix: Make it a habit - last thing before closing

**2. Writing vague tasks**
- Bad: "Handle authentication"
- Good: "Implement JWT token generation in auth/jwt.ts"
- Tasks should be completable in one session

**3. Letting docs get stale**
- ARCHITECTURE.md should reflect current reality, not plans
- Update it when you change architecture, not later
- Stale docs cause AI confusion

**4. Over-documenting**
- Don't write a novel - be concise
- AI reads these files at the start of every session
- Shorter = faster context loading = better

**5. Not reading recent session history**
- The AI should read MEMORY.md at session start
- This is where the memory lives
- Make sure to include it in your session start prompt

### ✅ Pro Tips

**1. Use Bootstrap for new projects**
- Don't manually fill out docs - let AI generate them
- Use the bootstrap prompts above
- Saves 40+ minutes per project
- More accurate (AI structures your thoughts)

**2. Use consistent session start prompts**
```
Read ARCHITECTURE.md, CLAUDE.md, MEMORY.md, and TASKS.md.
Then work on [specific task].
```

**3. Archive old session history when it gets long**
- Keep last 10-15 sessions in MEMORY.md
- Move older ones to `docs/memory-archive/YYYY-MM.md`
- Link to archive at top of MEMORY.md if needed

**4. Update TASKS.md in real-time**
- When AI completes tasks, mark them immediately with dates
- Don't batch updates - you'll forget details

**5. Reference file locations**
- Format: `file_path:line_number`
- Example: "Auth logic is in server/auth.ts:45"
- Makes it easy for AI (and humans) to find code

**6. For solo devs: Keep it lean**
- You don't need every section filled out
- MVP projects can skip enterprise sections
- Scale documentation as project grows

**7. For teams: Use MEMORY.md for collaboration**
- Everyone adds session summaries to MEMORY.md
- New developers read MEMORY.md to see recent work
- Becomes living team knowledge base

**8. When switching AI tools**
- Same docs work across Claude, ChatGPT, Cursor, etc.
- Just adjust the session start prompt slightly
- The framework is AI-agnostic

---

## Advanced Tips

### For Complex Projects

- Create subdirectory docs for detailed technical specs
- Link to them from ARCHITECTURE.md
- Keep the 5 core files concise and scannable

### When Context Gets Stale

If the AI seems confused:
1. Check if ARCHITECTURE.md reflects current reality
2. Review recent session summaries in MEMORY.md
3. Tighten behavior rules in CLAUDE.md
4. Break down tasks into smaller atomic units

### Handling Long Session Histories

When MEMORY.md session history gets very long:
- Archive old sessions to `docs/memory-archive/YYYY-MM.md`
- Keep last 10-15 sessions in MEMORY.md
- Add a link to the archive at the top if needed

### Team Collaboration

These files help human teams too:
- New developers onboard faster
- Decisions are documented with rationale
- Architecture is explicit, not tribal knowledge
- Task progress is visible to everyone

---

## Troubleshooting

### Bootstrap-Specific Issues

**AI-generated docs are too long:**
```
These docs are too verbose. Please condense each file to be more concise
while keeping all essential information.
```

**AI-generated docs are too short:**
```
These docs need more detail. Expand ARCHITECTURE.md with complete data models
and API endpoint definitions. Expand TASKS.md with more granular tasks.
```

**Stack choices seem odd:**
```
Why did you choose [technology X]? What are the trade-offs vs [technology Y]?
I'm leaning toward [technology Z] because [reason].
```

**Not sure if ready to start coding:**
```
Review all 5 files and tell me if anything is missing or unclear before I
start development. Flag any decisions that need my input.
```

### General Issues

**AI seems confused about the project:**
- Check if ARCHITECTURE.md reflects current reality
- Make sure session summaries are being added to MEMORY.md
- Tell the AI explicitly: "Review recent session history in MEMORY.md"

**AI doesn't remember previous sessions:**
- Did you add a session summary last time?
- Is the session history in MEMORY.md?
- Are you telling the AI to read MEMORY.md at session start?

**Docs feel overwhelming:**
- Start minimal, grow over time
- PROJECT.md can be 1 page for MVP
- ARCHITECTURE.md can skip optional sections initially
- TASKS.md just needs a few milestones to start

---

## For Existing Projects

Adding this framework to an existing project:

1. Start by creating PROJECT.md (document what you've already built)
2. Create ARCHITECTURE.md (document current architecture)
3. Create CLAUDE.md (define behavior and conventions)
4. Create MEMORY.md (add initial entry: "Project documented on [date]")
5. Create TASKS.md (list remaining work)

Then follow the standard workflow for all future sessions.

---

## Template Structure

This repository contains:

```
AgentDocsSOP/
├── README.md              (this file - complete guide)
├── templates/
│   ├── PROJECT.md        (template with examples and instructions)
│   ├── ARCHITECTURE.md   (template with architecture sections)
│   ├── CLAUDE.md         (template with behavior rules and protocols)
│   ├── MEMORY.md         (template for session history with archiving)
│   └── TASKS.md          (template with milestone organization)
└── example-project/      (filled-in examples showing usage)
    ├── PROJECT.md
    ├── ARCHITECTURE.md
    ├── CLAUDE.md
    ├── MEMORY.md
    └── TASKS.md
```

---

## Why This Works

### For the AI

- Eliminates ambiguity about project context
- Provides explicit behavior rules
- Creates retrievable memory via session logs
- Reduces hallucination and assumption-making
- Enables consistent coding patterns

### For You

- No more re-explaining your project every session
- Visible progress tracking
- Documentation that stays current
- Decisions captured with rationale
- Calmer, more productive development cadence

### The Compound Effect

As sessions accumulate:
- MEMORY.md becomes a rich project history
- ARCHITECTURE.md captures architectural evolution
- TASKS.md shows momentum and progress
- PROJECT.md anchors all decisions to user value
- CLAUDE.md ensures consistency in how work gets done

You build **institutional knowledge** even though the AI is stateless.

---

## Credits & Further Reading

This framework is based on the "Simple 4-Part Framework" for working with AI coding assistants, expanded to a 5-file system with separated memory for better scalability.

**Core Principles**:
- PROJECT.md for strategic alignment
- ARCHITECTURE.md for technical truth
- CLAUDE.md for behavior consistency
- MEMORY.md for session history (rolling window)
- TASKS.md for operational momentum

Together, they simulate persistent memory and institutional knowledge in a stateless AI environment.

---

**Ready to start?** Copy the templates from `templates/` or use the Bootstrap approach above. Experience AI agents that remember everything! 🚀
