---
name: principle-prefer-arrays
description: "Apply when choosing a collection or data structure. Start with an array. Use a map, tree, or anything more exotic only when a measurement shows it is faster."
user-invocable: false
---

# Prefer Arrays

Use an array by default. An array with a sort and a binary search, such as `qsort` and `bsearch` in C, goes a long way before you need anything else.

If you think you need a dictionary, a tree, or something more exotic, prove it. Measure it against the array version and keep it only if it is faster.
