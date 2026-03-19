# PanelClaw Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** 构建 PanelClaw——一个由 OpenClaw 驱动的学术圆桌论坛全自动模拟系统，内容预生成，通过 GitHub Pages 网页动态播放。

**Architecture:** 预生成内容存为 JSON，GitHub Pages 静态网页读取 JSON 做打字机动画播放，支持进度控制和全展开模式。OpenClaw 负责生成对话脚本，网页纯前端实现。

**Tech Stack:** HTML/CSS/JS（纯前端）、JSON 数据文件、OpenClaw（内容生成）、GitHub Pages（部署）

---

### Task 1: 项目基础结构

**Files:**
- Create: `CLAUDE.md`
- Create: `README.md`
- Create: `.gitignore`
- Create: `LICENSE`

**Step 1: 创建 CLAUDE.md（AI开发指导文档）**

内容见下方，包含项目概述、嘉宾阵容、数据结构、OpenClaw工作流、文件结构、开发约定。

**Step 2: 创建 README.md**

项目介绍，包含：项目简介、核心功能、快速了解、演示数据、技术栈、项目结构、项目资源、参赛信息。

**Step 3: 创建 .gitignore**

```
materials/
.DS_Store
node_modules/
*.log
```

**Step 4: 创建 LICENSE（MIT）**

**Step 5: Commit**

```bash
git add CLAUDE.md README.md .gitignore LICENSE
git commit -m "docs: 初始化项目基础文档"
```

---

### Task 2: 数据文件 — speakers.json

**Files:**
- Create: `data/speakers.json`

**Step 1: 创建 data/speakers.json**

包含所有嘉宾信息：

```json
[
  {
    "id": "host",
    "name": "郑书新",
    "name_en": "Shuxin Zheng",
    "role": "host",
    "title": "副教授 · 大模型方向负责人",
    "affiliation": "北京中关村学院 / 中关村人工智能研究院",
    "avatar": "assets/avatars/zhengshuxin.jpg",
    "bio": "微软亚研院-中科大联合培养博士，前微软研究院首席研究员。现任中关村人工智能研究院副院长，北京中关村学院副教授。研究方向：通用AI、生成式AI、科学智能。Science封面文章，Google Scholar引用超6000次，多项AI世界冠军。",
    "language": "zh"
  },
  {
    "id": "feifei",
    "name": "李飞飞",
    "name_en": "Fei-Fei Li",
    "role": "guest",
    "order": 1,
    "title": "教授 · HAI联合院长",
    "affiliation": "Stanford University / World Labs",
    "avatar": "assets/avatars/feifei.jpg",
    "bio": "Stanford计算机科学教授，HAI（以人为本AI研究院）联合院长，World Labs联合创始人。ImageNet创始人，推动深度学习革命的关键人物。著有《我看见的世界》，倡导AI多样性与包容性。",
    "language": "zh"
  },
  {
    "id": "kaiming",
    "name": "何恺明",
    "name_en": "Kaiming He",
    "role": "guest",
    "order": 2,
    "title": "助理教授",
    "affiliation": "MIT CSAIL / 前Meta FAIR",
    "avatar": "assets/avatars/kaiming.jpg",
    "bio": "MIT CSAIL助理教授，前Meta FAIR研究科学家。ResNet、Mask R-CNN、MAE等里程碑论文作者，Google Scholar引用超40万次，深度学习领域最具影响力研究者之一。",
    "language": "zh"
  },
  {
    "id": "sam",
    "name": "Sam Altman",
    "name_en": "Sam Altman",
    "role": "guest",
    "order": 3,
    "title": "CEO",
    "affiliation": "OpenAI",
    "avatar": "assets/avatars/sam.jpg",
    "bio": "OpenAI CEO，领导GPT-4、ChatGPT、o系列模型研发。前Y Combinator总裁。坚定的AGI推进者，认为AI将压缩科学进步的时间线。",
    "language": "en"
  },
  {
    "id": "lobster",
    "name": "OpenClaw龙虾",
    "name_en": "OpenClaw Lobster",
    "role": "guest",
    "order": 4,
    "title": "首席研究员",
    "affiliation": "龙虾研究院",
    "avatar": "assets/avatars/lobster.jpg",
    "bio": "龙虾研究院首席研究员，世界上第一只能参加学术panel的AI龙虾。专长：AI Agent自主科研、龙虾计算理论、多智能体协作。不需要睡觉，科研效率是人类的24倍。",
    "language": "zh"
  },
  {
    "id": "secretary",
    "name": "Panel秘书",
    "name_en": "Panel Secretary",
    "role": "secretary",
    "title": "AI Panel秘书",
    "affiliation": "PanelClaw",
    "avatar": "assets/avatars/secretary.jpg",
    "bio": "",
    "language": "zh"
  }
]
```

