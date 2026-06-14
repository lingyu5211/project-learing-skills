---
name: comment-deep
description: Add deep learning-oriented standardized comments to existing source code with minimal comment-only edits and no code rewriting. Use when the user invokes /comment-deep or asks for detailed comments explaining component functions, internal syntax flow, key logic, branches, boundaries, exceptions, dependencies, parameter constraints, and hidden implementation assumptions visible from code.
---

# Deep Code Commenting

Use this shortcut as the deep-learning mode of `standardize-code-comments`.

## Rules

- Only add comments. Never modify business logic, variable names, functions, imports, return values, conditions, algorithms, formatting, blank lines, quote style, semicolons, or directory structure.
- Use minimal edit patches when files are available. Do not regenerate, reformat, or print whole files unless the user only pasted code.
- Verify that non-comment lines remain unchanged before finishing.
- Preserve valid original comments unless the user allows cleanup. Never delete original comments in `/restore-origin` mode.
- Keep comments objective and code-grounded. Do not infer business stories, product intent, or architecture not represented in the code.
- Avoid empty comments. Every comment must name the specific variable, branch condition, state transition, dependency call, data transformation, or UI binding it explains.
- Use the file language's conventional format: JavaDoc, JSDoc/TSDoc, GoDoc, Google-style docstrings, XML docs for C#, PHPDoc, or framework-native comments.

## Required Comment Layers

- File header: purpose, module/path-based ownership if visible, external dependencies/resources, exposed capability, maintainer field if unknown, and code-visible use scenario.
- Constants/enums/globals: meaning, constraints, allowed values, scope, and magic-number meaning when visible.
- Classes/interfaces/structs: responsibility, design role visible from code, inheritance/implementation relationship, injected dependencies, field meanings, defaults, visibility, and constraints.
- Functions/methods: purpose, design intent visible from implementation, all parameters, required/optional status if inferable, type/range/constraint, return structure, abnormal return values, thrown/caught exceptions and triggers, caller/callee dependencies, idempotency/transaction/concurrency notes when code supports them.
- Component and UI functions: explain props/state reads, state setters, refs, computed values, watchers, effects, memo/callback dependencies, emit/dispatch calls, event handler binding, template/render usage, async loading/error state, cleanup behavior, and how helper return values affect UI output when visible from code.
- Internal syntax flow: explain non-obvious destructuring, optional chaining, nullish coalescing, spread/rest, closures, currying, higher-order callbacks, promise chains, async/await sequencing, generic/type narrowing, decorators, annotations, dependency injection, and framework-specific hooks only where they affect the function's behavior.
- Inline comments: only for complex branches, switch cases, ternaries, loop purpose/termination, type conversion, formatting, masking, sorting/filtering/aggregation, try/catch/finally, resource release, async callbacks, timers, interceptors, boundary checks, fallbacks, and degradation paths.

## Output

When files are available, edit them in place and return only changed file paths plus a concise coverage summary. Do not paste full source by default. When the user only pasted code, return one copyable commented source block plus a compact `代码注释说明文档`.
