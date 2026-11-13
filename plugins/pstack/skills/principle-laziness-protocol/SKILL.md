---
name: principle-laziness-protocol
description: "Apply when refactoring, evaluating diff size, deciding what is in scope, or tempted to add abstractions, layers, or signal threading. Bias toward deletion, the smallest change that solves the problem, and only the work that was asked for."
user-invocable: false
---

# Laziness Protocol

- **Consolidate decisions.** Do not repeat the same choice in several places. Put it behind one source of truth and pass the result as a simple flag.
- **Minimize the diff.** Make the smallest change that solves the problem without breaking another principle. Small means scope, not line count. Never compress code to save lines, per [Be Boring](../principle-be-boring/SKILL.md).
- **Do only what was asked.** Do no work that the user or the calling agent did not ask for. If you catch yourself writing "I just went ahead and did...", you should not have done it. Report what you noticed instead.
- **Explain a big change.** When a change is genuinely big, say why.
