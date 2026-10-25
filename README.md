# structured-talking-head-edit

**2～3 分钟结构化口播精剪 Skill**（配合 ChatCut Desktop 使用）

当前版本：**v2.8.0** · 打包日期：2026-10-25

本仓库是该技能的主发布仓库。适合为单人竖版口播做「爆点前置 + 语音精剪 + 噪音分析（需要才降噪）+ B-roll 分轨（V2 净版 + V3 独立小窗）+ 简体字幕 + 成片检查」的完整剪辑。

---

## 仓库内容

| 路径 | 说明 |
| --- | --- |
| `SKILL.md` | 主规则文件（v2.8.0） |
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

安装后在对应宿主中与 structured-talking-head-edit 并排使用即可。

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

## v2.8.0 核心硬规则（节选）

- **降噪先分析**：用 ffprobe 探测说话间隙底噪（顶在 -20dB 左右或更高、或没有真静音段 → 需要降噪；已在 -35dB 或更低 → 跳过）；需要时对 A1 音轨启用 denoise（strength=1），导出后验证底噪下降、人声清晰；不需要就跳过，不误加处理器。
- **分轨模式（V2 净版 B-roll + V3 独立小窗）**：小窗和 B-roll 分开放在不同轨道；V2 放净版全画幅 B-roll（1080×1920，`-an` 无音轨），V3 放独立 248×248 带框小窗视频（素材本身含 2px 深蓝框 + 右下 4px 荧光粉错位边，`-an -r 30`），按原始尺寸放置 `left=792、top=40`，不缩放、不加蒙版；与主轨精确同步、首/中/尾三帧验收。
- **字幕只出现一次**：只保留 V1 主轨字幕；每次 enable 字幕或重建小窗后，必须用 `read_captions` 复查所有字幕轨，把 V2/V3 轨字幕 `visible=false`（重建小窗会重置 V3 字幕为可见，必须复查）。
- **开头前 2 秒强制保留 A-roll**：第一条 B-roll 入点不得早于 00:02.000（30fps = 第 60 帧）。
- **BGM**：用户音乐原始音量 0dB，裁到与主轨等长、结尾淡出 2 秒。
- **语速**：默认 FFMPEG 前置整体 1.1x，不在时间线用 `playbackRate`。
- **预览确认门**：剪完必须停下给预览等用户确认，确认后才导出。

完整规则见 `SKILL.md`。

---

## 许可说明

- 本仓库（structured-talking-head-edit）为作者自有技能，保留所有权利；如需商业使用请联系作者。
- eian-riso-broll 版权归 Eian 所有，使用须遵守其官方仓库的 [Eian Personal Non-Commercial License 1.0](https://github.com/YIAN6557/eian-riso-broll/blob/main/LICENSE)。
