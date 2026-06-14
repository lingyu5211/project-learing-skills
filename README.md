# Claude Code Skills：工业级代码注释技能包

这个仓库提供一组面向 Claude Code 的代码注释 Skills，核心目标是：

- 只为现有源码补充注释
- 不修改业务逻辑
- 尽量使用最小注释补丁，避免整文件重写
- 提供更适合学习、复盘、交接的细粒度注释

这套 Skills 特别适合：

- 学习开源项目
- 梳理遗留项目
- 给简历项目补充高质量注释
- 给团队协作代码补全统一注释规范

## 包含的 Skills

- `standardize-code-comments`
  主入口，默认使用深度学习向注释模式。
- `comment-basic`
  基础注释模式，只补充文件、类、函数、参数、返回值等核心注释。
- `comment-deep`
  深度注释模式，重点补充组件内部函数、Hooks、Watchers、Effects、异步流程、边界处理等细节说明。
- `doc-summary`
  只输出注释说明文档，不返回带注释源码。
- `restore-origin`
  完整保留原有注释，只补充缺失注释。
- `rule`
  输出当前技能采用的完整注释规则。

## 这套 Skills 解决什么问题

这次技能重点修正了两类常见问题：

- 注释空泛，只会写“处理数据”“执行逻辑”这种无信息量描述
- 模型为了加注释直接重写整个文件，导致 token 使用量变高，还容易引入无关改动

当前规则已经明确要求：

- 优先做“就地最小注释补丁”
- 不允许改 imports、逻辑、空行、引号风格、分号、格式
- 完成前要确认“非注释代码行保持不变”
- 对组件内函数、事件处理器、Hook、Watcher、Effect、闭包、异步状态、UI 绑定关系进行更具体说明

## 仓库结构

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

## 如何安装到 Claude Code

Claude Code 会从以下目录自动发现 Skills：

- 全局目录：`~/.claude/skills/`
- 项目目录：`.claude/skills/`

每个 Skill 都必须是独立文件夹，并且文件夹内必须包含 `SKILL.md`。

### 方式一：安装到全局目录

适合所有项目通用。

Windows PowerShell 示例：

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

### 方式二：安装到单个项目

适合只在某个项目里使用。

先进入目标项目根目录，再执行：

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

## 在 Claude Code 里怎么用

进入你的项目后启动 Claude Code：

```powershell
claude
```

然后直接输入对应命令：

```text
/standardize-code-comments
/comment-basic
/comment-deep
/doc-summary
/restore-origin
/rule
```

## 推荐使用方式

为了减少 token 消耗、避免整文件重写，建议在提示词里明确加上这些约束：

- `只添加注释`
- `就地修改文件`
- `不要输出完整源码`
- `确认非注释代码未变化`
- `只处理指定目录或指定文件`

推荐示例：

```text
/comment-deep 请只处理 src/components 目录下的文件。要求就地修改文件，只添加注释，不重写完整文件，并确认非注释代码保持不变。
```

```text
/comment-basic 请只给当前文件补充基础注释，输出保持简洁，除非必要不要返回完整源码。
```

```text
/restore-origin 请完整保留现有注释，只补充缺失注释，不改格式，不改逻辑。
```

```text
/doc-summary 请只根据当前代码输出注释说明文档和模块逻辑梳理，不返回带注释源码。
```

## 各 Skill 的适用场景

### `standardize-code-comments`

适合默认使用。你不想手动选模式时，直接用它。

### `comment-basic`

适合这些场景：

- 只想快速补齐函数注释
- 只关心文件、类、函数层级说明
- 想尽量压低 token 开销

### `comment-deep`

适合这些场景：

- 需要学习现有项目实现
- 需要解释组件内部函数行为
- 需要分析 Hook、Watcher、Effect、事件处理器、异步调用链
- 需要更细的边界、异常、状态流转说明

### `doc-summary`

适合这些场景：

- 你只想要一份总结文档
- 不想让模型直接改源码
- 想先理解模块结构和复杂逻辑

### `restore-origin`

适合这些场景：

- 老项目里已有大量历史注释
- 你不希望模型碰原注释
- 只允许“补”，不允许“改”

### `rule`

适合这些场景：

- 想查看当前完整注释规范
- 想确认技能的边界和输出规则

## 更新已有安装

如果你之前已经安装过旧版本，重新覆盖一次即可：

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

如果你是第一次创建 `~/.claude/skills` 目录，而 Claude Code 当时已经在运行，覆盖后建议重启一次 `claude`。

## 常见问题

### 1. Skills 没显示出来

检查这几项：

- 目录名是否和 Skill 名一致
- 每个 Skill 文件夹里是否存在 `SKILL.md`
- 你放置的位置是否是 `~/.claude/skills/` 或 `.claude/skills/`

### 2. 还是会改动太多代码

建议在提示词里增加这些明确限制：

- `edit files in place`
- `comments only`
- `do not rewrite full files`
- `confirm non-comment lines stayed unchanged`

同时尽量缩小范围，例如只指定：

- `src/components/Button.tsx`
- `src/hooks/useUser.ts`
- `src/views/order/`

### 3. 输出还是太长

优先这样做：

- 使用 `/comment-basic`
- 只指定 1 个文件或 1 个目录
- 明确写上 `不要返回完整源码`

### 4. 只想看说明，不想改代码

直接使用：

```text
/doc-summary
```

## 附加说明

- `code-comment-skills.zip` 仅用于下载、分享、备份。
- 真正给 Claude Code 安装时，使用的是每个 Skill 文件夹本身，不是 zip 文件。
