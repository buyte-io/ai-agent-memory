# PROJECT.md

**Project**: TaskFlow - Smart Task Manager
**Version**: 1.0
**Last Updated**: 2025-01-09

---

## Vision

A lightweight task management app that helps solo founders and small teams stay focused on their most important work without overwhelming complexity.

---

## Problem Statement

Existing task managers fall into two categories: either they're too simple (basic to-do lists with no structure) or too complex (enterprise project management tools with steep learning curves). Solo founders and small teams waste time managing their task manager instead of doing the work.

They need something that provides just enough structure to stay organized (projects, priorities, due dates) without the cognitive overhead of Gantt charts, dependencies, and complex workflows. Current solutions either lack the basics (no due dates, no projects) or bury users in features they'll never use.

---

## Target Users

### Primary User Persona 1
**Who**: Solo founders and indie hackers building products
**Need**: Track tasks across multiple projects, prioritize daily work, see what's urgent
**Context**: Working alone, juggling multiple responsibilities, need to stay focused without constant context switching

### Primary User Persona 2
**Who**: Small startup teams (2-5 people)
**Need**: Shared task visibility, lightweight coordination, no project management overhead
**Context**: Fast-paced environment, everyone wears multiple hats, need simple collaboration without meetings

---

## User Stories

### Core Stories
1. As a user, I want to create projects to organize my tasks, so I can mentally separate different areas of work
2. As a user, I want to add tasks with titles, descriptions, and due dates, so I know what needs to be done and when
3. As a user, I want to set task priorities (high, medium, low), so I can focus on what matters most
4. As a user, I want to see today's tasks in a focused view, so I'm not overwhelmed by everything at once
5. As a user, I want to mark tasks complete and see them archived, so I feel progress and can reference completed work
6. As a team member, I want to assign tasks to teammates, so we know who's responsible for what
7. As a user, I want to filter tasks by project, priority, and assignee, so I can find relevant work quickly

### Nice-to-Have Stories (Post-MVP)
1. As a user, I want to add recurring tasks (daily/weekly), so I don't have to recreate routine work
2. As a user, I want to add subtasks to break down complex work, so I can track granular progress
3. As a user, I want email reminders for overdue tasks, so nothing falls through the cracks

---

## Success Criteria

**Activation Metrics**:
- User creates at least 1 project and 3 tasks in first session
- User marks at least 1 task complete within first 3 days

**Engagement Metrics**:
- 50% of users return daily in first week
- 30% of users active after 30 days (mark tasks complete or add new tasks)

**Quality Metrics**:
- App loads in <2 seconds on 3G connection
- Task actions (create, complete, edit) feel instant (<300ms)

**Adoption Target**:
- 15 beta users actively using (5+ completed tasks) in first 2 weeks

---

## Scope Boundaries

### In Scope (MVP)
- Create/edit/delete projects
- Create/edit/delete/complete tasks with title, description, due date, priority
- Assign tasks to team members
- Today view (tasks due today or overdue)
- Project view (all tasks in a project)
- Filter by priority, assignee
- Simple team invites (email-based)
- Mobile-responsive web interface

### Explicitly Out of Scope (Not MVP)
- Native mobile apps (web only for MVP)
- Calendar integration (Google Calendar, Outlook)
- File attachments on tasks
- Time tracking
- Comments/discussions on tasks
- Email notifications (except invite emails)
- Recurring tasks
- Subtasks
- Task dependencies
- Gantt charts or timeline views

---

## Key Assumptions & Constraints

**Assumptions**:
- Users will manually check the app daily (no push notifications for MVP)
- Teams are small enough (<10 people) that simple assignment works (no complex roles/permissions)
- Users are comfortable with web-only (no native app requirement)

**Constraints**:
- Must ship MVP within 8 weeks
- Must use free-tier hosting to validate before paying for infrastructure
- Must work well on mobile browsers (responsive, not native)

---

## Open Questions

1. Do users need to see completed tasks in the main views, or is an archive sufficient?
   - **Current thinking**: Archive is sufficient, keeps main views focused
2. Should we support guest users (no account) for trying the app?
   - **Decision needed by**: Week 2 of development

---

## Change Log

### 2025-01-09 - Version 1.0
- Initial project documentation created
- Defined MVP scope and success criteria
