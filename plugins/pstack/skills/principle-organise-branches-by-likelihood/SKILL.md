---
name: principle-organise-branches-by-likelihood
description: "Apply when writing an if/else chain or a switch. Order the cases from the most likely to the least likely, the default case included."
user-invocable: false
---

# Organise Branches by Likelihood

Order the branches of an if/else chain or a switch from the most likely to the least likely. In a switch this includes the default case, which comes first when it is the most likely.

```c
if (most_likely_branch()) {
}
else if (second_most_likely_branch()) {
}
else {
    // least likely branch
}
```

```c
switch (x) {
case mostLikely: break;
case secondMostLikely: break;
default:
    // least likely
    break;
}
```

Use a compiler hint such as `__builtin_expect(!!(x), 1)` only after a measurement shows it is faster. Reach compiler-specific code through a macro, so that the code still compiles where the hint is not supported.
