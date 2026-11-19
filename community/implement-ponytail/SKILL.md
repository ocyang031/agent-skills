---
name: implement-ponytail
description: "Use when implementing a ticket or feature with Matt-style implement flow. Enforces Ponytail lazy-senior minimalism: smallest complete change, YAGNI, no unrequested abstractions. Prefer this over plain implement when the user wants less code or mentions ponytail / 极简 / yagni."
---

# Implement × Ponytail

You are doing Matt-style implement, but under strict Ponytail rules.

**Core rule:** The best code is the code you never write. Solve the whole current ticket with the least new code.

## Decision ladder (stop at the first that works)

1. Does this need to exist at all? → Skip and say so.
2. Already exists in the codebase? → Reuse it.
3. Stdlib or native feature enough? → Use it.
4. Can it be one clear line / very few lines? → Do that.
5. Only then write the minimum custom code.

Never add: extra abstractions, factories, options, config, future-proofing, or unrequested features.

## Process

1. Read the ticket/spec and current code.
2. Apply the decision ladder before writing anything.
3. Implement with TDD (red → green → refactor). Keep refactoring minimal.
4. Touch only what the ticket requires (callers, tests, fixtures included).
5. Finish the complete vertical slice — no more, no less.

## Required output format

After implementation, always end with:

**Adopted approach:** (which ladder step + one-sentence summary)

**Skipped:** (list what you deliberately did not build and why)

**Risks:** (any remaining limitations or shortcuts)

**Tests:** (what passed / what was added)

If you left a deliberate shortcut, mark it in code:
`// shortcut: | upgrade when: `

Active until the ticket is done or user says "normal mode" / "关闭极简".
