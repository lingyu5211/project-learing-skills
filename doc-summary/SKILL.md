---
name: doc-summary
description: Generate only a code comment explanation document for existing source code without returning modified or commented source files. Use when the user invokes /doc-summary or asks for a documentation-only summary of current code comments, module flow, complex logic, implicit constraints, and boundary scenarios.
---

# Code Comment Summary Document

Use this shortcut when the user wants documentation only. Do not output rewritten source code.

## Rules

- Do not modify, rewrite, optimize, refactor, or evaluate the source code.
- Base every statement on visible code. Do not invent business context or implementation intent.
- Preserve neutrality: summarize what the code does, not whether it is good or bad.

## Document Structure

Output `代码注释说明文档` with:

- Adopted comment convention by language: JavaDoc, JSDoc/TSDoc, GoDoc, Google-style docstrings, XML docs, PHPDoc, or framework convention.
- File/module responsibilities visible from file names, paths, imports, and exports.
- Core execution flow and dependency/call relationships visible from code.
- Key complex logic blocks: branches, loops, async flow, component-local functions, hooks/watchers/effects, event handlers, state transitions, data transformation, exception handling, fallback/degradation, resource cleanup.
- Internal syntax explanations for non-obvious constructs: destructuring, spread/rest, closures, higher-order callbacks, promise chains, async/await sequencing, type narrowing, decorators, annotations, and framework hooks when visible.
- Implicit constraints and boundary scenarios visible from validation, conditions, types, default values, and exception paths.
- Multi-file project summary when multiple files are supplied.

Avoid returning commented source unless the user changes the request.
