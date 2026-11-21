---
name: council
description: Trigger this if the user says 'council'.
---

# Council

## Before the review

Before an audit:

- Address outstanding PR comments.
- Fix known issues.
- Run relevant checks.

Give the council the updated implementation. Do not defer known fixes until reviews return. If the user wants to discard the implementation and explore new ideas, skip fixes to code being replaced.

## Starting delegates

Bring in three delegates to help with the user's request, usually for review or feedback.

- Use one strong model from each of three different providers, at high reasoning effort.
- Use the council members named in the user's instructions. Otherwise, pick the latest flagship model from each provider, for example Claude Opus, GPT Sol, and Gemini Neon.
- If you cannot reach three providers, or a named member is unavailable, report it instead of substituting.
- In T3 Code, use `orchestrator_capabilities` to resolve the models, then use `delegate_task` to start one delegate per model in parallel.
- Elsewhere, use the harness's subagent tools.
- Give each delegate the request and relevant context.
- For review or feedback, keep their work read-only.

## While they run

- Do not wait idle. When a result arrives, check its findings against the code at once. Decide what to fix while the other delegates run.
- Do not edit files while a delegate still reviews the same checkout.
- If the user's instructions mark a delegate as non-blocking, do not wait for it. Treat a late result as feedback and do not record its score.

## Scoring

- For a code review, ask each delegate for a score out of 10.
- Count each full review pass as one round.
- A fresh review after fixes starts a new round.

## Reporting

Collect the delegates' responses. Summarize the useful findings, disagreements, and recommended next steps.

If the work ends in a pull request, put the results in the PR description before the model and harness line at the end:

```markdown
## Council review

Rounds: 2

| Delegate | Round 1 | Round 2 |
| --- | --- | --- |
| Claude Opus | 7/10 | 9/10 |
| GPT Sol | 8/10 | 10/10 |
| Gemini Neon | 7/10 | 9/10 |
```

- If a delegate gives no score, write `no score`. Do not invent one.
- If the PR is open, edit the description. Do not post a comment for this.
- If there is no PR, put the same results in the final reply only.

## Fix and review loop

If you agree with the delegates' recommendations, make the changes and request a fresh review. Continue until all delegates are satisfied with the outcome.

## Scope

Do not let repeated reviews cause scope creep. Fight to keep scope limited.
