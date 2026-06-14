---
name: comment-basic
description: Add basic standardized comments to existing source code with minimal comment-only edits and no code rewriting. Use when the user invokes /comment-basic or asks for concise comments covering file purpose, classes, functions, parameters, and return values only.
---

# Basic Code Commenting

Use this shortcut as the basic mode of `standardize-code-comments`.

## Rules

- Only add comments. Do not change logic, names, values, branches, algorithms, imports, quote style, semicolons, formatting, directory structure, or behavior.
- Use minimal edit patches when files are available. Do not rewrite or print whole files unless the user only pasted code.
- Verify that non-comment lines remain unchanged before finishing.
- Keep all valid original comments. Do not remove or rewrite them unless the user explicitly asks for comment cleanup.
- Comment only what the current code proves. Do not invent business context or architecture intent.
- Use the language's standard convention: JavaDoc, JSDoc/TSDoc, GoDoc, Google-style Python docstrings, XML docs for C#, PHPDoc, or framework-conventional comments.

## Scope

Add concise comments for:

- File header: module/file purpose, exposed capability, visible dependencies, maintainer field if unknown.
- Classes/interfaces/structs: responsibility, inheritance/implementation relation, key fields.
- Functions/methods: concrete purpose, parameters, return value, exceptions only when directly visible. For component-local functions, mention the visible props/state/hook/template binding they interact with.
- Constants/enums/globals: meaning and allowed values when inferable.

Avoid detailed inline comments except for a condition, loop, or exception path that would be hard to understand without a comment.

## Output

When files are available, edit them in place and return only changed file paths plus a short summary. When the user only pasted code, return one commented source block and a short `代码注释说明文档`.
