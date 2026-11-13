---
name: c-best-practices
description: C best practices. Use when reading or editing any .c or .h file, or code in a language derived from C.
paths: ["**/*.c", "**/*.h"]
---

# C best practices

Apply the **type-system-discipline** principle skill first. These rules apply to C and languages derived from it.

## Return values

- Check the return value of every non-void call. When the right response to failure is the same as to success, as with `printf` or `fclose`, cast the call to `(void)` to show that you ignore the value on purpose.
- Functions we write return `void` when they cannot fail and `bool` when they can. Return `int` only in the rare case where callers need several levels of failure. A function that must fit an external signature, such as a callback, is the exception.
- Return results through out-parameters, and construct objects in place.

  Prefer:

  ```c
  bool init_large_struct(large_struct_t *largeStruct);
  ```

  Avoid:

  ```c
  large_struct_t create_large_struct(void);
  ```

## goto

Use `goto` inside a function when it reduces complexity.

- Run shared cleanup before a function returns.

  ```c
  bool function(void) {
      bool ret = false;

      if (!something_that_can_fail())
          goto cleanup;

      // good path
      ret = true;
  cleanup:
      // cleanup resources
      return ret;
  }
  ```

- Leave deeply nested code.

  ```c
      for (int i = 0; i < MAX_I; ++i) {
          for (int j = 0; j < MAX_J; ++j) {
              for (int k = 0; k < MAX_K; ++k) {
                  if (some_early_exit()) {
                      goto next_task;
                  }
              }
          }
      }

  next_task:
      // work
  ```

- Separate optional tasks.

  ```c
      // do task1
      if (!needs_task2())
          goto optional_task3;

  optional_task2:
      // do task2

  optional_task3:
      // do task3
      if (!needs_task4())
          goto tasks_done;

  optional_task4:
      // do task4

  tasks_done:
      // work
  ```

## Struct layout

Order struct fields to reduce the struct's size. Here `type1` is 24 bytes and `type2` is 16 bytes on a 64-bit target.

```c
struct type1 {
    bool field1;
    void *field2;
    int field3;
};

struct type2 {
    void *field2;
    int field3;
    bool field1;
};

_Static_assert(sizeof(struct type2) < sizeof(struct type1), "type2 should be smaller than type1");
```

## Upgradable structures

Start every public struct with a type tag and a `pNext` pointer. A later API version adds fields in a new extension struct that callers chain through `pNext`. The original struct never changes.

```c
enum structure_type {
    VERSION1_DATA,
    VERSION1_EX_DATA, // added in version 2
};

struct version1_data {
    enum structure_type type;
    void *pNext;
    int data;
};

// added in version 2, and version1_data does not change
struct version1_ex_data {
    enum structure_type type;
    void *pNext;
    int data;
};

void do_something(struct version1_data *v1Data) {
    assert(v1Data != NULL);
    assert(v1Data->type == VERSION1_DATA);

    v1Data->data = 5;

    if (v1Data->pNext != NULL) {
        enum structure_type *nextType = v1Data->pNext;
        if (*nextType == VERSION1_EX_DATA) {
            struct version1_ex_data *exData = v1Data->pNext;
            exData->data = 6;
        }
    }
}
```

## Public headers

Public API headers in `include/` document the library for the people who call it. These comments are required. Private headers and source files keep only the comments that poteto-mode's Comments section allows.

- Open each public header with a short summary of what a user might use the library for, followed by examples of how to use it. When the library's notes in `meta/` open with a usage example, the header carries the same example.
- Put a comment above each type that says what it is and where it is used. Give each field its own comment that says what the field is for.
- Put a comment above each function that says what it is, why you would use it, and what each parameter means. A function-like macro in the public API counts as a function.

When `~/Dev/Projects/lightspeed/include/log/log.h` exists, it is a worked example.

## Types

### Declarations

- Use the plain `char` type only to store and use character values.
- Use typedefs that state size and signedness in place of the basic numeric types, such as `uint32_t` instead of `unsigned int`.

### Implicit conversion

Do not implicitly convert an expression of integer type to a different underlying type if any of these holds:

- The conversion is not to a wider integer type of the same signedness.
- The expression is complex.
- The expression is not constant and is a function argument.
- The expression is not constant and is a return expression.

Do not implicitly convert an expression of floating type to a different type if any of these holds:

- The conversion is not to a wider floating type.
- The expression is complex.
- The expression is a function argument.
- The expression is a return expression.

### Casts

- Cast a complex expression of integer type only to a type of the same signedness that is no wider than the expression's underlying type.
- Cast a complex expression of floating type only to a floating type that is the same size or narrower.
- When `~` or `<<` is applied to an operand whose underlying type is `unsigned char` or `unsigned short`, cast the result straight back to that type.

### Pointer conversion

- Convert a pointer to a function only to or from an integral type.
- Convert a pointer to an object only to or from an integral type, another pointer-to-object type, or a pointer to `void`.
- Never cast away the `const` or `volatile` qualification of the pointed-to type.
