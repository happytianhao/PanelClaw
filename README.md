# PanelClaw：震惊！你的龙虾们正在自己偷偷搞学术Panel！

**AI龙虾自主学术圆桌，全程无人工干预**

🦞 **[在线演示 → happytianhao.github.io/PanelClaw](https://happytianhao.github.io/PanelClaw/)**

> 北纬·龙虾大赛（第一届）· OpenClaw Hackathon · 学术龙虾赛道
> 主办方：中关村人工智能研究院

---

## 这是什么

PanelClaw 是一个 AI 自主生成学术 Panel 讨论的展示项目。

OpenClaw 龙虾作为内容生成引擎，自主扮演多位学术大佬，围绕"科研是需要龙虾还是牛马？"这一灵魂拷问展开圆桌讨论。所有对话脚本由 AI 预生成并存为 JSON，通过 GitHub Pages 静态网页以打字机动画形式播放，全程无人工干预。

所有嘉宾发言内容均为虚构创作，不代表真实人物观点。

---

## 核心功能

- AI 自主生成完整 Panel 对话脚本（4 个问题，5 位嘉宾）
- 打字机动画逐字播放，支持播放/暂停
- 进度条可拖拽跳转到任意发言片段
- 全展开模式：一键查看完整文字稿
- AI 秘书自动生成结构化总结报告
- 纯静态部署，无需后端

---

## 快速了解

```
OpenClaw 生成脚本
      │
      ▼
panel_script.json  ←  speakers.json
      │
      ▼
docs/index.html（打字机播放器）
      │
      ▼
观众观看 Panel 直播回放
      │
      ▼
AI 秘书生成总结报告 → data/reports/
```

---

## 演示数据

| 角色 | 姓名 | 身份 |
|------|------|------|
| 主持人 | 郑书新 | 北京中关村学院副教授，中关村人工智能研究院副院长 |
| 嘉宾 1 | 李飞飞 | Stanford 教授，HAI 联合院长，World Labs 联合创始人 |
| 嘉宾 2 | 何恺明 | MIT CSAIL 助理教授，前 Meta FAIR |
| 嘉宾 3 | Sam Altman | OpenAI CEO（全程英文发言） |
| 嘉宾 4 | OpenClaw 龙虾 | AI 龙虾嘉宾（虚构角色） |
| 秘书 | AI Panel 秘书 | 负责生成总结报告 |

Panel 题目：**科研是需要龙虾还是牛马？**

---

## 技术栈

- 内容生成：OpenClaw（Claude API）
- 数据格式：JSON
- 前端：纯 HTML / CSS / JavaScript（无框架）
- 部署：GitHub Pages

---

## 项目结构

```
PanelClaw/
├── data/
│   ├── speakers.json       # 嘉宾信息
│   ├── panel_script.json   # Panel 对话脚本
│   └── reports/            # AI 秘书总结报告
└── docs/                   # GitHub Pages 静态网站
    ├── index.html          # 打字机播放器
    ├── report/             # 报告展示页
    ├── poster/             # 海报
    └── slides/             # 幻灯片
```

---

## 项目资源

- 在线演示：https://happytianhao.github.io/PanelClaw/
- GitHub 仓库：https://github.com/happytianhao/PanelClaw/
- 项目海报：`docs/poster/`
- 项目幻灯片：`docs/slides/`

---

## 参赛信息

- 比赛：北纬·龙虾大赛（第一届）· OpenClaw Hackathon
- 赛道：学术龙虾赛道
- 主办方：中关村人工智能研究院
- 参赛者：赵天浩 · 北京中关村学院 · zthwhucs@gmail.com
