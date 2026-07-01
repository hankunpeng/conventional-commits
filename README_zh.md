# 约定式提交 (Conventional Commits)

简体中文 | [English](./README.md)

在 Git 仓库中强制执行、验证、检查和管理 [约定式提交 (Conventional Commits)](https://www.conventionalcommits.org/zh-hans/)。本工具包可帮助您规范化提交消息、自动生成语义化变更日志，并安装 Git 钩子以实现自动执行。

## 功能特性

本工具包提供以下功能来支持您工作流中的约定式提交：

- **提交信息检查** — 根据约定式提交规范验证提交信息。
- **变更日志生成** — 从 Git 历史记录中自动生成分组的变更日志。
- **Git 钩子安装** — 设置 `commit-msg` 钩子，在每次提交时自动执行规范检查。
- **完整示例参考** — 包含正确和错误提交格式的参考示例。
- **规范说明引用** — 提供约定式提交 1.0.0 规范的快速参考摘要。

## 提交消息格式

约定式提交遵循结构化的布局，以确保整个提交历史的一致性和可读性：

```text
<type>[optional scope][optional !]: <description>

[optional body]

[optional footer(s)]
```

### 支持的类型

检查器支持以下标准及常见的提交类型：

| 类型 | 描述 |
|------|-------------|
| `feat` | 新功能 |
| `fix` | Bug 修复 |
| `docs` | 文档变更 |
| `style` | 格式调整（不影响代码逻辑） |
| `refactor` | 代码重构（既不是新功能也不是 Bug 修复） |
| `perf` | 性能优化 |
| `test` | 新增或修正测试 |
| `build` | 构建系统或外部依赖变更 |
| `ci` | CI 配置文件变更 |
| `chore` | 日常维护 |
| `revert` | 撤销之前的提交 |

## 前提条件

在安装和运行本仓库中的脚本之前，请确保您的系统满足以下前提条件：

- **Bash**（v4.0 或更高版本，已安装在系统中 — 脚本可以直接在 Zsh、Fish 或其他 Shell 中执行）
- **Git**
- 标准 Unix 工具（`sed`、`awk`、`grep`）

## 安装方法

本仓库是一个兼容多个智能体（Agent）平台的 AI 智能体技能。

### 方法 1：全局安装（适用于所有项目）

将本仓库克隆到您智能体平台的全局技能目录下，使其在每个项目中都可用：

```bash
cd ~/.agents/skills/
git clone https://github.com/hankunpeng/conventional-commits.git
```

该技能将被**自动发现** — 无需额外配置。

### 方法 2：项目级安装（推荐 — 仅适用于单个项目）

克隆本仓库并将其链接到您项目的 `.agents/skills/` 目录中：

```bash
# 克隆技能仓库
cd ~/your_path
git clone https://github.com/hankunpeng/conventional-commits.git

# 创建符号链接（软链接）
cd ~/your_project_root
mkdir -p .agents/skills
ln -s ~/your_path/conventional-commits .agents/skills/conventional-commits
```

该技能将**仅针对当前项目自动发现**。

### 验证安装

安装完成后，可以让 AI 智能体检查一条提交消息以确认技能是否正常工作：

```
> lint this commit message: "feat(auth): add OAuth2 support"
```

如果技能加载正确，它将使用 `scripts/commit-lint.sh` 来验证该消息。

## 快速上手

您可以使用提供的脚本来检查您的提交消息、安装钩子或生成变更日志。

### 检查提交消息

要根据规范验证提交消息，请运行 `commit-lint.sh` 脚本：

```bash
~/your_path/conventional-commits/scripts/commit-lint.sh "feat(auth): add email verification"
# ✔ Commit message style is valid!

~/your_path/conventional-commits/scripts/commit-lint.sh "added new login page"
# ✗ Invalid commit message format.
```

### 安装 Git 钩子

在仓库中自动检查每次提交的消息（如果未提供路径，则默认为当前目录）：

```bash
~/your_path/conventional-commits/scripts/install-git-hook.sh ~/your_repo
# ✔ Installed commit-msg git hook successfully
```

### 生成变更日志

要从 Git 提交历史中创建语义化变更日志，请使用版本范围运行 `generate-changelog.sh` 脚本：

```bash
./scripts/generate-changelog.sh HEAD~10..HEAD
./scripts/generate-changelog.sh v1.0.0..v1.1.0 v1.1.0
```

**示例输出：**

```markdown
# Changelog

## v1.1.0 (2026-06-30)

### Features

- **auth**: add email verification (a1b2c3d)

### Bug Fixes

- fix memory leak in parser (e4f5g6h)
```

## 项目结构

本仓库包含以下文件和目录：

```
conventional-commits/
├── SKILL.md                              # Gemini CLI 技能定义
├── README.md                             # 英文说明文档
├── LICENSE                               # MIT 许可证
├── examples/
│   └── commit-messages.md                # 正确和错误的提交示例
├── references/
│   └── conventional-commits-spec.md      # 规范摘要（中文）
└── scripts/
    ├── commit-lint.sh                    # 提交消息检查器
    ├── generate-changelog.sh             # 变更日志生成器
    └── install-git-hook.sh               # Git 钩子安装器
```

## 示例参考

有关有效和无效提交消息示例的完整集合，请参阅 [examples/commit-messages.md](examples/commit-messages.md)。

**快速有效示例：**

```
feat: add dark mode toggle
fix(parser): handle empty input without crash
refactor(api)!: rename user endpoints
```

## 规范引用

使用以下引用来深入了解约定式提交规范：

- 参阅 [references/conventional-commits-spec.md](references/conventional-commits-spec.md) 获取写成**中文**的简明规范摘要。
- 访问 [约定式提交 1.0.0 官方网站](https://www.conventionalcommits.org/zh-hans/) 以获取官方中文规范与指南。
- 了解约定式提交如何与 [语义化版本 (Semantic Versioning)](https://semver.org/) 结合使用。

## 许可证

本项目采用 [MIT 许可证](LICENSE) 进行许可。
