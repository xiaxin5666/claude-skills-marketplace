# 磁盘清理技能

为 Claude Code 提供分等级、跨平台的磁盘空间分析与清理能力。支持 Windows、macOS、Linux。

## 安装方式

### 方式一：Git 克隆（推荐）

一次性下载所有技能，后续可以 `git pull` 更新：

```bash
# SSH
git clone git@github.com:xiaxin5666/claude-skills-marketplace.git

# 或 HTTPS
git clone https://github.com/xiaxin5666/claude-skills-marketplace.git
```

然后把你需要的技能复制到 Claude Code 技能目录：

```bash
# 安装单个技能（以 disk-cleanup 为例）
cp -r claude-skills-marketplace/skills/disk-cleanup ~/.claude/skills/

# 或安装所有技能
cp -r claude-skills-marketplace/skills/* ~/.claude/skills/
```

> **注意**：Windows 用户的技能目录是 `%USERPROFILE%\.claude\skills\`，PowerShell 中执行：
> ```powershell
> Copy-Item -Recurse claude-skills-marketplace\skills\disk-cleanup $env:USERPROFILE\.claude\skills\
> ```

### 方式二：curl / wget 直接下载单个技能

无需克隆整个仓库，只下载你需要的那个技能：

```bash
# 以 disk-cleanup 为例，先创建目录
mkdir -p ~/.claude/skills/disk-cleanup

# curl 下载
curl -o ~/.claude/skills/disk-cleanup/SKILL.md \
  https://raw.githubusercontent.com/xiaxin5666/claude-skills-marketplace/main/skills/disk-cleanup/SKILL.md

# 或 wget 下载
wget -O ~/.claude/skills/disk-cleanup/SKILL.md \
  https://raw.githubusercontent.com/xiaxin5666/claude-skills-marketplace/main/skills/disk-cleanup/SKILL.md
```

### 方式三：下载 ZIP 包

如果无法使用 Git，可以直接下载 ZIP：

1. 打开 https://github.com/xiaxin5666/claude-skills-marketplace
2. 点击绿色 **Code** 按钮 → **Download ZIP**
3. 解压后，将 `skills/` 目录下需要的技能复制到 `~/.claude/skills/`

### 方式四：手动复制

在浏览器中打开对应技能的 SKILL.md 文件，直接复制全部内容，在本地创建文件：

| 平台 | 路径 |
|------|------|
| macOS / Linux | `~/.claude/skills/<技能名>/SKILL.md` |
| Windows | `%USERPROFILE%\.claude\skills\<技能名>\SKILL.md` |

SKILL.md 内容地址（以 disk-cleanup 为例）：

```
https://raw.githubusercontent.com/xiaxin5666/claude-skills-marketplace/main/skills/disk-cleanup/SKILL.md
```

### 安装后验证

在 Claude Code 中输入 `/disk-cleanup`，如果能自动补全并执行，说明安装成功。

---

## 已有技能

| 技能 | 描述 | 支持平台 |
|------|------|----------|
| [`disk-cleanup`](./skills/disk-cleanup/SKILL.md) | 磁盘分析与清理：缓存、临时文件、应用残留、SDK 旧版本、系统还原点等。分 6 个安全等级，支持 `--dry-run` 预览模式。 | Windows / macOS / Linux |

### disk-cleanup 使用示例

```bash
/disk-cleanup                  # 交互模式，按引导选择清理等级
/disk-cleanup safe             # 仅安全缓存（浏览器缓存、npm/pip、临时文件、回收站）
/disk-cleanup standard         # 标准清理（安全缓存 + 应用缓存 + 商店缓存）
/disk-cleanup deep             # 深度清理（上述 + OEM 残留 + 旧 SDK + 重复文件）
/disk-cleanup full             # 完整清理（上述 + 系统还原点）
/disk-cleanup --dry-run        # 预览模式：仅分析，不执行删除
/disk-cleanup target=Chrome    # 针对特定项目清理
```

---

## 贡献技能

有好用的技能？欢迎分享！

1. Fork 本仓库
2. 创建你的技能目录：`skills/<技能名>/SKILL.md`
3. 将技能添加到 [`registry.json`](./registry.json) 和本 README 的技能列表中
4. 提交 Pull Request

### 技能格式

每个技能存放在 `skills/` 下的独立目录中，目录内包含一个 `SKILL.md` 文件：

```
skills/
└── 技能名/
    └── SKILL.md    # YAML 前置信息 + Markdown 指令
```

`SKILL.md` 文件结构：

```yaml
---
name: 技能名               # 必填，kebab-case，也是 / 命令名
description: "描述..."     # 强烈推荐，Claude 据此决定是否自动调用
user-invocable: true       # 是否可通过 / 菜单手动调用
argument-hint: "[参数]"    # 可选，斜杠命令的参数提示
---
```

完整示例参见 [`skills/disk-cleanup/SKILL.md`](./skills/disk-cleanup/SKILL.md)。

### 编写建议

- **一个目录一个技能** — 保持技能独立
- **清晰的命名** — 使用 kebab-case，便于搜索
- **准确的描述** — 帮助 Claude 判断何时自动调用
- **尽量跨平台** — 标注支持的操作系统
- **危险操作分等级** — 让用户控制风险

---

## 技能索引

机器可读的技能索引见 [`registry.json`](./registry.json)。
