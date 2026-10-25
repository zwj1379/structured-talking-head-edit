口播精剪 Skill · structured-talking-head-edit v2.8.0
=====================================================

【包含内容】
1. SKILL.md          —— structured-talking-head-edit v2.8.0（规则已写死）
2. 新任务提示词.txt  —— 新开会话时直接复制粘贴的启动提示词

【v2.8.0 写死的规则（不可违反）】
- 降噪先分析：ffprobe 探测说话间隙底噪（顶在 -20dB 左右或更高、或没有真静音段 → 需要降噪；
  已在 -35dB 或更低 → 跳过）；需要时对 A1 音轨启用 denoise（strength=1），导出后验证底噪下降、
  人声清晰；不需要就跳过，不误加处理器
- 分轨模式（V2 净版 B-roll + V3 独立小窗）：小窗和 B-roll 分开放在不同轨道；
  V2 放净版全画幅 B-roll（1080×1920，-an 无音轨），V3 放独立 248×248 带框小窗视频
  （素材本身含 2px 深蓝框 + 右下 4px 荧光粉错位边，-an -r 30），按原始尺寸放置 left=792、top=40，
  不缩放、不加蒙版；与主轨精确同步、首/中/尾三帧验收
- 字幕只出现一次：只保留 V1 主轨字幕；每次 enable/重建小窗后必须复查，V2/V3 轨字幕一律隐藏
- 开头前 2 秒强制保留 A-roll：第一条 B-roll 入点不得早于 00:02.000（30fps 即第 60 帧）
- B-roll：动态视频素材，约 4 分钟成片至少 5 段，全屏 cover、立即静音
- BGM：用户提供的音乐原始音量 0dB（ChatCut 默认压到 -18dB，需显式设回 0dB），
  裁到与主轨等长、结尾淡出 2 秒
- 语速：默认 FFMPEG 前置整体 1.1x（视频+音频同时加速），不在时间线用 playbackRate

【使用方式】
1. 打开 ChatCut Desktop（确认连接正常）
2. 新开一个豆包/WorkBuddy 会话（当前会话连不上 ChatCut 时，新会话才能重新加载连接）
3. 把「新任务提示词.txt」全文粘贴到新会话第一条消息
4. 确认后由 AI 按 Skill 完整执行，剪完预览确认再导出

【Riso 信息动画（可选配套）】
本技能可选配 eian-riso-broll（Riso 孔版风信息动画 B-roll）一起使用：
- 该技能为第三方独立包，采用 Eian 个人非商业许可，禁止再分发；
- 请从官方仓库获取：git clone https://github.com/YIAN6557/eian-riso-broll.git
  详细安装见仓库根 README.md。

【Skill 安装位置（本机示例）】
/Users/a123/Library/Application Support/DoubaoWork/Default/.doubaowork/agent_mode/workspace/.user_skills/structured-talking-head-edit/
（用户自定义 Skill 目录，新任务会自动加载）
