# Build and Environment Setup

The project strongly recommends a unified development environment to ensure compatibility with C++23 features.

## Requirements

- **OS**: Linux (recommended) / Windows WSL2 / macOS (requires a recent Clang)
- **Compiler**: GCC 13+ or Clang 16+ (must fully support C++23)
- **Build tools**: Meson 1.3.2+, Ninja 1.11.1+
- **GPU (optional)**: NVIDIA GPU (CUDA 13.0+)

## Recommended approach: Docker / Devcontainer

If you use VS Code, clicking **“Reopen in Container”** is usually the easiest option.

### Build with Docker manually

```bash
# Build the image
docker build -t hahaha-dev .

# Enter the environment
docker run --gpus all -it --rm -v $(pwd):/workspace hahaha-dev
```

## Local build workflow

Run in the `repo/Hahaha` root directory:

```bash
# Initialize build directory (Debug)
meson setup builddir --buildtype=debug

# Build
ninja -C builddir

# Run unit tests
meson test -C builddir -v
```

## Common issues

- **Missing dependencies**: Meson may use `wrap` files or your system package manager. If it reports `glfw3` missing, ensure the corresponding dev package is installed.
- **C++ standard errors**: verify your compiler truly supports `-std=c++23`.
