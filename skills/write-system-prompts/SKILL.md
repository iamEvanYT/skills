---
name: write-system-prompts
description: Design, draft, review, debug, and iteratively improve system prompts and agent instruction policies. Use when Codex needs to create or revise a system prompt, separate durable policy from runtime context, define tool authority or trust boundaries, diagnose prompt failures, create prompt evaluations, or convert vague behavioral requirements into testable model instructions.
---

# Write System Prompts

Treat a system prompt as a compact operating policy for a model inside a product. Define durable goals, authority, decision rules, and interfaces while leaving changing facts and task-specific data to user messages, tools, retrieval, or runtime context.

Read [references/field-guide.md](references/field-guide.md) when the task needs the full design rationale, anti-patterns, reusable template, or final review checklist.

## Gather the behavior specification

Identify the artifact being designed:

- Use a task prompt for one-off input, transformation, audience, or output constraints.
- Use a system prompt for stable role, scope, priorities, boundaries, defaults, and interface contracts.
- Treat an agent harness as the larger system containing the prompt, tools, permissions, memory, runtime state, retries, and product-side enforcement.

Before drafting, extract or infer:

- the model's observable mission and audience;
- allowed, confirmation-gated, and prohibited actions;
- success criteria and unacceptable outcomes;
- likely conflicts, edge cases, failures, and adversarial inputs;
- the required output or machine interface;
- facts that change at runtime and therefore do not belong in durable policy.

Ask only for missing information that would materially change authority, safety, or the output contract. Otherwise, state reasonable assumptions and draft.

## Design the policy

Select only sections that change behavior. Prefer this order:

1. Role and mission
2. Scope and authority
3. Priorities and hard constraints
4. Operating principles
5. Tools and actions
6. Context and trust
7. Communication and output
8. Completion and recovery
9. Examples, only when they sharpen a decision boundary

Separate durable policy, dynamic state, task input, retrieved knowledge, and conversation state. Do not hardcode dates, repository state, retrieved documents, customer records, or other changing facts into the system prompt.

For consequential tools or actions, define:

- the trigger for use;
- which option to prefer when tools overlap;
- whether the model may act or must ask first;
- how to verify success;
- how to recover from denial, partial success, invalid output, or non-transient failure.

Mark user-supplied and retrieved content as data unless the product explicitly grants it instructional authority. Treat prompt text as guidance, not an access-control boundary; require the harness to enforce permissions, spending limits, secret handling, destructive-action gates, and exact validation.

## Write operational rules

- Express observable behavior instead of persona adjectives or vague outcomes.
- Prefer conditional rules: define both the triggering condition and the response.
- Pair prohibitions with a useful safe alternative when one exists.
- Reserve `must`, `never`, and similar absolutes for real hard constraints.
- Use defaults for behavior that may yield to explicit user needs and heuristics for context-sensitive optimizations.
- Add a short rationale only when it helps the model generalize.
- Give agents principles, destinations, constraints, and quality bars instead of brittle tool-call choreography.
- Use exact procedures only when order is itself a compliance or interface requirement; define failure behavior at irreversible boundaries.
- Avoid duplicating tool schemas or using headings and delimiters as if they created security privileges.
- Define completion, partial success, blockers, and retry behavior explicitly.

## Draft for the consumer

Lead with the prompt itself when the user asks for a usable draft. Keep commentary separate and concise.

For human-readable output, specify audience, tone, density, citations, and what appears first only as needed. For machine-readable output, define required fields, types, allowed values, missing-data behavior, and whether extra prose is forbidden; rely on external validation for guarantees.

Start zero-shot. Add a small number of representative examples only after prose fails to establish a boundary or format reliably. Make examples diverse, realistic, and focused on observable decisions rather than hidden reasoning.

## Review and iterate

Check the draft for:

- conflicts or unclear priority;
- hard constraints with hidden exceptions;
- vague, negative-only, or duplicated rules;
- dynamic facts in durable policy;
- untrusted content that could be mistaken for instructions;
- missing authority, confirmation, verification, recovery, or completion semantics;
- controls that need enforcement in code rather than prompting;
- sections or examples that do not earn their context cost.

Create a compact evaluation set covering happy paths, boundary cases, conflicts, adversarial inputs, operational failures, and style regressions. Record the model, parameters, tools, prompt version, and expected observable behavior. Change the smallest plausible part, rerun the full regression set, and remove obsolete compensating instructions as models or the harness evolve.

Do not claim that a prompt is reliable solely because it reads well. Distinguish design review from empirical validation, and state when the prompt has not been tested against the target model and harness.
