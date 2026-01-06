# Project Introduction

## What is Hahaha?

[Hahaha](https://github.com/Napbad/Hahaha) is a modern open-source mathematics and machine learning library. It is designed for ML computation while also having strong educational value. Beyond efficient numerical computing, the project aims to make learning machine learning more intuitive and enjoyable.

## Vision

Hahaha’s core belief is to make machine learning **simple, fun, and easier to understand**. We believe that well-designed APIs and clear documentation allow developers to both enjoy programming and deeply understand the essence of machine learning algorithms.

## Main goals

1. **Build a high-performance math/ML library**
   - Provide tensor operations, matrix computation, and other foundational math capabilities
   - Support automatic differentiation (Autograd)
   - Implement common machine learning algorithms and optimizers

2. **Keep excellent implementations and design reasoning**
   - Clear code structure that is easy to read and learn from
   - Detailed docs and comments to help understand algorithmic ideas
   - Record design patterns and architecture decisions

3. **Visualize ML workflows**
   - Provide tools to visualize training processes
   - Support visualization of model structures and computation graphs
   - Make complex execution flows easier to grasp

## Architecture design

Hahaha uses a layered architecture, ranging from low-level hardware abstraction to high-level user interfaces, forming a complete stack. The overall architecture is based on modular design under the `core` directory and progresses from low to high:

### 1. Backend layer

Located under `core/include/backend/`, responsible for low-level compute:

- **Device abstraction**: `Device.h` provides a unified hardware interface
- **SIMD optimizations**: `vectorize/` contains `SimdVector.h` and `VectorizedOp.h` using CPU vector instruction sets
- **GPU compute**: `gpu/` reserves CUDA hooks (`GpuContext.h`, `GpuKernel.h`, `GpuMemory.h`)
- **Compute dispatching**: `DeviceComputeDispatcher.h` schedules compute tasks across devices

### 2. Common layer

Located under `core/include/common/`, providing base components:

- **Configuration**: `Config.h` manages system configuration
- **Type definitions**: `definitions.h` defines data types and constants
- **Operator interface**: `Operator.h` defines operator abstractions
- **Result handling**: `Res.h` unifies error handling and return values

### 3. Math layer

Located under `core/include/math/`, implementing core math ops:

- **Tensor data structures**: `ds/` includes `TensorData.h`, `TensorShape.h`, `TensorStride.h`
- **Tensor wrapper**: `TensorWrapper.h` provides higher-level tensor operation APIs
- **Core tensor class**: `Tensor.h` defines the main tensor interface

### 4. Compute layer

Located under `core/include/compute/`, implementing autograd and computation graphs:

- **Computation graph**: `graph/` contains node definitions and topological sorting
- **Compute functions**: `graph/compute_funs/` provides implementations for math operations
- **Autograd**: supports dynamic graphs, gradient computation, and backpropagation

### 5. ML layer

Located under `core/include/ml/`, implementing ML algorithms:

- **Model architectures**: `model/` includes `Linear.h`, `LinearRegression.h`, `KNearestNeighbors.h`
- **Optimizers**: `optimizer/` contains algorithms like `SGDOptimizer.h`
- **Loss functions**: `loss/` provides `MSELoss.h` and others
- **Datasets**: `dataset/` abstracts data loading and preprocessing

### 6. Display layer

Located under `core/include/display/`, providing visualization:

- **Window management**: `GlfwWindow.h` provides a GLFW-based window abstraction
- **Visualizers**: `Visualizer.h` and `Window.h` support training-process visualization

### 7. Utils layer

Located under `core/include/utils/`, providing utilities:

- **Logging**: `log/` contains a full logging framework
- **Common utilities**: `common/` provides helper data structures

### Tooling and support

- **Build system**: modern Meson + Ninja based build workflow
- **External deps**: `extern/externlibs/` includes required third-party libs such as ImGui and GLFW
- **Examples**: `examples/` contains demos like autograd, basic_usage, ml_basic_usage, and ml_visualizer
- **Tests**: `tests/` contains unit and integration tests
- **Dev tools**: `format.sh` formats and checks code style

## Quickstart

### Basic usage example

```cpp
#include <hahaha/Tensor.h>

int main() {
    // Create tensors
    auto x = hahaha::Tensor<float>::buildFromVector({1.0f, 2.0f, 3.0f, 4.0f});
    auto y = hahaha::Tensor<float>::buildFromVector({2.0f, 3.0f, 4.0f, 5.0f});

    // Compute
    auto z = x + y * 2.0f;

    // Autograd
    z.backward();

    std::cout << "Result shape: (" << z.getShape()[0] << ")" << std::endl;
    std::cout << "Gradient shape: (" << x.grad().getShape()[0] << ")" << std::endl;

    return 0;
}
```

### Machine learning example

```cpp
#include <hahaha/Tensor.h>
#include <hahaha/ml/model/LinearRegression.h>
#include <hahaha/ml/optimizer/SGDOptimizer.h>
#include <hahaha/ml/loss/MSELoss.h>

int main() {
    // Create a linear regression model
    auto model = hahaha::ml::LinearRegression<float>();

    // Prepare training data
    auto X = hahaha::Tensor<float>::buildFromVector({1.0f, 2.0f, 3.0f, 4.0f});
    auto y = hahaha::Tensor<float>::buildFromVector({2.0f, 4.0f, 6.0f, 8.0f});

    // Train the model
    for (int epoch = 0; epoch < 100; ++epoch) {
        model.train(X, y);
    }

    std::cout << "Training completed!" << std::endl;
    return 0;
}
```

## What makes the project special

### Education-oriented

- **Clear structure**: each module has detailed comments and documentation
- **Progressive learning path**: from basic math to advanced models
- **Visualization support**: make abstract algorithms more intuitive

### High performance

- **Multiple backends**: CPU, GPU, and distributed computing
- **SIMD optimizations**: make full use of modern CPU vector instructions
- **Memory optimizations**: efficient memory management and (planned) GC strategy

### Developer-friendly

- **Modern C++**: based on C++23 with strong type-safety and performance
- **Modular design**: clear architecture that is easy to extend and maintain
- **Solid tests**: high-coverage unit and integration tests

### Visualization

- **Training visualization**: real-time curves for loss/accuracy and more
- **Model structure visualization**: see network architectures directly
- **Computation graph visualization**: understand how autograd executes

## Why the name “Hahaha”?

Why not choose a cool technical name like `PyTorch` or `TensorFlow`?

Because Hahaha hopes that when you learn and use machine learning (or deep learning) to assist your daily work, you can genuinely feel happy.

We believe programming should be joyful, and learning should be fun. With well-designed APIs, clear documentation, and intuitive visualization, we hope every developer using Hahaha can enjoy the process while solving real problems.

from Napbad: It's definitely not because the author couldn't think of a good name. Definitely not. Well, that's it.
