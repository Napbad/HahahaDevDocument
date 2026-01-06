# Autograd (Design)

The corresponding Chinese page (`src/zh/design/autograd.md`) is currently empty in the source repository. This English page provides a **starter outline** for future design content.

## Suggested topics

- Goals / non-goals (dynamic graph vs static graph; educational clarity)
- Graph data structures: nodes, edges, topological ordering
- Gradient storage and accumulation semantics
- Backward API: `backward()` behavior and entry points
- Operator definitions and derivative rules
- Memory management and lifetime during backprop
- Debugging: tracing, `std::stacktrace`, graph visualization hooks
- Testing strategy (numerical gradient checks + edge cases)
