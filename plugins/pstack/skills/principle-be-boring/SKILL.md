---
name: principle-be-boring
description: "Apply when designing or writing code, and whenever tempted to cut line count, build a system, add an abstraction, write event-based code, or split a long function. Solve the problem the most direct way with language basics, one expression per line."
user-invocable: false
---

# Be Boring

Do the thing the simplest, most direct way. Simple, boring designs and code beat clever ones. Write as if the language were as primitive as assembly.

- **Avoid systems.** Solve the problem in front of you directly. Do not build a framework, registry, or plugin mechanism to solve it.
- **Use the basics.** `if` statements, loops, and arrays cover most code. You rarely need anything more exotic.
- **Minimise abstractions.** An abstraction confuses more often than it helps. Write plain code instead.
- **Avoid events.** Event-based code is hard to follow and hard to debug. Do not write it.
- **One expression per line.** Give each expression its own statement, so a breakpoint can stop on every value.

  Avoid:

  ```c
  int x = ((y + sum_of_things()) * another_thing());
  ```

  Prefer:

  ```c
  int sumOfThings = sum_of_things();
  int anotherThing = another_thing();
  int yPlusSumOfThings = y + sumOfThings;
  int x = yPlusSumOfThings * anotherThing;
  ```

- **Never optimise for line count.** Do not write compact code, or add an abstraction, to save lines. Many lines are not a sign of bad code, especially when each line holds one expression.
- **Keep a function's code in one function.** Never split a function only because it is long. Length is not complexity. A *complex* function may point to a bad design, so review the design instead.
