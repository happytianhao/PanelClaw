# PanelClaw：震惊！你的龙虾们正在自己偷偷搞学术Panel！

**AI龙虾自主学术圆桌，全程无人工干预**

🦞 **[在线演示 → happytianhao.github.io/PanelClaw](https://happytianhao.github.io/PanelClaw/)**

> 北纬·龙虾大赛（第一届）· OpenClaw Hackathon · 学术龙虾赛道
> 主办方：中关村人工智能研究院

---

## 这是什么

PanelClaw 是一场由 AI 龙虾自主发起的学术圆桌 Panel。

OpenClaw 龙虾们自发组织，各自扮演学术大佬角色，围绕"科研是需要龙虾还是牛马？"展开激烈讨论——主持人是龙虾，嘉宾是龙虾，连会后写总结的秘书也是龙虾。每只龙虾作为独立智能体，自主发言、相互回应，全程无人工干预。

网页端完整还原了这场 Panel 的全过程，支持逐字回放，让你身临其境感受龙虾们的学术碰撞。

所有嘉宾发言内容均为虚构创作，不代表真实人物观点。

---

## 核心功能

- 多智能体自主 Panel：每只龙虾独立扮演角色，自主发起对话
- 打字机动画逐字回放，支持播放/暂停
- 进度条可拖拽跳转到任意发言片段
- 全展开模式：一键查看完整文字稿
- AI 秘书龙虾自动生成结构化总结报告
- 纯静态部署，无需后端

---

## Panel 回放

```
各龙虾智能体自主发言
      │
      ▼
panel_script.json  ←  speakers.json
      │
      ▼
docs/index.html（打字机回放播放器）
      │
      ▼
观众观看 Panel 全程回放
      │
      ▼
AI 秘书龙虾生成总结报告 → docs/data/reports/
```

---

## 龙虾阵容

| 角色 | 扮演者（龙虾） | 身份 |
|------|------|------|
| 主持人 | 郑书新龙虾 | 北京中关村学院副教授，中关村人工智能研究院副院长 |
| 嘉宾 1 | 李飞飞龙虾 | Stanford 教授，HAI 联合院长，World Labs 联合创始人 |
| 嘉宾 2 | 何恺明龙虾 | MIT CSAIL 助理教授，前 Meta FAIR |
| 嘉宾 3 | Sam Altman 龙虾 | OpenAI CEO（全程英文发言） |
| 嘉宾 4 | OpenClaw 龙虾 | 本届 Hackathon 吉祥物，龙虾视角看学术圈 |
| 秘书 | AI 秘书龙虾 | 负责生成总结报告 |

Panel 题目：**科研是需要龙虾还是牛马？**

---

## 技术栈

- 多智能体框架：OpenClaw（Claude API）
- 数据格式：JSON
- 前端：纯 HTML / CSS / JavaScript（无框架）
- 部署：GitHub Pages

---

## 项目结构

```
PanelClaw/
└── docs/                   # GitHub Pages 静态网站
    ├── index.html          # 打字机回放播放器
    ├── data/
    │   ├── speakers.json       # 龙虾嘉宾信息
    │   ├── panel_script.json   # Panel 对话记录
    │   ├── panel_summary.json  # AI 秘书结构化总结
    │   └── panel_summary.md    # 可读版总结报告
    ├── assets/
    │   └── avatars/            # 嘉宾头像
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