**Step 2: Commit**

```bash
git add data/speakers.json
git commit -m "data: 添加嘉宾信息数据"
```

---

### Task 3: 数据文件 — panel_script.json（OpenClaw生成）

**Files:**
- Create: `data/panel_script.json`

**Step 1: 准备 OpenClaw 生成 Prompt**

用以下 Prompt 让 OpenClaw 生成完整对话脚本：

```
你是一个学术圆桌论坛的内容生成助手。请为以下panel生成完整的对话脚本。

Panel主题：科研是需要龙虾还是牛马？

参与者：
- 主持人：郑书新（北京中关村学院副教授，AI研究者）
- 嘉宾1：李飞飞（Stanford教授，ImageNet创始人）
- 嘉宾2：何恺明（MIT教授，ResNet作者）
- 嘉宾3：Sam Altman（OpenAI CEO，全程英文发言）
- 嘉宾4：OpenClaw龙虾（AI龙虾嘉宾，幽默但有实质观点）

议程：
Q1: AI时代，科研范式正在发生什么根本性变化？（李飞飞→何恺明→Sam→龙虾）
Q2: "龙虾科研"（AI Agent自主科研）vs "牛马科研"（人工密集），你更看好哪条路？（何恺明→Sam→龙虾→李飞飞）
Q3: 给年轻研究者：现在应该怎么做科研，才不会被AI取代？（Sam→龙虾→李飞飞→何恺明）
Q4（总结）: 一句话：科研到底需要龙虾还是牛马？（全员依次）

每位嘉宾发言风格：
- 郑书新：专业、有条理，善于引导话题
- 李飞飞：温暖有力，关注人文价值
- 何恺明：简洁、技术导向，喜欢用具体例子
- Sam Altman：英文，宏观愿景，对AGI充满信心
- OpenClaw龙虾：幽默自嘲，但观点有实质内容，偶尔提到"龙虾视角"

要求：
1. 每人每次发言200-400字
2. 嘉宾之间可以互相引用或友好反驳
3. Sam全程英文
4. 龙虾嘉宾适当幽默，但不能只是段子
5. 每轮结束后，Panel秘书生成50-100字的该轮摘要
6. 输出严格的JSON格式，结构如下：

[
  {"id": 1, "speaker": "郑书新", "role": "host", "type": "opening", "round": 0, "content": "..."},
  {"id": 2, "speaker": "郑书新", "role": "host", "type": "question", "round": 1, "content": "..."},
  {"id": 3, "speaker": "李飞飞", "role": "guest", "type": "answer", "round": 1, "search_query": "AI scientific discovery paradigm shift", "content": "..."},
  ...
  {"id": N, "speaker": "Panel秘书", "role": "secretary", "type": "summary", "round": 1, "content": "..."}
]

type字段说明：opening/question/answer/summary/closing
search_query：嘉宾引用网络资料时填写搜索词，否则为null
```

**Step 2: 将生成结果保存为 data/panel_script.json**

**Step 3: Commit**

```bash
git add data/panel_script.json
git commit -m "data: 添加panel对话脚本"
```

---

### Task 4: 嘉宾头像资源

**Files:**
- Create: `docs/assets/avatars/` 目录

**Step 1: 准备头像**

