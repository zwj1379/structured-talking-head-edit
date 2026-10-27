# slbb-chatcut-ckb

**结构化口播精剪 Skill**（配合 ChatCut Desktop 使用）

当前版本：**v2.9.0** · 打包日期：2026-10-25

本仓库是该技能的主发布仓库。适合为单人竖版口播（约 1～5 分钟）做「结构理解 → 爆点前置 → 语音精剪 → 视觉节奏 → 字幕 → 预览验收」的完整剪辑。规则按需路由到 `references/`，不把所有项目套进同一种节奏模板。

---

## 仓库内容

| 路径 | 说明 |
| --- | --- |
| `SKILL.md` | 主规则与路由框架（v2.9.0） |
| `references/` | 分域细则：音频/变速/降噪、B-roll 与真人窗、字幕与导出、ChatCut 排错 |
| `evals/` | 自检用例 |
| `agents/` | 宿主 agent 配置入口 |
| `新任务提示词.txt` | 新会话启动提示词，直接复制粘贴 |
| `README.txt` | 本版规则速查 |

> 原 `slbb-chatcut-oneclip` 已由本技能 + eian-riso-broll 组合取代。

---

## 配套：eian-riso-broll（Riso 信息动画，可选）

本技能可搭配 **eian-riso-broll** 生成 Riso 孔版风信息动画 B-roll（数字冲击 / 流程 / 前后对比 / 关键引述等 10 个模板，1080×1920 竖版、无音轨）。

**该技能是第三方独立包，采用 Eian 个人非商业使用许可 1.0，禁止再分发、禁止公开**，因此本仓库不包含其文件，仅提供官方获取途径：

```bash
git clone https://github.com/YIAN6557/eian-riso-broll.git
```

安装后在对应宿主中与 slbb-chatcut-ckb 并排使用即可。

---

## 安装到宿主

### 通道 A：WorkBuddy（MCP 连接器）

1. 将本仓库内容放入 `~/.workbuddy/skills/slbb-chatcut-ckb/`
2. `git clone https://github.com/YIAN6557/eian-riso-broll.git ~/.workbuddy/skills/eian-riso-broll`
3. 确认 `~/.workbuddy/mcp.json` 中 ChatCut MCP 条目存在（文件名**没有前导点**）
4. 用「新任务提示词.txt」开新会话，或直接说：用 slbb-chatcut-ckb + eian-riso-broll 帮我精剪这条口播并配 Riso 动画

### 通道 B：豆包工作（内置 ChatCut 插件）

1. 插件商店启用 ChatCut 插件，确认 ChatCut Desktop 在后台运行
2. 把本仓库内容（或整个仓库 zip）拖进对话框，AI 会解压装到 `.user_skills/slbb-chatcut-ckb/`
3. eian-riso-broll 同样方式从官方仓库获取安装
4. 重启豆包工作，新开会话验证

---

## v2.9.0 核心规则（节选）

- **先理解后动手**：按真实口播的语义结构决定删改和节奏，不套统一模板。
- **爆点前置**：只能使用原视频中真实说过的完整内容，前置后检查衔接与正文去重。
- **速度与声音"先分析、后决定"**：整体变速不是默认动作；降噪先分析、A/B 验证，不需要就跳过。
- **B-roll 按内容决策**：数量、静态或动态、是否带真人窗由内容与用户偏好决定；无窗 B-roll 需用户明确撤销，不靠模板密度自行省略。
- **`riso-presenter-248` preset（可选）**：仅当用户明确选择 Riso 动态真人窗或项目已冻结规格时启用——V2 净版 Riso + V3 独立 248×248 无声真人窗分轨（`left=792/top=40`、2px A 墨框 + 右下 4px B 墨错位边、原尺寸放置不缩放、`-an` 不设 muted、与最终 V1 同步、首/中/尾三帧验收）。
- **字幕只出现一次**：只留主口播字幕，实际发现重复轨才隐藏，重建轨道后复查。
- **预览确认门**：剪完停下给预览等用户确认，确认后才导出。

完整规则见 `SKILL.md` 与 `references/`。

---

## 许可说明

- 本仓库（slbb-chatcut-ckb）为作者自有技能，保留所有权利；如需商业使用请联系作者。
- eian-riso-broll 版权归 Eian 所有，使用须遵守其官方仓库的 [Eian Personal Non-Commercial License 1.0](https://github.com/YIAN6557/eian-riso-broll/blob/main/LICENSE)。