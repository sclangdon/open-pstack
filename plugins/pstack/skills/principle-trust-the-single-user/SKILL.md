---
name: principle-trust-the-single-user
description: "Apply when designing or implementing a single-user desktop application. Spend no time on threat modelling or defences against attackers. Does not apply to shared, multi-user, or networked software."
user-invocable: false
---

# Trust the Single User

A single-user desktop application has no hostile actor to defend against. Spend no time on threat models, attack vectors, or defences against hostile changes from outside.

The code must still be stable and robust. Validate external input at the boundary per [Boundary Discipline](../principle-boundary-discipline/SKILL.md), and assert internal state per [Assert Internal Correctness](../principle-assert-internal-correctness/SKILL.md).

This principle does not apply to shared, multi-user, or networked software.
