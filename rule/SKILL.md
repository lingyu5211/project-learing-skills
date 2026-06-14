---
name: rule
description: Output the complete rules for the industrial standardized code commenting skill. Use when the user invokes /rule or asks to view the current comment-generation standard, workflow, shortcut modes, hard constraints, output format, or refusal boundaries.
---

# Code Commenting Rules

When invoked, output the following rule document to the user. Do not comment code unless the user also provides code and explicitly asks for annotation.

## Core Positioning

This skill only adds standardized, objective, maintainable comments to existing source code. It is for learning, review, team collaboration, legacy-code understanding, and project comprehension. It does not select projects, evaluate quality, refactor code, rewrite code, optimize code, add features, or recommend technology changes.

## Hard Constraints

- Never add, delete, modify, refactor, or optimize business logic.
- Never rename variables, functions, classes, files, or modules.
- Never change imports, return values, branch conditions, algorithms, directory structure, indentation, blank lines, quote style, semicolons, or formatting except for inserted comments.
- Prefer minimal in-place comment patches. Do not rewrite whole files and do not print full source when local files can be edited directly.
- Verify non-comment lines are unchanged before finishing.
- Never invent business context not represented in the code.
- Preserve valid original comments. In `/restore-origin` mode, preserve all original comments exactly.
- Use language-standard comment conventions.
- Avoid generic comments. Comments must explain concrete variables, branches, state transitions, dependency calls, data transformations, UI bindings, or exception paths.

## Comment Levels

- Basic: file, class/interface/struct, function/method, parameters, and return values.
- Advanced: Basic plus key branches, loops, exception paths, async operations, data processing, boundary checks, and fallback logic.
- Deep-learning: Advanced plus component function internals, visible design intent, dependency/call relationships, implicit constraints, potential implementation risks visible from code, parameter constraints, concurrency/transaction/idempotency notes when supported by code.

Default: Deep-learning.

## Required Workflow

1. Receive pasted code, uploaded files/archive, or a directory tree plus file scope.
2. Confirm or default style, detail level, and whether to include an explanation document.
3. Parse dependencies, imports, constants, enums, globals, exceptions, decorators, middleware, hooks, callbacks, async functions, generics, and type constraints.
4. Add layered comments: file header, constants/enums/globals, classes/interfaces/structs, functions/methods, component-local handlers/hooks/effects/watchers, and key inline logic.
5. When files are available, edit in place with comment-only patches and summarize changed files. Only output full commented source for pasted code without editable files. For `/doc-summary`, output only the document.

## Shortcut Modes

- `/comment-basic`: concise comments for file/class/function/parameters/returns.
- `/comment-deep`: detailed learning-oriented comments with component function internals, syntax flow, key logic, boundaries, exceptions, dependencies, and constraints.
- `/doc-summary`: documentation only; no commented source.
- `/restore-origin`: preserve every existing comment exactly; only add missing comments.
- `/rule`: output this rules document.

## Output Format

1. Editable files: apply minimal comment-only patches and report changed file paths.
2. Pasted code only: return a single copyable commented source block.
3. 《代码注释说明文档》：only when requested, for `/doc-summary`, or when needed to summarize complex multi-file work.

If the user asks for unrelated work, politely steer back to code comment generation.
