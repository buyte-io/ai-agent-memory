# MEMORY.md

**Purpose**: Rolling memory of recent work sessions. This is where AI agents find context about what happened recently.

**Last Updated**: [Date]

---

## How This File Works

**What is this?**
- This file stores the last 10-15 session summaries
- It's a "rolling window" of recent project history
- AI agents read this at the start of each session to understand recent context

**Why separate from CLAUDE.md?**
- CLAUDE.md contains stable behavior rules and conventions
- MEMORY.md contains growing session history that changes constantly
- Separation keeps CLAUDE.md lean and MEMORY.md focused on recency

**Archiving Strategy:**
- Keep last 10-15 sessions in this file
- When it grows beyond 15 sessions, move oldest 10 to `docs/memory-archive/YYYY-MM.md`
- Keep most recent 5-10 sessions here
- Archive files are searchable when you need to reference old decisions

---

## Active Session History

**Format for each session** (append new sessions at the end):

```markdown
### Session: YYYY-MM-DD

**Completed Tasks**:
- [Task 1 with brief description]
- [Task 2]

**Files Created/Modified**:
- `path/to/file.ts` - [What changed]
- `path/to/other.ts` - [What changed]

**Key Decisions**:
- [Decision 1 and rationale]
- [Decision 2 and rationale]

**Problems Encountered**:
- [Issue 1 and how it was resolved]

**Next Steps**:
- [What should be done in next session]
- [Any blockers or open questions]
```

---

### Session: [First Session Date]

**Completed Tasks**:
- [Your first session summary will go here]

**Files Created/Modified**:
- [List files with brief descriptions]

**Key Decisions**:
- [Important decisions made]

**Next Steps**:
- [What to do next]

---

## Archiving Instructions

**When to archive:**
- When this file has more than 15 sessions
- Or when file becomes difficult to read (too long)
- Generally: monthly or quarterly depending on activity

**How to archive:**
1. Create `docs/memory-archive/` directory if it doesn't exist
2. Create a new file: `docs/memory-archive/YYYY-MM.md` (e.g., `2025-01.md`)
3. Move the oldest 10 sessions to the archive file
4. Keep the most recent 5-10 sessions in this file
5. Update the "Last Archived" note below

**Last Archived**: Never (initial file)

---

## Finding Old Context

**If you need context from old sessions:**
1. Check `docs/memory-archive/` directory
2. Files are organized by month/year
3. Use grep/search to find specific topics
4. Tell the AI: "Check docs/memory-archive/2025-01.md for context about [topic]"

**If a decision was really important:**
- It should also be documented in ARCHITECTURE.md (technical decisions)
- Or in CLAUDE.md "Key Decisions & Rationale" section (workflow decisions)
- Memory is for session-to-session continuity
- Permanent decisions belong in ARCHITECTURE.md or CLAUDE.md

---

## Guidelines for Session Summaries

**Keep them concise but informative:**
- Focus on "what" and "why", not detailed "how"
- Mention files changed (helps AI locate code)
- Document decisions and their rationale
- Note any gotchas or learnings
- Bullet points are fine (don't write essays)

**What to include:**
- ✅ Completed tasks
- ✅ Files created/modified
- ✅ Key technical decisions
- ✅ Problems solved
- ✅ Next steps

**What NOT to include:**
- ❌ Code snippets (put those in code comments)
- ❌ Long explanations (keep it summary-level)
- ❌ Repetitive information
- ❌ Obvious changes ("fixed typo in README")

---

## For AI Agents

**At session start:**
- Read this file completely (all active sessions)
- Pay special attention to the most recent 2-3 sessions
- Note any "Next Steps" from the last session
- Understand recent decisions and context

**At session end:**
- Append a new session summary using the format above
- Include the date in YYYY-MM-DD format
- Fill out all sections (even if brief)
- Check if file has >15 sessions - if so, suggest archiving

**When archiving:**
- Move oldest 10 sessions to `docs/memory-archive/YYYY-MM.md`
- Keep most recent 5-10 sessions in this file
- Update "Last Archived" date above
- Preserve formatting and structure in archive
