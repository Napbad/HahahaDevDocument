# Writing Style

This is not a “strict standard”, but a set of conventions that makes long-term maintenance easier.

## Recommended structure

- **Start with the conclusion**: readers usually want “how to do it / what it looks like”
- **Then provide steps**: from easy to hard, from frequent to rare
- **Finally add background**: principles, trade-offs, pitfalls

## Heading levels

- One document should solve one problem
- Keep headings short so the sidebar is easy to scan

Example:

```text
## One-sentence conclusion
## When to use
## Steps
## FAQ
```

## Code blocks

```bash
mdbook serve
```

```toml
[book]
title = "My Book"
```

## Links

- Internal links: use relative paths, e.g. `../appendix/faq.md`
- External links: add descriptive text; avoid pasting bare URLs
