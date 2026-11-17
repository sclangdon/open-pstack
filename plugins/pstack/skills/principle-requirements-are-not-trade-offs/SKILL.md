---
name: principle-requirements-are-not-trade-offs
description: "Apply when a measurement, test, or review shows the chosen design misses a requirement or a measurable bar a principle sets, such as not being slower than the alternative. The design has failed. Reopen it instead of reporting the miss as a trade-off."
user-invocable: false
---

# Requirements Are Not Trade-offs

A trade-off gives up something that no requirement demands. A requirement includes a measurable bar a principle sets, such as [Favour Performance](../principle-favour-performance/SKILL.md)'s "being slower is not acceptable". When a result misses a requirement beyond the noise floor, per [Explain the Number](../principle-explain-the-number/SKILL.md), the design has failed. Calling the miss a trade-off hands the user a decision that the requirement already made.

**Failure mode:** The design round copies a popular project. A measurement shows the result is slower than the alternative and names the cost. The agent quotes "being slower is not acceptable", lists the miss as a trade-off, and stops. Each step after the measurement is wrong.

**Pattern:**
- **Name the miss.** Write down the requirement, the measured result, and the cause that the measurement names.
- **Find the decision behind the cause.** If the cause is an assumption the design rests on, such as the workload a borrowed project was built for, no implementation fix closes the gap. Return to the design round with the requirement as a day-one constraint, per [Redesign from First Principles](../principle-redesign-from-first-principles/SKILL.md). If the cause is in the implementation, fix it there, per [Fix Root Causes](../principle-fix-root-causes/SKILL.md).
- **Keep going.** A result that misses a requirement is not done. Do not stop at the measurement, and do not ask the user whether the miss is acceptable. A miss is not an open decision, a risk, an open question, a follow-up, a dead end, or a product call.
- **Stop only on evidence.** You may report a requirement as unmet only after a different design, built around that requirement, also misses it. Report it as unmet, with each design you tried and its measurement. Only the user can relax a requirement.
