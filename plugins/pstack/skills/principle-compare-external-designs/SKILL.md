---
name: principle-compare-external-designs
description: "Apply when designing or implementing something other projects have solved. Study at least three widely used projects that solve a similar problem, critique them, check the assumption each rests on against our requirements, and take their best ideas into your design."
user-invocable: false
---

# Compare External Designs

Find out how other projects tackled the same problem. Investigate popular, widely used projects that solve a similar problem and compare them with your design.

- Ask what they thought of that you did not, what they have in common, and how you would improve them. Critique them and use the best ideas.
- Write down the assumption each design rests on, such as mostly hits, mostly reads, small keys, or one writer. Check that assumption against each of our requirements before you take the design. Reject a design whose assumption contradicts a requirement. A popular design suits its own users. Popularity is no evidence that it suits ours.
- Judge each design on our requirements and our workload, not on its reputation or its own benchmarks. Where the choice affects speed, measure it, per [Favour Performance](../principle-favour-performance/SKILL.md).
- Study at least three, so that one project does not bias the design. If you cannot find three, give their ideas less weight.
