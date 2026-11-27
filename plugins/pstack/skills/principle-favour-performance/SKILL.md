---
name: principle-favour-performance
description: "Apply when designing or implementing anything, and whenever speed trades against another goal. Performance is the first feature. Design for it from day one, measure competing ideas, and keep the fastest for the usual case."
user-invocable: false
---

# Favour Performance

Performance is the primary goal and the feature that sets the work apart. Design and implement for it from the first day.

- **Measure competing ideas.** For non-trivial or critical work, try several approaches, measure each, and keep the fastest for the usual case across the hardware the software supports, not just this machine, per [Tune for the Supported Hardware](../principle-tune-for-the-supported-hardware/SKILL.md). Vet each number with the [benchmark-checklist](../benchmark-checklist/SKILL.md) skill.
- **Push harder on hot paths.** When a measurement shows code is a bottleneck or on a critical path, try more ideas than usual. Write it in assembly when that proves more than 10% faster, behind run-time dispatch with a portable fallback.
- **Beat the alternatives.** When a third-party application or the code you replace does the same job, measure against it. Being slower is not acceptable. A design that measures slower has failed. Reopen it, per [Requirements Are Not Trade-offs](../principle-requirements-are-not-trade-offs/SKILL.md).
- **The usual case is ours.** Take the usual case from our requirements and our measured workload, never from the workload a borrowed design assumes.
