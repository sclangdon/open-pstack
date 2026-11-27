---
name: principle-tune-for-the-supported-hardware
description: "Apply when you write, tune, or benchmark performance-sensitive code: choosing block, tile, buffer, batch, or thread-pool sizes, thresholds, SIMD or GPU code paths, compiler target flags, or keeping a change because it measured faster. Tune for the whole range of hardware the software supports, not the machine you are running on."
user-invocable: false
---

# Tune for the Supported Hardware

The machine you run on is one sample of the hardware the software will meet, and usually not a typical one. A developer box or CI runner has more cores, bigger caches, wider vectors, faster storage, and more memory than much of the field. A value or code path tuned on it can be slower, or not run at all, elsewhere.

**Failure mode:** The agent sweeps tile sizes on its machine, hard-codes the winner, sizes the thread pool to its `nproc`, and builds with `-march=native`. The benchmark shows a gain. On users' machines the tiles spill a smaller cache, the pool oversubscribes fewer cores, and the binary dies with an illegal instruction on CPUs without AVX-512.

**Pattern:**
- **Know the supported range.** Take it from the user, the project's support matrix, or its shipped build targets: the instruction-set baseline, CPU vendors and generations, core counts, cache and memory sizes, GPUs, operating systems. When the project states none, ask the user. It is a domain fact, per [Requirements Come from the Domain](../principle-requirements-come-from-the-domain/SKILL.md). Until they answer, assume the broadest range the software could ship to, and say so.
- **Hard-code no fact about this machine in the general path.** Core and thread counts, cache and cache-line sizes, page size, vector width, memory size, GPU warp or wavefront size, and timings all vary. Query them at run time, or pick a value that holds up across the range.
- **Build for the baseline.** Shipped builds target the range's lowest instruction set, never `-march=native`, `-mcpu=native`, or `target-cpu=native`.
- **A hardware-specific path may ship beside the general one.** When tuning for particular hardware (an instruction set, a vendor, a cache size, a GPU) gives a large gain on that hardware, more than the 10% [Favour Performance](../principle-favour-performance/SKILL.md) asks of assembly, ship it as a second path. The general path still ships, tuned for the whole range. The program picks the path at run time from detected features (CPUID, `getauxval`, a device query), never at build time, and runs the general path on anything else. Build and test both, forcing the general path on hardware that has the specific one. The specific path may hard-code the facts of the hardware it targets.
- **A win on one machine is a hypothesis.** Keep a tuning choice in the general path only when it wins, or at least does not lose, at the low end and on another microarchitecture or vendor in the range. When you can measure on one machine only, sweep the parameter and choose from the flat part of the curve rather than its peak, since the peak moves between machines. Prefer designs with no cliff to tune around, such as cache-oblivious algorithms. Tune at install or run time when the best value really differs across the range.
- **Report the hardware with the number.** Give the CPU model, core count, and cache and memory sizes, and say which part of the range was not measured.
- **The low end is a requirement.** A change that is faster on your machine and slower at the low end of the range is a regression, per [Requirements Are Not Trade-offs](../principle-requirements-are-not-trade-offs/SKILL.md).

When the software ships to one known machine or fleet, such as an embedded board, a console, or a named cluster, that machine is the supported range. Tune for it, and the dev box counts only when it is that machine.
