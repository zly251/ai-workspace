# AI 工作台 · ai-workspace

> 一个人的 AI 工程实践。把 **Codex / DeepSeek Harness / Claude Code** 三个 Agent 拧成一套能真正交付、而不是只会聊天的流水线。

![状态](https://img.shields.io/badge/status-持续更新-brightgreen)
![文档](https://img.shields.io/badge/docs-%E4%B8%AD%E6%96%87-blue)
![License](https://img.shields.io/badge/license-MIT-lightgrey)

---

## 为什么有这个仓库

网上教你"用 AI 写代码"的内容很多，但大多停在"它给我写了一段能跑"的层次。真正难的是：

- 模型天天在变，**今天能用的免费模型，明天可能就被下架或涨价**；
- 一个 Agent 干不了全活，**规划、执行、验收得分工**；
- AI 说"已完成"和"真的完成"之间，隔着一条**验收鸿沟**。

这个仓库记录我怎么解决这三件事：一套每天自检的模型池、一套三 Agent 分工的协作规范、一套"先拿证据再签字"的验收习惯。

**核心原则：AI 负责干活，人负责拍板和验收。不要把判断权交出去。**

---

## 项目

| 项目 | 说明 |
|---|---|
| [`job-agent`](./job-agent) | 求职助手 · JobAgent：本地运行的自动求职代理，岗位抓取 / 智能匹配 / 自动投递 / 反馈闭环 / 到手价值核算（子模块） |

> `job-agent` 是独立仓库（[zly251/job-agent](https://github.com/zly251/job-agent)），在这里以 git submodule 形式挂载，方便总仓库统一入口。

---

## 我的 AI 三件套

| 角色 | 工具 | 干什么 |
|---|---|---|
| **架构师 / 深读** | Claude Code | 读大代码库、做架构分析、写重构方案；复杂规划优先给它 |
| **落地执行** | Codex（ChatGPT App 内） | 真写文件、跑命令、跑测试；免费档 `gpt-6-luna` 足够日常编码 |
| **日常主力 + 编排** | DeepSeek Harness（DSH） | 长任务、批处理、连知识库、跑子代理；本仓库里大部分自动化都是它做的 |

一句话分工：**Claude Code 想清楚 → Codex 写出来 → DSH 串起来并验收。**

---

## 文档导航

| # | 文档 | 内容 |
|---|---|---|
| 01 | [我的 AI 工作台](./docs/01-我的-AI-工作台.md) | 三个 Agent 怎么分工、为什么这么配、协作规范 |
| 02 | [Codex 免费档实战](./docs/02-Codex-免费档实战.md) | 免费账号能用哪些模型、配额真相、沙箱坑、桌面端身份 |
| 03 | [免费模型池与每日体检](./docs/03-免费模型池与每日体检.md) | 免费 / 限免 / 积分三档管理、两层验收、探活方法 |
| 04 | [踩坑与红线](./docs/04-踩坑与红线.md) | 那些踩过才知道的坑，和几条绝不越过的红线 |

---

## 环境

- Windows 11 · Node.js 18+ · PowerShell 7
- AI 客户端：ChatGPT 桌面 App（Codex）、DSH 桌面端、Claude Code
- 模型路由：自建反代 + 官方免费额度，追求「零成本 / 低成本」跑通全流程

---

## License

MIT © zly251
