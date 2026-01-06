# HahahaDevDocument

Development notes, design docs, and architecture decisions for the **[Hahaha](https://github.com/Napbad/Hahaha)** project.

## Language

This repository is organized language-first under `src/`:

- **English**: `src/en/` (start at `src/en/README.md`)
- **中文**：`src/zh/`（从 `src/zh/README.md` 开始）

When built, you can access content via:

- **English**: `.../en/...`
- **中文**：`.../zh/...`

## Fast preview & build

- **Preview (both languages)**:

```bash
mdbook serve
```

- **Build (both languages)**:

```bash
mdbook build
```

## Directory convention

Under `src/`, we **group by language first**, then by topic:

- `src/en/<section>/...`
- `src/zh/<section>/...`
