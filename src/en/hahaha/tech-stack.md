# Tech Stack and Choices

From day one, Hahaha has aimed for **education-first** and a **pragmatic balance with performance**, so the technology choices are modern but intentionally restrained.

## Core language: C++23

We chose the latest **C++23** standard.

- **Why so new?** C++23 brings stronger template metaprogramming expressiveness (Concepts) and features like `std::stacktrace`, which help express tensor operations cleanly and improve debugging.
- **Educational value**: demonstrate how modern C++ tackles complexity in high-performance computing, instead of piling up C-style code.

## Build system: Meson + Ninja

The project uses **Meson**:

- **Readability**: `meson.build` is easy to follow, lowering the barrier for contributors to understand the build.
- **Speed**: the Ninja backend provides a very fast incremental compile experience.

## Core dependencies (extern libs)

We avoid heavy dependencies and only bring in a small set of key components:

- **GoogleTest (GTest)**: ensure each math operator has solid unit tests.
- **ImGui + GLFW**: for `MLVisualizer`, rendering real-time training curves and parameter distribution.
- **CUDA 13.0 (reserved)**: architecture hooks are prepared for future GPU acceleration.

## Tooling and infrastructure

- **Docker/Devcontainer**: provide a standardized C++23 build environment.
- **clang-format/clang-tidy**: enforce style via scripts such as `format.sh`.
