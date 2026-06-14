# Claude Code Skills: Industrial Code Commenting

This repository contains a Claude Code skill set focused on adding objective, standardized comments to existing source code without changing business logic.

## Included Skills

- `standardize-code-comments`
  Default entry for deep, learning-oriented code comments.
- `comment-basic`
  Add concise file, class, function, parameter, and return comments.
- `comment-deep`
  Add detailed comments for internal logic, component functions, hooks, watchers, effects, async flow, and boundary handling.
- `doc-summary`
  Generate only the comment explanation document, without returning commented source.
- `restore-origin`
  Preserve all original comments and only supplement missing comments.
- `rule`
  Output the full commenting rules used by this skill set.

## Design Goals

- Only add comments. Do not change business logic.
- Prefer minimal in-place comment patches over full-file rewrites.
- Keep non-comment code lines unchanged.
- Explain concrete logic instead of producing vague comments.
- Improve readability for source learning, review, and handoff.

## Repository Structure

```text
.
|-- README.md
|-- code-comment-skills.zip
|-- standardize-code-comments/
|   |-- SKILL.md
|   `-- agents/openai.yaml
|-- comment-basic/
|   |-- SKILL.md
|   `-- agents/openai.yaml
|-- comment-deep/
|   |-- SKILL.md
|   `-- agents/openai.yaml
|-- doc-summary/
|   |-- SKILL.md
|   `-- agents/openai.yaml
|-- restore-origin/
|   |-- SKILL.md
|   `-- agents/openai.yaml
`-- rule/
    |-- SKILL.md
    `-- agents/openai.yaml
```

## Install For Claude Code

Claude Code discovers skills from either:

- Global scope: `~/.claude/skills/`
- Project scope: `.claude/skills/`

Each skill must be an individual folder containing `SKILL.md`.

### Install Globally On Windows PowerShell

```powershell
$src = "C:\path\to\this\repository"
$dest = "$HOME\.claude\skills"

New-Item -ItemType Directory -Force -Path $dest | Out-Null

$skills = @(
  "standardize-code-comments",
  "comment-basic",
  "comment-deep",
  "doc-summary",
  "restore-origin",
  "rule"
)

foreach ($skill in $skills) {
  Copy-Item -Recurse -Force "$src\$skill" "$dest\$skill"
}
```

### Install In A Single Project

Run the following from the target project root:

```powershell
$src = "C:\path\to\this\repository"
$dest = ".claude\skills"

New-Item -ItemType Directory -Force -Path $dest | Out-Null

$skills = @(
  "standardize-code-comments",
  "comment-basic",
  "comment-deep",
  "doc-summary",
  "restore-origin",
  "rule"
)

foreach ($skill in $skills) {
  Copy-Item -Recurse -Force "$src\$skill" "$dest\$skill"
}
```

## How To Use In Claude Code

Start Claude Code in your project:

```powershell
claude
```

Then invoke a skill directly:

```text
/standardize-code-comments
/comment-basic
/comment-deep
/doc-summary
/restore-origin
/rule
```

## Recommended Prompts

Use these prompts to reduce token usage and avoid full-file rewrites:

```text
/comment-deep Please annotate only files under src/components. Edit files in place, add comments only, do not rewrite full files, and confirm non-comment code stayed unchanged.
```

```text
/comment-basic Please add concise comments to the current file only. Keep the output short and avoid returning the full source unless needed.
```

```text
/restore-origin Preserve all original comments exactly. Only add missing comments and do not reformat or rewrite code.
```

```text
/doc-summary Based on the current code, output only a comment explanation document and module logic summary.
```

## Commenting Behavior

This skill set is tuned to avoid two common problems:

- Vague comments such as "handle data" or "process logic"
- Full-file regeneration that increases token cost

The current rules explicitly require:

- Minimal comment-only edits when files are editable
- No import, logic, formatting, blank-line, quote-style, or semicolon changes
- Concrete explanations for component-local functions, hooks, watchers, effects, event handlers, closures, async sequencing, and UI state flow

## Update Existing Installation

If you already installed an older version, copy the folders again and overwrite the existing ones:

```powershell
$src = "C:\path\to\this\repository"
$dest = "$HOME\.claude\skills"

$skills = @(
  "standardize-code-comments",
  "comment-basic",
  "comment-deep",
  "doc-summary",
  "restore-origin",
  "rule"
)

foreach ($skill in $skills) {
  Copy-Item -Recurse -Force "$src\$skill" "$dest\$skill"
}
```

If Claude Code was already running when you first created the skills directory, restart `claude`.

## Troubleshooting

- Skill not visible:
  Make sure the directory name matches the skill name and that each folder contains `SKILL.md`.
- Changes still feel too broad:
  Add "edit files in place", "comments only", and "confirm non-comment lines stayed unchanged" to the prompt.
- Output is still too verbose:
  Limit the file scope, such as `src/components/Button.tsx`, and prefer `/comment-basic` for lighter runs.

## Notes

- `code-comment-skills.zip` is included for convenient download and sharing.
- The skill folders are the real installation units. Claude Code does not install from the zip directly.
