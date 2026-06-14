---
name: restore-origin
description: Preserve every original source-code comment exactly and only add missing standardized comments with minimal comment-only edits. Use when the user invokes /restore-origin or asks to keep all existing comments unchanged while supplementing absent file, class, function, component handler, parameter, return, constant, enum, or key-logic comments.
---

# Preserve Original Comments

Use this shortcut when original comments must remain untouched.

## Rules

- Do not delete, rewrite, move, merge, translate, or simplify any existing comment.
- Only add missing comments around existing code.
- Do not modify business logic, names, values, branches, algorithms, imports, formatting, indentation, blank lines, quote style, semicolons, or directory structure.
- Use minimal edit patches when files are available. Do not rewrite or print whole files unless the user only pasted code.
- Verify that all pre-existing non-comment lines and original comment lines remain unchanged.
- Keep new comments objective and based only on visible code.
- Use language-standard comment formats: JavaDoc, JSDoc/TSDoc, GoDoc, Google-style docstrings, XML docs for C#, PHPDoc, or framework-native comments.

## Comment Targets

Supplement missing comments for:

- File headers.
- Constants, enums, and global variables.
- Classes, interfaces, structs, attributes, and member variables.
- Public, protected, private, sync, async, callback, hook, decorator, generic functions/methods, component-local handlers, watchers, effects, computed values, validators, and event handlers.
- Non-obvious internal syntax and component behavior: captured variables, props/state reads, setters, refs, emit/dispatch calls, async sequence, cleanup, template/render binding, and helper return values when visible from code.
- Important branches, loops, conversions, data formatting, exception handling, cleanup, async flow, boundary checks, fallback, and degradation logic.

## Output

When files are available, edit them in place and return only changed file paths plus a short summary that original comments were retained. When the user only pasted code, return one commented source block and a compact `代码注释说明文档`.
