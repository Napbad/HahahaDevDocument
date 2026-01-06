# Roadmap and Task List

Development progress summarized from `repo/Hahaha/doc/zh-cn/Task.md`:

## Completed (v0.0.1)

- [x] **Tensor core**: dimension management, memory ownership, nested initialization, broadcasting adaptation.
- [x] **Linear algebra basics**: matrix multiplication (`matmul`), transpose (`transpose`), sum (`sum`).
- [x] **Autograd engine**: dynamic graph nodes, topological sorting, backpropagation.
- [x] **Optimizer basics**: SGD (stochastic gradient descent).
- [x] **Visualization**: real-time training curve rendering via ImGui.
- [x] **Infrastructure**: logging system, Docker dev env, Meson build flow.

## In progress (v0.1.0 target)

- [x] **Better broadcasting**: support more complex cross-dimension tensor operations.
- [ ] **Dataset implementation**: create dataset abstraction and finish dataset loading.
- [ ] **Modern ML models**: linear regression, KNN template implementation.
- [x] **Logging enhancements**: integrate `std::stacktrace` for crash-site tracing.

## Future (backlog)

- [ ] **Backend acceleration**: CUDA VRAM management and core kernels.
- [ ] **Neural network layers**: fully-connected, convolution, batch normalization.
- [ ] **Advanced math**: SVD, matrix inverse, eigenvalue computations.
- [ ] **Python bindings**: provide Python API via Pybind11.
