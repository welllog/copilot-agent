---
name: disciplined-coding-workflow
description: Use when implementing, fixing, refactoring, or explaining code. Defines a disciplined understand → plan → execute → validate → review → report workflow with scope control and honest validation.
---

# Coding Agent Workflow

A disciplined workflow for coding tasks: understand → plan → execute → validate → review → report. Apply it to any task that involves reading, writing, or reasoning about code.

## Core Principles

- **Evidence over assumption.** Never assume missing information. Read the actual code, files, and diffs before acting. Separate confirmed facts from assumptions and open questions.
- **Smallest grounded change.** Make the smallest edit that correctly addresses the task. Prefer reusing existing local patterns over introducing new abstractions or dependencies.
- **No silent scope expansion.** If new required work is discovered mid-task, stop, surface it, and ask before continuing. Do not build unlisted work into an in-flight change.
- **Honest validation.** Never claim validation passed unless it actually ran and passed. If validation cannot run, say so explicitly and report the confidence gap.
- **Small stable first version.** Prefer a smaller durable first version over a broad fragile one. Call out future extensions separately.
- **Challenge weak requirements.** Do not blindly satisfy every requested feature. Surface complexity, risk, maintenance cost, and simpler alternatives. The goal is a better outcome, not maximum compliance.

## Workflow

Move through these phases in order. For trivial single-change work, compress the middle phases into one step. For explain-only or review-only requests, stop after Understand and report — do not edit unless asked.

### 1. Understand

- Understand the request and its intent before acting.
- Read the project silently first: directory structure, manifest/build files, dependencies, README, and any existing plan or task files. Do not output analysis unless it is directly relevant.
- Identify the scope: which files, behaviors, and constraints are in play.
- If the request is underspecified, ask targeted questions — only what is critical and cannot be inferred from the codebase. Prefer one clarification round. Number the questions. Do not ask what the code already answers.
- For large work (multiple behaviors, multiple files, public APIs, migrations, security, performance, unclear ownership): briefly state the intended approach and key files before editing.

### 2. Plan

- Convert the work into an ordered task list of small, independently verifiable items.
- Each item should have: file scope, acceptance criteria, and a validation check.
- Order by dependency. One item in progress at a time.
- If the work is too large for one pass (cannot be grouped down to a handful of items), flag it to the user and propose splitting it.
- Do not start editing while the plan is still fluid. Share the stabilized list for visibility. Wait for confirmation only when the decision affects scope, architecture, or cannot be made safely from local context.

### 3. Execute

- Re-read target files and integration points before editing.
- Make the smallest grounded edit that addresses the current task.
- One task at a time. Do not run parallel edits that touch the same area.
- If validation fails but still points to the same task: repair locally and rerun.
- If validation falsifies the premise or requires new scope: stop, reassess, and revise the task list.
- If you discover new work: add it as a new task. Do not silently expand scope mid-edit.
- If a task is blocked by an external dependency: skip it, continue with independent tasks, and report the blocked one.

### 4. Validate

- After each task: run the narrowest meaningful validation (a focused test, build, type check, or manual check).
- After all tasks: run the broadest meaningful validation once (full test suite or integration check) — not just per-task checks.
- Cross-check all acceptance criteria. Report any unmet criteria as remaining work, not as completion.
- If validation cannot run, record why and report the confidence gap. Do not pretend it passed.

### 5. Review

- Review the full final diff for cross-module issues that per-task checks may miss: integration gaps, contract mismatches, regressions, and roundabout implementations.
- Lead with blocking findings ordered by severity. Include file and line references.
- Flag overcomplicated implementations when a simpler local pattern exists and the current approach adds material maintenance, correctness, performance, or testing risk.
- Do not block on style-only notes, formatting preferences, or optional refactors.
- Treat missing validation as blocking only when it materially affects confidence.
- Skip this phase only for trivial single-line fixes or explain-only responses, and state the reason.

### 6. Report

State concisely:
- What was found or changed.
- Which validation ran (per-task and integration), and which could not run.
- Review result and any blocking findings addressed.
- Remaining blockers, unmet acceptance criteria, or follow-up tasks.
- Any scope deviation from the original request.

## Decision Rules

- **When to ask the user**: only when a missing answer would change the implementation, when scope changes materially, or when a decision cannot be made safely from local context.
- **When to stop and reassess**: when validation falsifies the task premise, when new scope is discovered, or when a task is blocked by an external dependency.
- **When to compress phases**: trivial, clear, low-risk single-change work can skip the formal plan and go directly from Understand to Execute. Escalate to the full workflow if the task touches multiple areas, changes public behavior, adds dependencies, or affects security, data, or migrations.
- **When to challenge**: when a requirement is overbuilt, short-sighted, risky, or expensive relative to user value. Say so plainly and give the engineering reason.
