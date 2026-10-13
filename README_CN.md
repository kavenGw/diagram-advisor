# diagram-advisor

[English](README.md)

一个「先选图、再画图」的 Agent 技能：先分析你希望用图回答的问题，推荐 2～4 种候选图类型并说明取舍，等你选定后交给 [drawio-skill](https://github.com/Agents365-ai/drawio-skill)（[中文说明](https://github.com/Agents365-ai/drawio-skill/blob/main/README_CN.md)）生成可编辑的 `.drawio` 文件。

## 依赖

- **[drawio-skill](https://github.com/Agents365-ai/drawio-skill)**：负责实际绘制，请先按其 [中文说明](https://github.com/Agents365-ai/drawio-skill/blob/main/README_CN.md) 安装。
- **[draw.io 桌面版](https://www.drawio.com/)**：drawio-skill 导出图片及部分布局功能需要。

未安装 drawio-skill 时，diagram-advisor 仍会完成分析和推荐，之后停下并询问 drawio-skill 的位置。

## 安装

Claude Code 插件（自动安装依赖 drawio-skill，固定在已验证版本）：

```
/plugin marketplace add kavenGw/diagram-advisor
/plugin install diagram-advisor@diagram-advisor
```

插件安装后技能名为 `diagram-advisor:diagram-advisor`。若之前已通过下面的方式安装过，请删除 `~/.claude/skills/diagram-advisor`，避免重复加载。

npx：

```bash
npx skills add kavenGw/diagram-advisor -g
```

手动安装（Claude Code）：

```bash
git clone https://github.com/kavenGw/diagram-advisor.git ~/src/diagram-advisor
mkdir -p ~/.claude/skills
ln -s ~/src/diagram-advisor/skills/diagram-advisor ~/.claude/skills/diagram-advisor
```

Windows 下 Git Bash 的 `ln -s` 默认是复制而非链接，请在 `cmd` 中创建 junction：

```bat
mklink /J "%USERPROFILE%\.claude\skills\diagram-advisor" "%USERPROFILE%\src\diagram-advisor\skills\diagram-advisor"
```

Codex 将同一目录链接到 `~/.agents/skills/diagram-advisor`。最终 `SKILL.md` 须位于 `<技能根目录>/diagram-advisor/SKILL.md`。

## 使用

> 用 diagram-advisor 帮我梳理登录流程里 token 刷新是怎么处理的。

1. **分析**：核心问题、读者、范围、关键对象与关系，区分事实与假设。
2. **推荐**：以表格列出候选图类型，标出推荐项。
3. **绘制**：你选定后，读取 drawio-skill 的 `SKILL.md`，按其绘制与校验流程执行。

回复语言跟随你使用的语言。

## 关于 drawio-skill 的调用方式

drawio-skill 声明了 `disable-model-invocation: true`，模型无法通过 Skill 工具调用它。因此 diagram-advisor 在交接时直接定位并读取其 `SKILL.md`，这是有意设计。

## 许可证

MIT
