---
name: principle-requirements-come-from-the-domain
description: "Apply when you set, adopt, or chase a numeric bar such as accuracy, precision, tolerance, error bound, resolution, latency, or throughput. Derive it from the real-world problem (the physics, the inputs' uncertainty, what the output feeds) or take it from the user or a spec. A bar with no source is a guess, not a requirement."
user-invocable: false
---

# Requirements Come from the Domain

A requirement states what the real problem needs. A number picked because it looks safe, such as machine epsilon, 1e-12, six decimal places, or the tightest tolerance the tests pass, is not a requirement. Chasing it costs time, design freedom, and speed, and buys nothing the problem can use.

**Failure mode:** The agent sets a precision target for a numerical model without deriving it. The team spends weeks reaching it and gives up performance to get there. Review finds that the physics never needed it. The inputs and the model's own error made the real bar orders of magnitude looser.

**Pattern:**
- **Name the source of every bar.** Each numeric target records where it came from: the user, a spec or standard, or a derivation from the domain. A bar without a source does not go into a plan, a rubric, a test, or a design.
- **Derive it from the problem.** Ask what the output feeds, and how large an error must be before it changes a decision, an outcome, or what a person can perceive. Ask how uncertain the inputs are (measurement noise, sensor resolution, manufacturing tolerance) and how wrong the model is (simplifying assumptions, discretisation, omitted effects). The output cannot be more accurate than its inputs and model allow, so precision beyond that is noise. Set the bar at the largest error the consumer tolerates, with a stated margin, and show the arithmetic.
- **Take the inputs to the derivation from the domain.** Use datasheets, standards, the literature, and the project's data. When none states a number the design depends on, ask the user. It is a domain fact they may hold, not a design question you can settle by experiment.
- **Derive test tolerances from the bar.** Never from machine epsilon, and never from the tightest value that passes.
- **Re-derive an expensive bar before you chase it.** When a bar forces a slower design, a costlier algorithm, wider types, or repeated failed attempts, check its source before more work. An unsourced bar that costs speed breaks [Favour Performance](../principle-favour-performance/SKILL.md). [Requirements Are Not Trade-offs](../principle-requirements-are-not-trade-offs/SKILL.md) binds only bars that have a source.
- **A derived bar binds both ways.** When the derivation shows the problem needs more precision than you assumed, that bar is a requirement. Meet it.
