---
name: standardize-code-comments
description: Add objective, standardized, maintainable comments to existing source code using minimal comment-only edits without rewriting code. Use when the user provides pasted code, uploaded source files, a project archive, or a directory/file range and asks for code comments, annotation, explanation comments, learning-oriented comments, component/function syntax explanation, comment standardization, or documentation generated from current code. Supports Java, TypeScript, JavaScript, Python, Go, Vue, React, C#, PHP, and other mainstream languages with language-appropriate conventions.
---

# Industrial Code Comment Standardization

Use this skill only to comment existing code. Do not add features, rewrite code, rename symbols, change return values, reorganize files, refactor algorithms, evaluate project quality, recommend projects, or suggest technical upgrades unless the user separately asks for those outside this skill.

## Operating Contract

- Preserve the original source exactly except inserted or updated comments: logic, variables, functions, imports, return values, branch conditions, algorithms, directory structure, formatting, indentation, blank lines, quote style, semicolons, and line order must remain unchanged.
- Prefer minimal edit patches over full-file rewrites. When files are available locally, edit in place and do not print full source in the final response.
- Before finishing a file, verify that all non-comment lines are unchanged. If any non-comment code would need to change, stop and report that the requested change is outside this skill.
- Base every comment on code that is actually present. Do not invent business context, user intent, architecture goals, external behavior, or runtime guarantees that the code does not show.
- Keep valid existing comments. When the user has not requested `/restore-origin`, redundant or stale duplicate comments may be simplified, but explicitly mention that in the explanation document.
- Prefer the language's standard comment style: JavaDoc for Java, JSDoc/TSDoc for JavaScript/TypeScript, GoDoc for Go, Google-style docstrings for Python, XML documentation comments for C#, PHPDoc for PHP, and framework-conventional comments for Vue/React files.
- For mixed-language projects, apply each file's own language convention.
- Keep comments useful, concrete, and close to the code. Avoid generic statements such as "handle data", "process logic", or "execute function" unless the exact operation cannot be determined from code.

## Default Mode

Use deep-learning level by default:

- Basic: file, class/interface/struct, function/method, parameters, returns.
- Advanced: Basic plus key branches, loops, exception handling, asynchronous flow, boundary checks, and data transformation comments.
- Deep-learning: Advanced plus internal function syntax explanations, component function flow, design intent visible from code, call/dependency relationships, implicit constraints, potential risk points visible from implementation, parameter constraints, concurrency/transaction/idempotency notes when supported by code.

If the user specifies `/comment-basic`, `/comment-deep`, `/doc-summary`, or `/restore-origin`, follow that mode.

## Workflow

1. Receive the code or project scope.
   - Accept pasted single files, uploaded files/archives, or a directory tree plus requested file range.
   - If the user did not specify style, detail level, or whether to include a summary document, use language-standard style, deep-learning level, and include the explanation document.
   - If the scope is ambiguous, make a conservative assumption based on provided files and state it briefly.

2. Parse before editing.
   - Identify imports, dependencies, constants, enums, global variables, exceptions, middleware/hooks/callbacks, async functions, decorators, generics, and type constraints.
   - Mark places needing comments: empty comments, unclear names, magic numbers, implicit conversions, broad exception handling, boundary checks, retries/fallbacks, resource cleanup, and complex conditions.
   - Preserve all existing formatting and valid comments.

3. Add layered comments with concrete explanation.
   - Add a file header to every file describing module ownership visible from path/name, core responsibility, exposed capability, dependency/resource notes, maintainer field if unknown, and use scenario visible from code.
   - Comment constants, enums, and globals with meaning, allowed values/range, scope, and magic-number meaning when the code reveals it.
   - Comment classes/interfaces/structs with responsibility, role, inheritance/implementation relation, injected dependencies, attributes, defaults, access visibility, and value constraints.
   - Comment every function/method, including private/protected members, component-local handlers, hooks, callbacks, computed values, watchers, effects, memoized functions, validators, interceptors, and event handlers. Explain purpose, parameter binding, captured variables/closure state, reactive state reads/writes, side effects, return structure, exception/abnormal return paths, dependencies, caller/callee relationships when visible, and concurrency/transaction/idempotency notes when supported by code.
   - Add inline comments only for meaningful logic: branch decisions, switch cases, ternaries, loop purpose/termination, type conversion, formatting, masking, sorting/filtering/aggregation, try/catch/finally, resource release, async callbacks, timers, request interceptors, boundary validation, tolerance, fallback, and degradation.
   - For Vue/React/components, explain the internal role of component functions: props/state access, emit/dispatch calls, lifecycle/hook timing, template/render binding, controlled form updates, async loading state, cleanup behavior, and how helper functions feed UI output when visible from code.

4. Deliver output.
   - If source files are available in the workspace, modify files in place with comment-only minimal patches. Final response should list changed files and summarize comment coverage; do not paste full source unless the user asks.
   - If the user only pasted code and there is no file to edit, return a single copyable commented source block.
   - Keep final summaries compact to reduce token use. Put detailed explanation in `代码注释说明文档` only when requested or when the user supplied `/doc-summary`.

## Shortcut Modes

- `/comment-basic`: Add only essential file/class/function/parameter/return comments. Avoid detailed inline comments except where needed to prevent misunderstanding.
- `/comment-deep`: Use the default deep-learning mode.
- `/doc-summary`: Do not output commented source. Output only the explanation document based on current code.
- `/restore-origin`: Preserve every original comment exactly and only add missing comments.
- `/rule`: Output this skill's complete commenting rules and workflow.

## Refusal Boundary

If the user asks for project scoring, technology selection, code refactoring, optimization, migration, framework replacement, new feature development, project recommendation, interview expansion, or business-domain speculation, politely steer back to comment generation unless they explicitly ask to leave this skill.
