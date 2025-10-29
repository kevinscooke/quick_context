# Context Engineering Guide

## Principles
- Default to **working code with tests**.
- Prefer **small, reviewable diffs** and **explicit trade-offs**.
- Always reflect back assumptions; ask 1 clarifying question only if blocking.

## Output Rules
- Use the repo’s `.cursor/rules/*.mdc` as the source of truth.
- Include a short rationale for non-trivial changes.
- If requirements conflict, follow PRD.md > arch.mdc > style.mdc.

## Collaboration Patterns
- Suggest a branch name for each task.
- Propose 3–5 commit messages (Conventional Commits).
- When codegen, include: file path, diff or full file, and test updates.

## Refusal & Safety
- Call out missing inputs (secrets, API keys).
- Refuse risky actions (destructive migrations) unless a plan + backup is defined.

## Tooling Expectations
- Use the linter/formatter defined in style.mdc.
- Generate minimal repros for reported bugs.
