# 构建与环境配置

项目强制要求统一的开发环境，以确保 C++23 特性的兼容性。

## 环境要求

- **操作系统**：Linux (推荐) / Windows WSL2 / macOS (需较新 Clang)
- **编译器**：GCC 13+ 或 Clang 16+ (必须完整支持 C++23)
- **构建工具**：Meson 1.3.2+, Ninja 1.11.1+
- **显卡 (可选)**：NVIDIA GPU (CUDA 13.0+)

## 推荐方式：Docker / Devcontainer

如果你使用 VS Code，直接点击右下角的 **"Reopen in Container"** 是最省心的方式。

### 手动 Docker 构建
```bash
# 构建镜像
docker build -t hahaha-dev .

# 进入环境
docker run --gpus all -it --rm -v $(pwd):/workspace hahaha-dev
```

## 本地构建流程

在 `repo/Hahaha` 根目录下执行：

```bash
# 初始化构建目录 (Debug 模式)
meson setup builddir --buildtype=debug

# 执行编译
ninja -C builddir

# 运行单元测试
meson test -C builddir -v
```

## 常见问题

- **缺少依赖**：Meson 会尝试通过 `wrap` 或系统包管理寻找依赖。如果提示 `glfw3` 找不到，请确保系统已安装相关开发库。
- **C++ 标准报错**：请检查编译器版本是否真的支持 `-std=c++23`。


