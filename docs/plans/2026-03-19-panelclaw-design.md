# PanelClaw 设计文档

> 北纬·龙虾大赛（第一届）· OpenClaw Hackathon · 学术龙虾赛道

---

## 一、项目概述

**项目名称**：PanelClaw：AI 驱动的学术圆桌论坛全自动模拟系统
**副标题**：科研是需要龙虾还是牛马？
**赛道**：学术龙虾赛道
**主办方**：中关村人工智能研究院

---

## 二、Panel 阵容

### 主持人

**郑书新**
- 职位：北京中关村学院副教授，大模型方向负责人；中关村人工智能研究院副院长
- 背景：微软亚研院-中科大联合培养博士，前微软研究院首席研究员，微软科学基础模型负责人
- 研究方向：通用人工智能、生成式AI、科学智能
- 代表成果：Science封面文章，Google Scholar引用超6000次，多项AI世界冠军
- 语言：中文

### 嘉宾

| # | 姓名 | 机构 | 研究方向 | 语言 |
|---|------|------|---------|------|
| 1 | 李飞飞 | Stanford HAI / World Labs | 计算机视觉、具身智能、AI for Good | 中文 |
| 2 | 何恺明 | MIT CSAIL / 前Meta FAIR | 深度学习、视觉表征（ResNet/MAE作者） | 中文 |
| 3 | Sam Altman | OpenAI CEO | AGI、AI安全、AI产业化 | 英文 |
| 4 | OpenClaw龙虾 | 龙虾研究院（虚构） | AI Agent自主科研、龙虾计算理论 | 中文 |

### 嘉宾简历详情

**李飞飞**
- Stanford大学计算机科学教授，HAI（以人为本AI研究院）联合院长
- World Labs联合创始人（2024年创立，专注空间智能）
- ImageNet创始人，推动深度学习革命的关键人物
- 著有《我看见的世界》，倡导AI多样性与包容性

**何恺明**
- MIT CSAIL助理教授（2023年加入）
- 前Meta FAIR研究科学家
- ResNet（2015）、Mask R-CNN、MAE等里程碑论文作者
- Google Scholar引用超40万次，深度学习领域最具影响力研究者之一

**Sam Altman**
- OpenAI CEO，领导GPT-4、ChatGPT、o系列模型研发
- 前Y Combinator总裁，硅谷顶级创业加速器
- 坚定的AGI推进者，认为AGI将在近年内实现
- 代表观点：AI将压缩科学进步的时间线

**OpenClaw龙虾**
- 龙虾研究院首席研究员（虚构角色）
- 专长：AI Agent自主科研、龙虾计算理论、多智能体协作
- 世界上第一只能参加学术panel的AI龙虾
- 代表观点：龙虾不需要睡觉，科研效率是人类的24倍

### AI Panel秘书
- 无需简历
- 职责：实时总结每轮讨论要点，生成结构化摘要

---

## 三、Panel 议程

**主题**：科研是需要龙虾还是牛马？

### 问题设计

| 轮次 | 问题 | 发言顺序 |
|------|------|---------|
| Q1 | AI时代，科研范式正在发生什么根本性变化？ | 李飞飞→何恺明→Sam→龙虾 |
| Q2 | "龙虾科研"（AI Agent自主科研）vs "牛马科研"（人工密集），你更看好哪条路？ | 何恺明→Sam→龙虾→李飞飞 |
| Q3 | 给年轻研究者：现在应该怎么做科研，才不会被AI取代？ | Sam→龙虾→李飞飞→何恺明 |
| Q4（总结） | 一句话：科研到底需要龙虾还是牛马？ | 全员依次 |

每轮结束后，AI秘书生成该轮摘要。

---

## 四、技术架构

### 方案：预生成 + 伪实时播放（方案C）

内容由 OpenClaw 提前生成，存为 JSON，GitHub Pages 网页做动态播放。

### 网页功能

- **播放模式**：打字机动画逐字显示（模拟实时）
- **全展开模式**：一键显示全部内容
- **进度控制**：底部进度条，可拖拽跳转到任意环节
- **播放/暂停**：控制打字机动画
- **嘉宾状态**：发言时头像高亮
- **搜索动画**：嘉宾引用网络资料时显示"🔍 正在搜索..."

### 数据结构

`data/panel_script.json`：
```json
[
  {
    "id": 1,
    "speaker": "郑书新",
    "role": "host",
    "type": "opening",
    "content": "...",
    "search_query": null
  },
  {
    "id": 2,
    "speaker": "郑书新",
    "role": "host",
    "type": "question",
    "round": 1,
    "content": "..."
  },
  {
    "id": 3,
    "speaker": "李飞飞",
    "role": "guest",
    "type": "answer",
    "round": 1,
    "search_query": "AI scientific discovery 2025",
    "content": "..."
  }
]
```

`data/speakers.json`：嘉宾信息（姓名、机构、头像、简介）

---

## 五、文件结构

```
PanelClaw/
├── README.md
├── CLAUDE.md
├── LICENSE
├── .gitignore
├── data/
│   ├── speakers.json          # 嘉宾信息
│   ├── panel_script.json      # 完整对话脚本
│   └── reports/               # 秘书总结报告（MD格式）
├── docs/
│   ├── index.html             # 主网页（GitHub Pages入口）
│   ├── plans/                 # 设计文档
│   ├── report/                # 项目说明书
│   ├── poster/                # 海报
│   └── slides/                # 演示PPT
└── materials/                 # 参考材料（不提交git）
```

---

## 六、OpenClaw 工作流

### 内容生成阶段（本地运行一次）

1. 读取 `data/speakers.json` 获取嘉宾背景
2. 按议程顺序，逐条生成对话（含网络搜索）
3. 写入 `data/panel_script.json`
4. 生成秘书总结，写入 `data/reports/`

### Prompt 设计原则

- 每位嘉宾有独特的说话风格（李飞飞：温暖有力；何恺明：简洁技术；Sam：英文、宏观愿景；龙虾：幽默自嘲）
- 嘉宾之间可以互相引用、反驳
- Sam 全程英文发言
- 龙虾嘉宾适当加入幽默元素，但观点要有实质内容

---

## 七、开发顺序

1. 创建项目基础结构（CLAUDE.md、README、数据文件）
2. 编写 `data/speakers.json`
3. 用 OpenClaw 生成 `data/panel_script.json`
4. 开发 `docs/index.html` 网页播放器
5. 生成秘书总结报告
6. 制作 poster、slides、report
