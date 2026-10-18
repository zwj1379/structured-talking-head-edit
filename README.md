# structured-talking-head-edit

**2～3 分钟结构化口播精剪 Skill**（配合 ChatCut Desktop 使用）

当前版本：**v2.7.0** · 打包日期：2026-10-17

本仓库是该技能的主发布仓库（无公开 git 仓库历史，从 v2.7.0 起托管于此）。适合为单人竖版口播做「爆点前置 + 语音精剪 + B-roll 画中画 + 简体字幕 + 成片检查」的完整剪辑。

---

## 仓库内容

| 路径 | 说明 |
| --- | --- |
| `structured-talking-head-edit/SKILL.md` | 主规则文件（v2.7.0） |
| `structured-talking-head-edit/新任务提示词.txt` | 新会话启动提示词，直接复制粘贴 |
| `structured-talking-head-edit/README.txt` | 本版规则速查 |

> 原 `slbb-chatcut-oneclip` 已由本技能 + eian-riso-broll 组合取代。

---

## 配套：eian-riso-broll（Riso 信息动画，可选）

本技能可搭配 **eian-riso-broll** 生成 Riso 孔版风信息动画 B-roll（数字冲击 / 流程 / 前后对比 / 关键引述等 10 个模板，1080×1920 竖版、无音轨、可带透明通道）。

**该技能是第三方独立包，采用 Eian 个人非商业使用许可 1.0，禁止再分发、禁止公开**，因此本仓库不包含其文件，仅提供官方获取途径：

```bash
git clone https://github.com/YIAN6557/eian-riso-broll.git
```

安装后在对应宿主中与 structured-talking-head-edit 并排使用即可（两平台均可）。

---

## 安装到宿主

### 通道 A：WorkBuddy（MCP 连接器）

1. 将本仓库的 `structured-talking-head-edit/` 目录放入 `~/.workbuddy/skills/`
2. `git clone https://github.com/YIAN6557/eian-riso-broll.git ~/.workbuddy/skills/eian-riso-broll`
3. 确认 `~/.workbuddy/mcp.json` 中 ChatCut MCP 条目存在（文件名**没有前导点**）
4. 用「新任务提示词.txt」开新会话，或直接说：用 structured-talking-head-edit + eian-riso-broll 帮我精剪这条口播并配 Riso 动画

### 通道 B：豆包工作（内置 ChatCut 插件）

1. 插件商店启用 ChatCut 插件，确认 ChatCut Desktop 在后台运行
2. 把本仓库 `structured-talking-head-edit/` 目录（或整个仓库 zip）拖进对话框，AI 会解压装到 `.user_skills/structured-talking-head-edit/`
3. eian-riso-broll 同样方式从官方仓库获取安装
4. 重启豆包工作，新开会话验证

---

## v2.7.0 核心硬规则（节选）

- **开头前 2 秒强制保留 A-roll**：第一条 B-roll 入点不得早于 00:02.000（30fps = 第 60 帧）
- **每条 B-roll 必须带右上角方形真人窗**：人物内容 240×240、装饰组合 248×248，`left=792、top=40`（可见 x=792–1040 / y=40–288），2px A 墨细框 + 右下 4px B 墨错位边，直角，头肩近景，与正文 ≥16px 间距；预合成进成片、静音、与最终 V1 精确同步
- **无法合成合格真人窗时保留 A-roll 并报告缺口**，禁止隐藏真人窗或退回静态图降级
- **字幕只出现一次**：只留 V1 主轨，每次 enable/重建小窗后复查，V2/V3 轨一律隐藏
- **BGM**：用户音乐原始音量 0dB，裁到与主轨等长、结尾淡出 2 秒
- **语速**：默认 FFMPEG 前置整体 1.1x，不在时间线用 `playbackRate`
- **规避词**（品牌/同行/产品专名）：只在字幕层留白，不动音频、不改台词
- **预览确认门**：剪完必须停下给预览等用户确认，确认后才导出

完整规则见 `structured-talking-head-edit/SKILL.md`。

---

## 许可说明

- 本仓库（structured-talking-head-edit）为作者自有技能，保留所有权利；如需商业使用请联系作者。
- eian-riso-broll 版权归 Eian 所有，使用须遵守其官方仓库的 [Eian Personal Non-Commercial License 1.0](https://github.com/YIAN6557/eian-riso-broll/blob/main/LICENSE)。