为每位嘉宾准备头像图片，放入 `docs/assets/avatars/`：
- `zhengshuxin.jpg` — 郑书新
- `feifei.jpg` — 李飞飞
- `kaiming.jpg` — 何恺明
- `sam.jpg` — Sam Altman
- `lobster.jpg` — OpenClaw龙虾（可用龙虾emoji或卡通图）
- `secretary.jpg` — Panel秘书（可用机器人图标）

**Step 2: Commit**

```bash
git add docs/assets/
git commit -m "assets: 添加嘉宾头像"
```

---

### Task 5: 网页播放器 — docs/index.html

**Files:**
- Create: `docs/index.html`

**Step 1: 创建 HTML 结构**

页面结构：
```
┌─────────────────────────────────────────┐
│  PanelClaw · 科研是需要龙虾还是牛马？     │  ← 标题栏
├─────────────────────────────────────────┤
│  [郑书新] [李飞飞] [何恺明] [Sam] [龙虾] │  ← 嘉宾头像栏（发言时高亮）
├─────────────────────────────────────────┤
│                                         │
│  对话流区域（气泡形式）                   │  ← 主内容区
│                                         │
├─────────────────────────────────────────┤
│  ▶ ⏸  ════════●══════════  [全部展开]   │  ← 控制栏
└─────────────────────────────────────────┘
```

**Step 2: 实现核心 JS 逻辑**

```javascript
// 核心状态
let script = [];        // panel_script.json 数据
let speakers = [];      // speakers.json 数据
let currentIndex = 0;   // 当前播放位置
let isPlaying = false;  // 是否在播放
let typingSpeed = 30;   // 打字速度(ms/字)

// 核心函数
async function loadData() { /* 加载JSON */ }
function renderMessage(msg) { /* 渲染单条消息气泡 */ }
function typewriterEffect(el, text, callback) { /* 打字机动画 */ }
function showSearchAnimation(speaker, query) { /* 搜索动画 */ }
function highlightSpeaker(speakerId) { /* 头像高亮 */ }
function play() { /* 开始播放 */ }
function pause() { /* 暂停 */ }
function expandAll() { /* 全部展开 */ }
function seekTo(index) { /* 跳转到指定位置 */ }
```

**Step 3: 样式设计**

- 深色主题（#0f0f1a 背景）
- 每位嘉宾有专属颜色
- 气泡左右布局（主持人居中，嘉宾左右交替）
- 秘书总结用特殊卡片样式
- 搜索动画：脉冲效果

**Step 4: 进度条实现**

进度条显示当前播放位置（currentIndex / script.length），可拖拽跳转。

**Step 5: Commit**

```bash
git add docs/index.html
git commit -m "feat: 实现网页panel播放器"
```

---

### Task 6: 秘书总结报告

**Files:**
- Create: `data/reports/panel-summary.md`

**Step 1: 用 OpenClaw 生成完整总结报告**

Prompt：
```
请根据以下panel对话脚本，生成一份完整的学术圆桌论坛总结报告。

[粘贴 panel_script.json 内容]

报告格式：
# PanelClaw 论坛总结报告
## 论坛基本信息
## 各轮讨论摘要
## 嘉宾核心观点
## 主要分歧与共识
## 结论
```

**Step 2: 保存为 data/reports/panel-summary.md**

**Step 3: Commit**

```bash
git add data/reports/
git commit -m "data: 添加panel总结报告"
```

---

### Task 7: 最终检查与部署

**Step 1: 本地测试**

```bash
cd docs && python3 -m http.server 8080
# 访问 http://localhost:8080 验证网页正常
```

**Step 2: 确认 GitHub Pages 配置**

- 仓库设置 → Pages → Source: Deploy from branch → main → /docs

**Step 3: 推送到 GitHub**

```bash
git push origin main
```

**Step 4: 验证 GitHub Pages 可访问**

访问 `https://happytianhao.github.io/PanelClaw/` 确认正常。

---

## 开发顺序总结

1. Task 1: 基础文档（CLAUDE.md、README）
2. Task 2: speakers.json
3. Task 3: panel_script.json（需要OpenClaw）
4. Task 4: 头像资源
5. Task 5: 网页播放器
6. Task 6: 秘书总结报告
7. Task 7: 部署验证
