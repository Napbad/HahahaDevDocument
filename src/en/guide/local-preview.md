# Local Preview

## Install mdBook

mdBook is a Rust tool. Installing via `cargo` is recommended:

```bash
cargo install mdbook --locked
```

If you don’t have the Rust toolchain yet, install Rust first (we recommend `rustup`).

## Start the preview server

Run in the repository root:

```bash
mdbook serve
```

By default it listens on `http://localhost:3000` and auto-reloads when you edit Markdown under `src/` (including `src/en/` and `src/zh/`).

You can access languages via paths:

- English: `/en/...`
- Chinese: `/zh/...`

## Build static files

```bash
mdbook build
```

The output directory defaults to `book/` (configured by `[build].build-dir` in `book.toml`).
