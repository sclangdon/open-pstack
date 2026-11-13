---
name: principle-create-libraries
description: "Apply when designing or implementing application code. Build the application from reusable libraries wired together by thin program-specific code. Keep each library's API open, caller-first, coherent, and upgradable."
user-invocable: false
---

# Create Libraries

Compose applications from reusable libraries, and keep the program-specific code that wires them together thin. A library forces a strong API and can be tested on its own. Instead of adding code directly to an application, write a library that the application uses.

- **Be open, not closed.** Library users are programmers. Do not hide data behind getters, setters, or other needless machinery. Callers may change state directly. Hide decisions, not data.
- **Put the caller first.** A library exists to serve its caller. Design for the caller's needs, and do not make the caller's decisions for them.
- **Let coherence set the size.** A library can be a single function, and it can be large. Split a library only when it stops being coherent, never because of its size.
- **Make structures upgradable.** A released API cannot change, so plan for growth from the first version. A later version adds to a structure without changing what earlier callers see. The [c-best-practices](../c-best-practices/SKILL.md) skill shows the C pattern.
