---
name: principle-assert-internal-correctness
description: "Apply when writing or refactoring any function. Assert arguments, return values, preconditions, postconditions, and invariants. Assertions catch programmer errors inside the program. External input is still validated at the boundary."
user-invocable: false
---

# Assert Internal Correctness

Assertions detect programmer errors. Operating errors are expected and must be handled. An assertion failure is never expected. More assertions are better than fewer.

- **Assert pre- and postconditions.** Assert every function's arguments, return values, preconditions, postconditions, and invariants. A function must not operate blindly on data it has not checked.
- **Pair assertions.** For each property you enforce, find at least two code paths that can assert it. For example, assert that data is valid right before writing it to disk and again right after reading it back.
- **Assert the positive and the negative space.** Assert what you expect and what you do not expect. Interesting bugs cluster where data crosses between the valid and the invalid.
- **Assert only what the program owns.** An assertion confirms that what we expect to be true is true and what we expect to be false is false. Never assert external input from users or libraries. Validate it at the boundary per [Boundary Discipline](../principle-boundary-discipline/SKILL.md).
- **Exit at once.** A failed assertion stops the program immediately.

An assertion is not a guard. A guard handles a bad state and carries on. An assertion stops the program on one, so it never hides a bug.
