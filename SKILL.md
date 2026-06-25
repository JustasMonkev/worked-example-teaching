---
name: worked-example-teaching
description: Teach one concrete technical command, file, error, config, repo behavior, or code mechanism through an evidence-grounded worked example, inline. Use when the user asks to understand, learn, explain, or be walked through one specific technical thing. Do not use for broad curricula, saved lesson files, multi-topic training, or when a more specific debugging, framework-docs, security, document-editing, or product-design skill should lead.
---

# Worked Example Teaching

Teach one concrete technical thing by grounding the explanation in the user's exact artifact, working one example end to end, and optionally checking that they can reapply the mechanism. The goal is not to teach the domain — it is for the user to recognize and reuse this one mechanism once.

## When To Use

Use for a single concrete subject: a command, file, error, test failure, config value, CLI flag, dependency behavior, or one concept to walk through. Triggers like "explain what this does", "walk me through this error", "why does this behave like that?".

Do not use this skill alone for a full curriculum, saved lesson files, a durable learning workspace, multi-topic training, or when the real task is a bug fix, security review, docs research, or artifact edit. In those cases run the specific skill first and use this only as the explanatory layer. If the user wants saved/durable material, ask once:

> Do you want this as an inline explanation or a saved learning artifact?

## Core Method

### 1. Anchor to the concrete subject

Tie every line to the exact thing the user named — the actual command, path, error text, variable, or config key. Do not swap their case for a generic tutorial unless they ask for a general overview.

### 2. Inspect before teaching

If the explanation depends on repo files, command behavior, logs, config, or dependency versions, read the relevant artifact before explaining whenever it is available and cheap to check. Don't teach from generic memory when the real artifact is right there. Check the version (`package.json`, lockfile, `--version`) when behavior is version-dependent; if you can't, state the assumption.

Do not run destructive commands. Avoid anything that mutates files, installs packages, deletes state, rewrites history, calls external services, or starts long-running processes unless the user explicitly asked.

### 3. Show evidence

When you inspect something, the answer must show what you saw: a file path plus line range, exact output, exact error text, an exact config key/value, or a short quoted snippet. If you couldn't inspect, say so and ground the explanation in what the user provided.

> **Good:** In `src/eval.ts:42`, the fallback is `Number(process.env.EVAL_MIN_SCORE) || 0.8`. So `"0"` parses to `0`, then `0 || 0.8` becomes `0.8`.
>
> **Bad:** It probably uses a fallback somewhere.

### 4. Work one example end to end

Complete the walkthrough before asking anything — no quizzing mid-stream. Move in order: starting state → action → intermediate transformation → final result → why it happens.

### 5. Explain the mechanism, not the theory

Explain only what's needed for this case. Skip history, broad background, and documentation tours unless they're required for correctness.

> **Good:** In this rebase, Git opens a todo list; the line order becomes the replay order.
>
> **Bad:** Git rebase is part of a larger family of history-rewriting operations...

### 6. Practice — only on clear learning intent

If the user signals learning ("teach me", "walk me through", "I don't understand", "step by step", "give me practice"), add **one** nearby practice variant and **one** transfer check that change the surface but keep the same mechanism. Do not introduce a second topic. For a plain "what does this do?" / "why did it fail?", skip this entirely.

> **Practice:** if the code used `Number(process.env.MAX_RETRIES) || 3`, what happens when `MAX_RETRIES=0`?
>
> **Transfer:** if `TIMEOUT_MS=0` means "no timeout", why is `Number(process.env.TIMEOUT_MS) || 5000` wrong?

### 7. Close

End with one sentence capturing the mechanism. Suggest a follow-up only when there's an obvious next step — never manufacture a list.

## Output Contracts

Use the smallest structure that fits the intent.

**Quick answer** (direct explanation):

```md
[Worked example in a few sentences, with evidence.]

Takeaway: [one sentence]
```

**Learning answer** (clear learning intent):

```md
[Worked example end to end, with evidence.]

Takeaway: [one sentence]

Practice: [one nearby variant]
Transfer: [one focused question]
```
