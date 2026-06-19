---
name: technical-design-documentation
description: Create a Technical Design Document (TDD) for a software feature, system, or service. Activate when a user asks to write, draft, or create a technical design doc, technical spec, or TDD — or when planning a new feature, system change, or API that needs formal design documentation before implementation begins.
---
# Technical Design Documentation

Guide the user through producing a complete, AI-buildable Technical Design Document — structured so that an AI coding agent (or a human engineer) can implement the design with minimal ambiguity.

## Tools

- **AskUserQuestion**: Gather structured input from the user at key workflow steps before proceeding.
- **Read / Glob / Grep**: Explore existing codebases to populate architecture, data model, and dependency sections.
- **WebFetch**: Retrieve API contracts, external docs, or referenced RFCs.
- **Notion MCP** (if available): Read or write TDD documents in Notion.
- **gh**: Pull related PRs, issues, or ADRs for context.

## When to Use

Activate when:

- The user asks to write, draft, or create a "technical design doc", "TDD", or "technical spec"
- Someone says "I need to design [feature/system]" before writing any code
- A Jira ticket or task requires a design document before implementation
- The user is planning a new API, service, data model change, or cross-team integration
- An existing system is being refactored and the change needs a written design
- The user wants to document architectural decisions (ADRs) alongside an implementation plan

## Context

| Reference                                  | Contents                                                                                   |
| ------------------------------------------ | ------------------------------------------------------------------------------------------ |
| [tdd-template.md](references/tdd-template.md) | Full TDD template with all sections, guidance callouts, and placeholder text word for word |
| [tdd-guide.md](references/tdd-guide.md)       | When to use a TDD, who should write and review, and the review process and approval states |

## Workflow

### 1. Understand the Work

Use **AskUserQuestion** to gather initial context:

* What are you building? (feature name, system, or service)
* What problem does it solve or what goal does it achieve?
* Do you have a target codebase or repo to explore?
* Is there a ticket, issue, or existing spec to reference?

Then identify whether a full TDD is needed by referring to [tdd-guide.md](references/tdd-guide.md):

* **Required:** new services, cross-team changes, new infrastructure, meaningful architectural decisions, non-trivial risk to reliability/security/data/performance, or deprecating a system others depend on
* **Not required:** small bug fixes, internal refactors with no observable behaviour change, work following a well-established previously reviewed pattern

If in doubt, err on the side of writing one. A lightweight TDD is better than no shared understanding.

### 2. Explore the Codebase [IF APPLICABLE]

Use Read / Glob / Grep to understand:

- Existing architecture and service boundaries relevant to the design
- Current data models and schema patterns
- Existing API conventions (REST/event-driven/gRPC)
- Test patterns and deployment conventions

This prevents the TDD from proposing designs that conflict with existing systems.

### 3. Draft Each Required Section

Work through required sections **one at a time, in order**. For each section, repeat this three-step loop:

1. **Ask** — Use **AskUserQuestion** to ask clarifying questions that cover every field, sub-section, and placeholder for this section in [tdd-template.md](references/tdd-template.md). Ask targeted questions rather than open-ended ones (e.g. "Is X a goal or a non-goal?" rather than "What are your goals?"). Use what you learned in step 1 and step 2 to pre-fill what you can infer and ask the user to confirm or correct.
2. **Draft** — Write the section content. Replace guidance callout blocks with real content and italic placeholder text with specific, concrete answers.
3. **Verify** — Use **AskUserQuestion** to present the drafted section to the user and ask: "Is this section correct? Should anything be changed before we move on?" **Do NOT proceed to the next section until the user confirms.**

**IMPORTANT: You MUST complete all three steps (Ask → Draft → Verify) for each section before starting the next one. Never batch multiple sections together.**

Section order:

1. Document Header
2. Overview
3. Goals and Non-Goals
4. Background and Context
5. Proposed Design (including API Design and Data Model sub-sections where applicable)
6. Alternatives Considered
7. Risks and Mitigations
8. Operational Considerations
9. Testing Strategy

### 4. Complete Applicable Sections

Add optional sections where relevant:

- **API Design** — if introducing or changing any APIs (internal or external)
- **Data Model** — if changing persistent data (new tables, schema changes, backfills)
- **Security and Privacy** — if exposing new external surface, processing/storing user data, changing auth/authz, or adding new third-party dependencies

### 5. List Open Questions

Use **AskUserQuestion** to surface any unresolved decisions before writing this section:

- Are there any design decisions you haven't made yet?
- Are there dependencies on other teams or systems that are uncertain?
- Are there unknowns around performance, scale, or security you need answered?

Capture all unresolved questions with owner and deadline. All open questions must be resolved before approval. Do not list questions you already know the answer to.

### 6. Export or Publish the TDD

Before finalising the document, use **AskUserQuestion** to ask the user how they would like to save it:

> "Where would you like to save this TDD?
>
> 1. **Notion** — create it as a private page in Notion (requires Notion MCP)
> 2. **Markdown file** — export it as a `.md` file to a local path"

Based on the response:

- **Notion:** Use the **Notion MCP** to create a new private page and write the full TDD content to it. Confirm the page URL with the user once created.
- **Markdown file:** Use **AskUserQuestion** to ask for the file path where they would like the `.md` file saved (e.g. `docs/tdd/my-feature.md`), then write the document to that location.

### 7. Review Readiness Check

Before circulating for review, confirm:

- Design shepherd has reviewed the draft and signed off
- All required sections are complete with real content (no guidance blocks remaining)
- Goals are concrete and measurable — not vague
- Alternatives Considered section is substantive with specific trade-offs
- Risks table has real entries with mitigations
- Security risks have their own sub-section if applicable

### 8. Circulate for Review

Update status to `In Review` and share with reviewers:

- Circulate at least one week before you need a decision
- Allow two weeks for large or contentious designs
- Reviewers should aim to respond within five business days

## Guidelines

- **Never send a TDD for review without design shepherd sign-off** — an under-baked design wastes reviewers' time and erodes trust in the process
- **Goals must be concrete and measurable** — "improve performance" is not a goal; "reduce p99 latency from 800ms to under 200ms under normal load" is
- **Alternatives Considered is not optional** — it is one of the first things an experienced reviewer looks for; "didn't feel right" is not an acceptable reason for ruling out an alternative
- **A design with no identified risks is almost certainly incomplete** — think across reliability, security, data correctness, performance, operability, and reversibility
- **The TDD is a living document** — update it as understanding changes during implementation
- **Security risks deserve their own sub-section** — loop in the security reviewer early; security review is much cheaper before implementation than after
- **Use the full template** from [tdd-template.md](references/tdd-template.md) — do not skip required sections without explicit justification
- **A TDD is not a bureaucratic checkbox** — it is a tool for building shared understanding and catching problems early; a rushed or superficial TDD is worse than a short but honest one
