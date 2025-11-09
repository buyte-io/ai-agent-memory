# PROJECT.md

**Project**: [Project Name]
**Version**: 1.0
**Last Updated**: [Date]

---

## How to Fill This Out

**Purpose**: This file defines WHAT you're building and WHY it matters. It keeps technical decisions aligned with user value.

**Time needed**: 20-30 minutes for new projects

**Tips**:
- Keep it concise - AI agents read this at session start
- Focus on MVP scope, not future dreams
- Use concrete language, avoid jargon
- Update the Change Log when scope shifts

---

## Vision

> One-sentence vision that captures the essence of what you're building.

**Example**: "A personal finance tracker that helps freelancers visualize income variability and plan for irregular cash flow."

---

## Problem Statement

What specific pain point are you solving? Frame it in concrete, user-centric terms.

**Guidelines**:
- Avoid buzzwords and corporate speak
- Focus on observable user frustration
- Be specific about the context and consequences
- Keep it to 2-3 paragraphs maximum

**Example**:
"Freelancers struggle to budget when income varies month-to-month. Traditional budgeting apps assume steady paychecks, making them useless for gig workers. This leads to overspending in good months and panic in slow months, creating unnecessary financial stress."

---

## Target Users

### Primary User Persona 1
**Who**: [Role/Description]
**Need**: [What they need from this product]
**Context**: [When/where/why they need it]

**Example**:
- **Who**: Freelance designers and developers earning $3K-$10K/month
- **Need**: Predict upcoming expenses against variable income
- **Context**: Planning 2-3 months ahead while dealing with invoice delays

### Primary User Persona 2 (if applicable)
[Repeat structure above. Keep to 2-3 personas maximum.]

---

## User Stories

Frame key functionality as user stories. Focus on the "who", "what", and "why" - not implementation details.

**Format**: As a [user type], I want to [action], so that [benefit].

### Core Stories
1. As a freelancer, I want to input invoices with expected payment dates, so I can see when cash will actually arrive
2. As a user, I want to see my average monthly income over 3/6/12 months, so I can set realistic budgets
3. As a user, I want to categorize expenses and see spending patterns, so I know where my money actually goes
4. [Add 3-8 core stories that define MVP]

### Nice-to-Have Stories (Post-MVP)
1. [Optional features for future iterations]
2. [Keep this list short - focus on MVP first]

---

## Success Criteria

How will you know this is working? Define measurable outcomes.

**Activation Metrics**:
- [First meaningful action user takes, e.g., "User adds 3+ income entries in first session"]
- [Completion of setup, e.g., "User connects bank account or completes onboarding"]

**Engagement Metrics**:
- [Usage frequency target, e.g., "60% of users check dashboard 2+ times per week"]
- [Retention target, e.g., "40% of users active after 30 days"]

**Quality Metrics**:
- [Performance targets, e.g., "Dashboard loads in <2 seconds"]
- [User satisfaction, e.g., "NPS score >30 after 2 weeks of use"]

**Adoption Target**:
- [Early validation goal, e.g., "20 beta users actively using >3 times in first week"]

---

## Scope Boundaries

### In Scope (MVP)
- [Feature 1 - be specific]
- [Feature 2]
- [Feature 3]

### Explicitly Out of Scope (Not MVP)
- [Feature that might be expected but isn't included]
- [Integration or capability being deferred]
- [Clarify what you're NOT building to prevent scope creep]

---

## Key Assumptions & Constraints

**Assumptions**:
- [User behavior assumption, e.g., "Users will manually enter income data"]
- [Technical assumption, e.g., "Users have access to email notifications"]

**Constraints**:
- [Time constraint, e.g., "MVP must ship within 6 weeks"]
- [Budget constraint, e.g., "Must use free-tier services"]
- [Technical constraint, e.g., "Must work offline-first"]

---

## Open Questions

Track unresolved decisions that need answers before or during development.

1. [Question about user behavior or requirements]
2. [Technical uncertainty that needs research]
3. [Integration or dependency that needs clarification]

**Resolution Protocol**: When these get answered, move the answer to the appropriate section above and date it.

---

## Change Log

Track significant scope or vision changes over time. This helps maintain context across sessions.

### [Date] - Version [X.X]
- **Changed**: [What changed]
- **Rationale**: [Why it changed]
- **Impact**: [What this means for implementation]

**Example**:
```
### 2025-01-09 - Version 1.1
- **Changed**: Removed bank account integration from MVP
- **Rationale**: API costs and complexity too high for initial validation
- **Impact**: Users will manually enter transactions initially
```

---

## Notes & References

- [Link to design mockups]
- [Link to competitive analysis]
- [Link to user research or interviews]
- [Any other relevant documentation]
