# Reviewer Brief

This package is intended to help reviewers understand what Aurora-Lens is and what it is not.

## Review the actual category

Aurora-Lens is not a chatbot, dashboard, wrapper, content filter, approval workflow, or post-hoc audit tool.

It is a runtime admissibility gate operating over persistent governed state, with lawful continuation and forensic audit.

## What to evaluate

Reviewers should evaluate:
- whether the production chain is clearly separated
- whether Lens, Governor, PEF, and audit roles remain distinct
- whether admissibility is determined before output becomes consequence
- whether refusal, hold, revision, escalation, and audit are treated as governed outcomes
- whether the forensic path can show what was attempted, what was blocked or allowed, and why
- whether PEF ambiguity and hold behaviour are visible rather than hidden

## What not to assume

Do not assume:
- PEF is generic memory
- Lens is the whole Aurora architecture
- Governor makes admissibility decisions
- the ledger is merely post-hoc logging
- refusal is a UX failure
- public documentation exposes protected runtime internals

## Public-review limit

This package supports conceptual, architectural, and category review.

Production-level technical review requires access to protected materials under separate written agreement.
