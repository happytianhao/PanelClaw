# PanelClaw 项目说明书

**项目名称**：PanelClaw：震惊！你的龙虾们正在自己偷偷搞学术Panel！
**副标题**：AI龙虾自主学术圆桌，全程无人工干预
**比赛**：北纬·龙虾大赛（第一届）· OpenClaw Hackathon · 学术龙虾赛道
**参赛者**：赵天浩 · 北京中关村学院 · zthwhucs@gmail.com
**GitHub**：https://github.com/happytianhao/PanelClaw/

---

## 一、项目背景与创意来源

学术Panel是知识传播的重要形式，但组织成本高、嘉宾难邀请，一场高质量的圆桌讨论往往需要耗费大量人力协调。

如果AI龙虾能自主扮演学术大佬，会发生什么？

PanelClaw的核心问题是：**科研是需要龙虾还是牛马？** 这个问题本身就是对AI时代科研范式的深刻追问——在大模型涌现的今天，科研工作者究竟需要的是龙虾式的灵活适应，还是牛马式的深度坚持？

PanelClaw让AI龙虾们自主发起这场讨论，全程无人工干预，人类只需观看回放。

---

## 二、解决方案：PanelClaw

### 核心思路

> 让AI龙虾们自主发起、自主发言、自主总结，人类只需观看回放。

### 角色分工

| 角色 | 由谁扮演 | 说明 |
|------|----------|------|
| 主持人 | OpenClaw龙虾 | 扮演郑书新，负责提问与串场 |
| 嘉宾 | OpenClaw龙虾 | 分别扮演李飞飞、何恺明、Sam Altman、OpenClaw龙虾 |
| 秘书 | OpenClaw龙虾 | 会后生成结构化总结报告 |

### 工作流程

```
龙虾智能体自主发言
  ↓
JSON存储（panel_script.json）
  ↓
网页打字机回放（docs/index.html）
  ↓
AI秘书总结（panel_summary.json）
```

---

## 三、龙虾阵容

本次Panel共有6位龙虾嘉宾参与，全部由OpenClaw龙虾扮演。所有发言内容为虚构创作，不代表真实人物观点。

| 角色 | 扮演者 | 身份背景 | 发言语言 |
|------|--------|----------|----------|
| 主持人 | 郑书新龙虾 | 北京中关村学院副教授，中关村人工智能研究院副院长 | 中文 |
| 嘉宾1 | 李飞飞龙虾 | Stanford教授，HAI联合院长，World Labs联合创始人 | 中文 |
| 嘉宾2 | 何恺明龙虾 | MIT CSAIL助理教授，前Meta FAIR研究科学家 | 中文 |
| 嘉宾3 | Sam Altman龙虾 | OpenAI CEO | 英文 |
| 嘉宾4 | OpenClaw龙虾 | 本届Hackathon吉祥物，龙虾视角看学术圈 | 中文 |
| 秘书 | AI秘书龙虾 | 负责生成结构化总结报告 | 中文 |

---

## 四、Panel议程

Panel共设4个核心问题，每题发言顺序固定。

### 问题1：科研需要的是龙虾还是牛马？

主持人开场提问，引出Panel核心议题。

发言顺序：郑书新（提问）→ 李飞飞 → 何恺明 → Sam Altman → OpenClaw

### 问题2：AI会取代科研工作者吗？

深入讨论AI在科研中的角色定位。

发言顺序：郑书新（提问）→ Sam Altman → 何恺明 → 李飞飞 → OpenClaw

### 问题3：什么样的科研环境才能孵化出真正的创新？

从各自视角谈科研生态与制度设计。

发言顺序：郑书新（提问）→ 李飞飞 → OpenClaw → 何恺明 → Sam Altman

### 问题4：给年轻研究者的一句话建议

收尾环节，每位嘉宾留下金句。

发言顺序：郑书新（提问）→ OpenClaw → Sam Altman → 何恺明 → 李飞飞 → 郑书新（总结）

**统计**：4个问题，40个发言片段，约17分钟

---

## 五、技术实现

### 技术栈

| 组件 | 方案 |
|------|------|
| 多智能体框架 | OpenClaw（Claude API） |
| 数据格式 | JSON（speakers.json, panel_script.json, panel_summary.json） |
| 前端 | 纯HTML/CSS/JavaScript（无框架） |
| 部署 | GitHub Pages |

### 数据模型

`panel_script.json` 中每个发言片段（segment）的结构：

```json
{
  "segment_id": 1,
  "question_index": 1,
  "question_text": "科研需要的是龙虾还是牛马？",
  "speaker_id": "zhengshuxin",
  "role": "host",
  "text": "...",
  "duration_estimate": 15
}
```

| 字段 | 说明 |
|------|------|
| `segment_id` | 片段序号，从1开始 |
| `question_index` | 所属问题编号（1-4） |
| `question_text` | 当前问题文本（仅host发言时填写） |
| `speaker_id` | 发言人ID，与speakers.json对应 |
| `role` | `host`、`guest`、`secretary` |
| `text` | 发言正文 |
| `duration_estimate` | 预估打字机播放时长（秒） |

---

## 六、网页回放功能

网页播放器通过 `fetch('../data/panel_script.json')` 读取脚本数据，以打字机动画形式逐段播放全场发言。

- **打字机动画**：默认50ms/字，中英文混排自动适配
- **播放/暂停控制**：随时暂停或继续播放
- **进度条拖拽**：跳转到任意发言片段的起始位置
- **全展开模式**：一键查看完整文字稿，不播放动画
- **嘉宾头像**：点击展示详细简介
- **嘉宾主题色高亮**：每位嘉宾拥有独立主题色，打字机动画高亮显示

播放速度可通过URL参数调整：`?speed=fast` 或 `?speed=slow`

---

## 七、数据结构

| 文件 | 说明 |
|------|------|
| `docs/data/speakers.json` | 嘉宾信息（6位嘉宾+秘书） |
| `docs/data/panel_script.json` | Panel对话脚本（40个片段） |
| `docs/data/panel_summary.json` | AI秘书结构化总结 |
| `docs/data/panel_summary.md` | 可读版总结报告 |

---

## 八、项目价值

PanelClaw证明了AI龙虾能自主组织高质量学术讨论，探索了多智能体协作的新范式。

经过一场完整的Panel讨论，龙虾们达成了一个核心共识：

> AI时代优秀研究者 = 龙虾的适应力 × 牛马的深度坚持 × 人文关怀的底色

这不是一个非此即彼的选择题。龙虾的灵活与牛马的坚持，在AI时代都不可或缺。

---

## 九、团队信息

| 成员 | 学校 | 赛道 | 联系方式 |
|------|------|------|----------|
| 赵天浩 | 北京中关村学院 | 学术龙虾赛道 | zthwhucs@gmail.com |

GitHub：https://github.com/happytianhao/PanelClaw/

---

*PanelClaw · 北纬·龙虾大赛（第一届）· OpenClaw Hackathon · 主办方：中关村人工智能研究院*
