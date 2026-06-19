# TDD Guide

Reference guide covering when to use a Technical Design Document, who should write and review it, and the review process and approval states.

---

## 1. When to Use This Template

> This section is part of the template itself — keep it in the final doc so reviewers have context.

A Technical Design Document (TDD) is required before beginning significant engineering work. **Use this template when any of the following apply:**

- You are building a new service, system, or significant feature
- Your work touches multiple teams or has cross-cutting dependencies
- The change introduces new infrastructure, storage, or external APIs
- There is meaningful architectural decision-making involved
- The work carries non-trivial risk — to reliability, security, data, or performance
- You are deprecating or significantly changing a system others depend on

**You probably do not need a full TDD for:**

- Small bug fixes or low-risk iterative changes within a single service
- Internal refactors with no observable behaviour change
- Work that follows a well-established, previously reviewed pattern

> If you're unsure, err on the side of writing one. A lightweight TDD is better than no shared understanding. Scope it down after a conversation with your EM or Senior / Principal engineer.

---

## 2. Who Should Write and Review

### 2.1 Author

The tech lead or senior engineer responsible for the work. The author owns the document through design, review, and implementation. The TDD is a living document — update it as understanding changes.

### 2.2 Design Shepherd

A more senior engineer who guides the author, provides early feedback, and helps identify gaps before wider review. Assign one before you start writing.

### 2.3 Reviewers

Anyone whose team is affected by or depends on the work: engineers from impacted teams, EM or Director for cross-org changes, SRE for production services, Security for new external surface area or data handling, and platform/infrastructure teams if relevant.

> Do not send a TDD for review until the design shepherd has signed off on a draft. Sending an under-baked design to a wide group wastes everyone's time and erodes trust in the process.

### 2.4 Timeline

Circulate at least one week before you need a decision. For large or contentious designs, allow two weeks. Reviewers should aim to respond within five business days.

---

## 3. Review Process and Approval

> This section explains the review process — keep it in all documents.

### 3.1 States

- `Draft` — author is still writing; do not request review
- `In Review` — circulated to reviewers; feedback expected within 5 business days
- `Approved` — all open questions resolved, all reviewers satisfied, design shepherd signed off
- `Superseded` — replaced by a later design; link to successor

### 3.2 Approval

A document is approved when: the design shepherd has signed off, all required reviewers have either approved or explicitly deferred, and all open questions are resolved. The author updates the status field and notifies stakeholders.

### 3.3 Amendments

Significant changes after approval require notifying reviewers and, if the change affects their team, explicit re-approval. Minor clarifications can be made with a note and an updated Last Updated date.

> A TDD is not a bureaucratic checkbox — it is a tool for building shared understanding and catching problems early. A rushed or superficial TDD is worse than a short but honest one. If you find yourself writing one to satisfy a process requirement rather than to think through a problem, that's a signal to have a conversation with your EM.
