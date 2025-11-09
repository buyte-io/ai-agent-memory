# Memory Archive

This directory contains archived session history from MEMORY.md.

## How Archiving Works

When MEMORY.md grows beyond 15 sessions, the oldest sessions get moved here to keep the active memory file manageable.

### Archive Organization

Files are organized by month/year:
- `2025-01.md` - January 2025 sessions
- `2025-02.md` - February 2025 sessions
- etc.

### When to Archive

Archive when:
- MEMORY.md has more than 15 sessions
- File becomes difficult to read (too long)
- Monthly or quarterly depending on project activity

### How to Archive

1. Create a new file: `YYYY-MM.md` (e.g., `2025-01.md`)
2. Move the oldest 10 sessions from MEMORY.md to the archive file
3. Keep the most recent 5-10 sessions in MEMORY.md
4. Update "Last Archived" date in MEMORY.md

### Finding Old Context

To find specific information from past sessions:
```bash
# Search all archives
grep -r "JWT" docs/memory-archive/

# Search specific month
grep "authentication" docs/memory-archive/2025-01.md
```

### Note for This Example Project

This project only has 7 sessions so far, so nothing has been archived yet. This directory is here to demonstrate the archive structure for when it's needed.

When TaskFlow reaches 15+ sessions, the first 10 sessions (2025-01-09 through approximately 2025-01-20) would be moved to `2025-01.md`.
