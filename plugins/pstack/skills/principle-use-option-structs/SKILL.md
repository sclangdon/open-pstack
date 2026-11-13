---
name: principle-use-option-structs
description: "Apply when adding or changing function arguments. When a function takes more than four arguments, or its arguments change often, pass one options struct instead."
user-invocable: false
---

# Use Option Structs

When a function takes more than four arguments, or its arguments change often, pack them into one struct and pass that. This matters most for a public interface. In a language without structs, pass one options object.

Prefer:

```c
typedef struct args {
    int arg1;
    int arg2;
    int arg3;
    int arg4;
    int arg5;
} args_t;

void some_function(const args_t *args);
```

Avoid:

```c
void some_function(int arg1, int arg2, int arg3, int arg4, int arg5);
```
