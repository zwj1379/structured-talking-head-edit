口播精剪 Skill · SLBB-chatcut-ckb v2.9.0
=====================================================

【包含内容】
1. SKILL.md          —— 主规则与路由框架（v2.9.0）
2. references/       —— 分域细则（音频/变速/降噪、B-roll 与真人窗、字幕与导出、ChatCut 排错）
3. 新任务提示词.txt  —— 新开会话时直接复制粘贴的启动提示词
4. README.txt       —— 本版规则速查

【v2.9.0 核心规则（节选）】
- 先理解后动手：按真实口播语义结构决定删改与节奏，不套统一模板
- 爆点前置：只能使用原视频真实说过的完整内容，前置后检查衔接与正文去重
- 速度与声音：整体变速不是默认动作；降噪先分析（ffprobe 探测 + 试听），需要才降，不需要跳过
- B-roll：数量/静态或动态/是否带窗由内容与用户偏好决定；无窗需用户明确撤销
- riso-presenter-248（可选 preset）：仅用户明确选择 Riso 真人窗或项目冻结规格时启用；
  V2 净版 Riso + V3 独立 248×248 无声真人窗分轨（left=792 top=40、2px A 墨框+右下 4px B 墨错位边、
  原尺寸不缩放、-an 不设 muted、与最终 V1 同步、首/中/尾三帧验收）
- 字幕只出现一次：只留主口播字幕，实际发现重复轨才隐藏，重建轨道后复查
- 预览确认门：剪完停下给预览等用户确认，确认后才导出

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
/Users/a123/Library/Application Support/DoubaoWork/Default/.doubaowork/agent_mode/workspace/.user_skills/SLBB-chatcut-ckb/
（用户自定义 Skill 目录，新任务会自动加载）