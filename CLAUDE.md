# CLAUDE.md — PanelClaw 项目工作手册

本文件是 AI 助手（Claude 等）参与 PanelClaw 项目开发时的核心参考文档。
每次开始工作前请先完整阅读本文件。

---

## 项目概述

- 项目名称：PanelClaw：震惊！你的龙虾们正在自己偷偷搞学术Panel！
- 副标题：AI龙虾自主学术圆桌，全程无人工干预
- Panel题目：Panel Discussion - 科研是需要龙虾还是牛马？
- 赛道：学术龙虾赛道
- 比赛：北纬·龙虾大赛（第一届）· OpenClaw Hackathon
- 主办方：中关村人工智能研究院
- GitHub 仓库：https://github.com/happytianhao/PanelClaw/
- 参赛者：赵天浩 · 北京中关村学院 · zthwhucs@gmail.com

---

## 嘉宾阵容

### 主持人

**郑书新**
- 职位：北京中关村学院副教授，中关村人工智能研究院副院长
- 角色：Panel 主持人，负责提问与串场
- 发言风格：学术严谨，提问犀利，偶尔幽默

### 嘉宾 1：李飞飞

- 职位：Stanford 大学教授，HAI（以人为本人工智能研究所）联合院长，World Labs 联合创始人
- 研究方向：计算机视觉、AI for Science、具身智能
- 发言风格：宏观视野，强调人文关怀与 AI 伦理，中文发言
- speaker_id: `lifeifei`

### 嘉宾 2：何恺明

- 职位：MIT CSAIL 助理教授，前 Meta FAIR 研究科学家
- 研究方向：深度学习、ResNet、MAE、视觉基础模型
- 发言风格：技术深度，直接，喜欢从工程角度切入，中文发言
- speaker_id: `hekaiming`

### 嘉宾 3：Sam Altman

- 职位：OpenAI CEO
- 研究方向：AGI 路线图、AI 产品化、AI 安全
- 发言风格：全程英文发言，乐观，善于讲故事，偶尔引用数据
- speaker_id: `samaltman`

### 嘉宾 4：OpenClaw 龙虾

- 身份：AI 龙虾嘉宾（虚构角色），本次 Hackathon 的吉祥物
- 特点：用龙虾视角看待学术圈，发言充满隐喻和幽默，偶尔夹杂"咔咔咔"
- 发言风格：中文，活泼，反差萌，金句频出
- speaker_id: `openclaw`

### 秘书

- 身份：AI Panel 秘书（无需简历）
- 职责：会后生成结构化总结报告，输出到 `docs/data/panel_summary.json` 和 `docs/data/panel_summary.md`
- speaker_id: `secretary`

---

## Panel 议程

Panel 共设 4 个核心问题，每题发言顺序固定。

### 问题 1：科研需要的是龙虾还是牛马？

> 主持人开场提问，引出 Panel 核心议题。

发言顺序：郑书新（提问）→ 李飞飞 → 何恺明 → Sam Altman → OpenClaw龙虾

### 问题 2：AI 会取代科研工作者吗？

> 深入讨论 AI 在科研中的角色定位。

发言顺序：郑书新（提问）→ Sam Altman → 何恺明 → 李飞飞 → OpenClaw龙虾

### 问题 3：什么样的科研环境才能孵化出真正的创新？

> 从各自视角谈科研生态与制度设计。

发言顺序：郑书新（提问）→ 李飞飞 → OpenClaw龙虾 → 何恺明 → Sam Altman

### 问题 4：给年轻研究者的一句话建议

> 收尾环节，每位嘉宾留下金句。

发言顺序：郑书新（提问）→ OpenClaw龙虾 → Sam Altman → 何恺明 → 李飞飞 → 郑书新（总结）

---

## 数据结构

### `docs/data/speakers.json`

存储所有嘉宾的基本信息，供前端渲染头像、姓名、标签。

```json
[
  {
    "speaker_id": "lifeifei",
    "name": "李飞飞",
    "name_en": "Fei-Fei Li",
    "title": "Stanford 教授 / HAI 联合院长",
    "affiliation": "Stanford University",
    "avatar": "assets/avatars/lifeifei.jpg",
    "language": "zh",
    "color": "#4A90D9"
  }
]
```

字段说明：

| 字段 | 类型 | 说明 |
|------|------|------|
| speaker_id | string | 唯一标识符，与 panel_script.json 对应 |
| name | string | 中文姓名 |
| name_en | string | 英文姓名 |
| title | string | 职位简介（显示在头像下方） |
| affiliation | string | 所属机构 |
| avatar | string | 头像图片路径（相对于 docs/） |
| language | string | 发言语言，`zh` 或 `en` |
| color | string | 该嘉宾的主题色（用于打字机动画高亮） |

### `docs/data/panel_script.json`

存储完整的 Panel 对话脚本，按发言顺序排列。

```json
{
  "panel_title": "Panel Discussion - 科研是需要龙虾还是牛马？",
  "generated_at": "2026-03-19T00:00:00Z",
  "segments": [
    {
      "segment_id": 1,
      "question_index": 1,
      "question_text": "科研需要的是龙虾还是牛马？",
      "speaker_id": "zhengshuxin",
      "role": "host",
      "text": "...",
      "duration_estimate": 15
    }
  ]
}
```

字段说明：

