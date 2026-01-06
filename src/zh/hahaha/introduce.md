# 项目介绍

## 什么是 Hahaha？

[Hahaha](https://github.com/Napbad/Hahaha) 是一个现代化的开源数学和机器学习库，专为机器学习计算而设计，同时具备强大的教育价值。它不仅提供了高效的数值计算功能，还致力于让机器学习的学习过程更加直观和有趣。

## 项目愿景

Hahaha 的核心理念是让机器学习变得简单、有趣且易于理解。我们相信，通过精心设计的 API 和清晰的文档，可以让开发者在享受编程乐趣的同时，深入理解机器学习算法的本质。

## 主要目标

1. **构建高性能数学/ML库**
   - 提供张量运算、矩阵计算等基础数学功能
   - 支持自动微分（Autograd）功能
   - 实现常见的机器学习算法和优化器

2. **优秀的代码实现与设计思路记录**
   - 代码结构清晰，易于理解和学习
   - 详细的文档和注释，帮助开发者理解算法原理
   - 设计模式和架构决策的详细记录

3. **可视化机器学习过程**
   - 提供训练过程的可视化工具
   - 支持模型结构和计算图的可视化
   - 让复杂的算法执行过程变得直观

## 架构设计

Hahaha 采用分层架构设计，从底层硬件抽象到高层用户接口，形成了一个完整的技术栈。整体架构基于 `core` 目录下的模块化设计，从底层到高层递进：

### 1. Backend 层（后端层）
位于 `core/include/backend/` 目录，负责底层的计算功能实现：
- **设备抽象**：`Device.h` 提供统一的硬件接口
- **SIMD 计算优化**：`vectorize/` 子目录下的 `SimdVector.h` 和 `VectorizedOp.h` 利用 CPU 向量指令集
- **GPU 计算**：`gpu/` 子目录预留 CUDA 接口（`GpuContext.h`, `GpuKernel.h`, `GpuMemory.h`）
- **计算分发**：`DeviceComputeDispatcher.h` 实现跨设备的计算任务调度

### 2. Common 层（公共层）
位于 `core/include/common/` 目录，提供基础组件：
- **配置管理**：`Config.h` 管理系统配置
- **类型定义**：`definitions.h` 定义数据类型和常量
- **操作符接口**：`Operator.h` 定义运算符抽象
- **结果处理**：`Res.h` 统一错误处理和返回值

### 3. Math 层（数学层）
位于 `core/include/math/` 目录，实现核心数学运算：
- **张量数据结构**：`ds/` 子目录包含 `TensorData.h`, `TensorShape.h`, `TensorStride.h`
- **张量包装器**：`TensorWrapper.h` 提供高层张量操作接口
- **核心张量类**：根目录的 `Tensor.h` 定义张量主接口

### 4. Compute 层（计算层）
位于 `core/include/compute/` 目录，实现自动微分和计算图：
- **计算图**：`graph/` 子目录包含节点定义和拓扑排序
- **计算函数**：`graph/compute_funs/` 提供各种数学运算的具体实现
- **自动微分**：支持动态计算图的梯度计算和反向传播

### 5. ML 层（机器学习层）
位于 `core/include/ml/` 目录，实现机器学习算法：
- **模型架构**：`model/` 子目录包含 `Linear.h`, `LinearRegression.h`, `KNearestNeighbors.h`
- **优化器**：`optimizer/` 包含 `SGDOptimizer.h` 等优化算法
- **损失函数**：`loss/` 提供 `MSELoss.h` 等损失计算
- **数据集**：`dataset/` 抽象数据加载和预处理接口

### 6. Display 层（显示层）
位于 `core/include/display/` 目录，提供可视化功能：
- **窗口管理**：`GlfwWindow.h` 基于 GLFW 的窗口抽象
- **可视化器**：`Visualizer.h` 和 `Window.h` 支持训练过程可视化

### 7. Utils 层（工具层）
位于 `core/include/utils/` 目录，提供辅助功能：
- **日志系统**：`log/` 子目录包含完整的日志框架
- **公共工具**：`common/` 提供辅助数据结构

### 工具与支持
- **构建系统**：基于 Meson + Ninja 的现代化构建流程
- **外部依赖**：`extern/externlibs/` 包含 ImGui, GLFW 等必要的第三方库
- **示例代码**：`examples/` 目录提供 autograd、basic_usage、ml_basic_usage、ml_visualizer 等示例
- **测试套件**：`tests/` 目录包含完整的单元测试和集成测试
- **开发工具**：`format.sh` 脚本提供代码格式化和检查功能

## 快速开始

### 基本使用示例

```cpp
#include <hahaha/Tensor.h>

int main() {
    // 创建张量
    auto x = hahaha::Tensor<float>::buildFromVector({1.0f, 2.0f, 3.0f, 4.0f});
    auto y = hahaha::Tensor<float>::buildFromVector({2.0f, 3.0f, 4.0f, 5.0f});

    // 执行计算
    auto z = x + y * 2.0f;

    // 自动微分
    z.backward();

    std::cout << "Result shape: (" << z.getShape()[0] << ")" << std::endl;
    std::cout << "Gradient shape: (" << x.grad().getShape()[0] << ")" << std::endl;

    return 0;
}
```

### 机器学习示例

```cpp
#include <hahaha/Tensor.h>
#include <hahaha/ml/model/LinearRegression.h>
#include <hahaha/ml/optimizer/SGDOptimizer.h>
#include <hahaha/ml/loss/MSELoss.h>

int main() {
    // 创建线性回归模型
    auto model = hahaha::ml::LinearRegression<float>();

    // 准备训练数据
    auto X = hahaha::Tensor<float>::buildFromVector({1.0f, 2.0f, 3.0f, 4.0f});
    auto y = hahaha::Tensor<float>::buildFromVector({2.0f, 4.0f, 6.0f, 8.0f});

    // 训练模型
    for (int epoch = 0; epoch < 100; ++epoch) {
        model.train(X, y);
    }

    std::cout << "Training completed!" << std::endl;
    return 0;
}
```

## 项目特色

### 🎯 教育导向
- **清晰的代码结构**：每个模块都有详细的注释和文档
- **渐进式学习**：从基础数学到复杂模型的完整学习路径
- **可视化支持**：让抽象的算法变得直观可见

### 🚀 高性能
- **多后端支持**：CPU、GPU、分布式计算
- **SIMD优化**：充分利用现代CPU的向量指令
- **内存优化**：高效的内存管理和垃圾回收

### 🛠️ 开发者友好
- **现代C++**：使用C++23标准，提供类型安全和性能
- **模块化设计**：清晰的架构，便于扩展和维护
- **完善的测试**：高覆盖率的单元测试和集成测试

### 📊 可视化
- **训练过程可视化**：实时显示loss、accuracy等指标
- **模型结构可视化**：直观展示神经网络架构
- **计算图可视化**：理解自动微分的执行过程

## 为什么叫做 Hahaha？

为什么不取一个像 `PyTorch`、`TensorFlow` 那样的酷炫技术名字呢？

因为 Hahaha 希望你在学习机器学习、使用机器学习（又或者是深度学习）算法辅助完成自己每天的日常工作的时候，能够让你真心地感到高兴！

我们相信，编程应该是一件快乐的事情，学习应该是一件有趣的事情。通过精心设计的 API、清晰的文档和直观的可视化，我们希望让每个使用 Hahaha 的开发者都能在解决问题的同时，享受到编程带来的乐趣。

就像听到一个有趣的笑话时，你会情不自禁地笑出声一样，我们希望 Hahaha 能成为你编程旅程中的快乐源泉！😄

来自Napbad：这绝对不是因为作者想不出好名字。绝对不是。嗯，是这样。
