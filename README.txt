口播精剪 Skill · structured-talking-head-edit v2.7.0
=====================================================

【包含内容】
1. SKILL.md          —— structured-talking-head-edit v2.7.0（规则已写死）
2. 新任务提示词.txt  —— 新开会话时直接复制粘贴的启动提示词

【v2.7.0 写死的规则（不可违反）】
- 开头前 2 秒强制保留 A-roll：若计划开头用 B-roll/Riso，成片 00:00.000–00:02.000
  必须连续真人画面，第一条 B-roll 入点不得早于 00:02.000（30fps 即第 60 帧）
- 每条 B-roll 都必须带右上角方形真人窗：人物内容 240×240、完整装饰组合 248×248，
  left=792、top=40（可见 x=792–1040 / y=40–288，顶、右侧各留 40px 安全边距）；
  2px A 墨细框 + 右下 4px B 墨错位边，直角；头肩近景，不切五官；
  与正文至少 16px 间距；真人窗与 B-roll 都静音，预合成进成片、与最终 V1 精确同步
- 无法给某段 B-roll 合成合格真人窗时：保留 A-roll 主画面并报告缺口，
  不得交付无窗 B-roll，禁止隐藏真人窗或退回静态图降级
- 字幕只出现一次：只保留 V1 主轨字幕，每次 enable/重建小窗后必须复查，
  V2/V3 轨字幕一律隐藏
- B-roll：动态视频素材，按主轨时长选 1～3 段（4 分钟至少 5 段），全屏 cover、立即静音
- BGM：用户提供的音乐原始音量 0dB（ChatCut 默认压到 -18dB，需显式设回 0dB），
  裁到与主轨等长、结尾淡出 2 秒
- 语速：默认 FFMPEG 前置整体 1.1x（视频+音频同时加速），不在时间线用 playbackRate
- 规避词（品牌/同行/产品专名）：只在字幕层留白，不动音频、不改台词、不写替代说法

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