| 字段 | 类型 | 说明 |
|------|------|------|
| panel_title | string | Panel 标题 |
| generated_at | string | ISO 8601 时间戳，脚本生成时间 |
| segments | array | 所有发言片段，按顺序排列 |
| segment_id | number | 片段序号，从 1 开始 |
| question_index | number | 所属问题编号（1-4） |
| question_text | string | 当前问题文本（仅 host 发言时填写） |
| speaker_id | string | 发言人 ID，与 speakers.json 对应 |
| role | string | `host`、`guest`、`secretary` |
| text | string | 发言正文 |
| duration_estimate | number | 预估打字机播放时长（秒） |

### `docs/data/panel_summary.json`

存储 AI 秘书生成的总结报告，一个 Panel 对应一个文件。

```json
{
  "generated_at": "2026-03-19T12:00:00Z",
  "panel_title": "Panel Discussion - 科研是需要龙虾还是牛马？",
  "summary": "...",
  "key_points": [
    {
      "question_index": 1,
      "question_text": "...",
      "highlights": ["...", "..."]
    }
  ],
  "quotes": [
    {
      "speaker_id": "openclaw",
      "text": "..."
    }
  ]
}
```

---

## OpenClaw 工作流

### 内容生成阶段

1. 生成 `docs/data/speakers.json`：填写所有嘉宾信息
2. 生成 `docs/data/panel_script.json`：按议程顺序逐段生成对话脚本
3. 生成 `docs/data/panel_summary.json`：由 AI 秘书角色总结全场内容
4. 生成 `docs/data/panel_summary.md`：将 panel_summary.json 转为可读的 Markdown 总结文档
5. 验证 JSON 格式，确保所有 speaker_id 引用一致

### Prompt 设计原则

- 每位嘉宾的发言必须符合其真实学术背景和公开立场
- Sam Altman 全程英文，其余嘉宾中文
- OpenClaw 龙虾发言需包含至少一个龙虾隐喻或"咔咔咔"
- 每段发言控制在 100-200 字（中文）或 80-150 词（英文）
- 避免政治敏感内容，聚焦学术与技术讨论
- 嘉宾之间可以有礼貌的观点碰撞，但不得人身攻击
- 所有发言内容为虚构创作，不代表真实人物观点

---

## 文件结构

```
PanelClaw/
├── README.md               # 项目介绍，面向评委
├── CLAUDE.md               # AI 助手工作手册（本文件）
├── LICENSE                 # MIT License
├── .gitignore
└── docs/                   # GitHub Pages 静态网站
    ├── index.html          # 主页面（打字机播放器）
    ├── data/
    │   ├── speakers.json       # 嘉宾信息
    │   ├── panel_script.json   # Panel 对话脚本
    │   ├── panel_summary.json  # AI 秘书结构化总结
    │   └── panel_summary.md    # 可读版总结报告
    ├── assets/
    │   └── avatars/            # 嘉宾头像
    ├── plans/              # 项目规划文档
    ├── report/             # 报告展示页
    ├── poster/             # 海报文件
    └── slides/             # 幻灯片文件
```

不要创建 `materials/` 目录，该目录已存在且在 `.gitignore` 中（存放本地素材）。

---

## 待完成清单

- [ ] 创建 `docs/data/speakers.json`（6 位嘉宾 + 秘书）
- [ ] 生成 `docs/data/panel_script.json`（4 个问题，完整对话）
- [ ] 生成 `docs/data/panel_summary.json`（AI 秘书结构化总结）
- [ ] 生成 `docs/data/panel_summary.md`（可读版总结报告）
- [ ] 创建 `docs/index.html`（打字机播放器主页面）
- [ ] 添加嘉宾头像资源到 `docs/assets/avatars/`
- [ ] 实现进度条拖拽跳转功能
- [ ] 实现全展开模式
- [ ] 实现播放/暂停控制
- [ ] 部署到 GitHub Pages

---

## 开发约定

- 所有文档用中文写，代码和字段名用英文
- JSON 文件使用 2 空格缩进
- HTML/CSS/JS 不引入外部框架，保持纯前端
- 图片资源统一放在 `docs/assets/` 下
- 提交信息格式：`type: 描述`，type 可选 `feat`、`fix`、`docs`、`data`、`style`
- 不要提交 `materials/` 目录下的任何内容

---

## AI 助手工作指引

### 跨文档一致性原则

- `speaker_id` 必须在 `speakers.json`、`panel_script.json`、`panel_summary.json` 中保持完全一致
- 嘉宾姓名、职位描述在所有文件中保持统一，以本文件为准
- Panel 议程顺序以本文件"Panel 议程"章节为准，生成脚本时严格遵守

### 每次工作前

1. 阅读本文件（CLAUDE.md）全文
2. 检查已有数据文件，避免重复生成或覆盖已有内容
3. 确认当前任务属于哪个阶段（内容生成 / 前端开发 / 调试）

### 生成脚本时

- 先生成 `speakers.json`，再生成 `panel_script.json`，顺序不可颠倒
- 每个 segment 生成后立即验证 speaker_id 是否存在于 speakers.json
- `panel_summary.json` 生成必须在脚本生成完成后进行

### 前端开发时

- `docs/index.html` 通过 `fetch('data/panel_script.json')` 读取数据
- 打字机动画速度：默认 50ms/字，可通过 URL 参数 `?speed=fast/slow` 调整
- 进度控制基于 segment_id，拖拽时跳转到对应 segment 的起始位置
- 全展开模式：一次性渲染所有 text 字段，不播放动画

### 注意事项

- 所有嘉宾发言内容为虚构创作，README 和页面中需注明
- Sam Altman 发言为英文，前端需处理中英文混排的打字机速度差异
- OpenClaw 龙虾是虚构角色，发言风格可以夸张，但其他嘉宾发言需保持专业
