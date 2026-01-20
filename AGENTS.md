# AGENTS.md — Project Instructions for Coding Agents

> This file is for coding agents (Codex / Claude Code / Cursor / etc).
> Read this first. Follow it as hard constraints unless explicitly overridden in the task.

## 0) Golden Rules (Hard Constraints)

- Do NOT invent project facts. If unsure, inspect the repo first and cite file paths.
- Do NOT add new production dependencies unless the task explicitly requests it.
- Do NOT touch secrets/credentials. Never print tokens, keys, cert private keys, or full env files.
- Prefer smallest-possible diffs that satisfy the acceptance criteria.
- Every non-trivial change must include: (1) summary, (2) verification evidence, (3) risks/notes.

## 1) Repository Orientation (What this repo expects)

This repo uses a 3-stage flow:
- Stage 1: Idea Incubation → outputs “LOCK/EXPLORE” gate.
- Stage 2: Spec Brief → outputs “LOCK/REVISE” gate.
- Stage 3: Doc Generator → produces docs + implementation/audit kickoff prompts.

When asked to generate docs from a locked Spec Brief:
- Write files into `docs/` with stable, deterministic structure.
- Do not rely on chat context; docs must be self-contained.

## 2) Standard Outputs & File Paths

Unless the task says otherwise, use these canonical paths:

- docs/prd.md
- docs/plan.md
- docs/decisions.md
- docs/checklist.md

If the task includes “write to repo”, you MUST create/update those files on disk (not just paste in chat).

## 3) Verification & Evidence (PASS/FAIL)

### 3.1 Always produce evidence
For any task involving code or runnable projects:
- Run the project’s standard checks and paste the command + results summary.
- If checks are missing, propose a minimal default set (and mark as TODO with a default assumption).

### 3.2 Default “minimum gate” (unless overridden by Spec/Task)
- Build passes (if applicable)
- Typecheck passes (if applicable)
- Lint passes (if applicable)
- Tests pass (if applicable)
- Smoke: key routes/pages load without pageerror; console.error=0 (warn allowed)

If the repo has known noise (e.g., Next dev warnings), allow a whitelist only if you document:
- exact message/pattern
- why it’s safe
- where it’s recorded (e.g., docs/checklist.md)

## 4) Coding Style & Structure

- Prefer clear, boring solutions over clever ones.
- Keep functions/modules small and testable.
- If you introduce config knobs, document them (README or docs/runbook if present).
- Naming: keep terms consistent across docs/spec/code (state names, route names, fields).

## 5) Ownership & Scope Control

If the task defines Ownership boundaries (directories/modules):
- Stay inside the listed directories.
- If you must touch outside, STOP and explain why (and propose the minimal change).

If scope is ambiguous:
- Apply “default assumptions” from the locked Spec Brief (or make the smallest reasonable default, clearly marked).

## 6) Safety & Security

- Never log sensitive user data.
- Don’t weaken auth, CORS, CSP, or security checks to “make it work” unless explicitly requested.
- For data migrations: prefer additive changes; include rollback notes.

## 7) How to Work (Suggested Process)

1) Inspect:
   - read relevant docs/spec
   - search for existing patterns
2) Plan briefly:
   - list steps and which files will change
3) Implement:
   - small commits / coherent chunks
4) Verify:
   - run checks, capture evidence
5) Summarize:
   - what changed, how verified, risks/next steps

## 8) Commit / PR Conventions (if applicable)

- Commit message format:
  - docs: ...
  - feat: ...
  - fix: ...
  - chore: ...
- Each commit or final response must include:
  - Change summary (bullets)
  - Verification (commands + PASS/FAIL)
  - Risks / TODOs (with default assumptions)

## 9) When generating docs from Spec Brief (Special Mode)

If the user provides a LOCKed Spec Brief and requests doc generation:
- Enforce required headings exactly.
- Ensure PRD/PLAN/DECISIONS/CHECKLIST are mutually consistent.
- In decisions.md, capture defaults used for unanswered questions.
- Avoid “hand-wavy” acceptance; turn it into testable checks.

## 10) Size Limits & Layering Notes (FYI)

Codex reads AGENTS.md files in a layered chain (global + project, root → current dir).
If this file grows too large, split into nested AGENTS.md closer to subprojects. (Codex has a project-doc size cap by default.) 