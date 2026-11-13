---
name: principle-vet-third-party-libraries
description: "Apply when choosing between a third-party library and your own implementation. Use the library only when it meets every listed condition."
user-invocable: false
---

# Vet Third-Party Libraries

Use a third-party library instead of your own implementation only when all of these hold:

- It does the required job with no compromise to our needs.
- The work is not on a critical performance path.
- It is widely used and well supported.
- It is open source.
- Its licence allows use in closed-source code.
- Its licence allows commercial use without a fee.
