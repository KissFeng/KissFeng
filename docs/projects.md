# 核心系统与项目实践 (Featured Projects Architecture)

本项目记录汇总了主导研发的企业级智能体平台、跨端运行时容器及公开知识体系的技术架构与核心特性。

---

## 🤖 1. NexusAgent
> **企业级全栈智能体协同平台 (Multi-Agent Orchestration Platform)** `Proprietary`

* **状态机编排**：基于 LangGraph 深度重构复杂 Agent 协同流，将黑盒隐式 ReAct 循环收敛为确定性的有向状态图（StateGraph），实现全流程状态外部持久化 Checkpointer 快照与高危操作人机在回路（HITL）中断审批。
* **双路混合检索 (Hybrid RAG)**：融合 Qdrant 稠密向量与 Rank-BM25 稀疏切片，结合互易秩融合（RRF）算法进行二次重排，动态注入会话事实偏好、实体画像与长期记忆。
* **MCP 网关与流式工作台**：落地标准 Model Context Protocol（MCP）客户端网关，集成 SSE 极速流式传输与思维链全流程留痕。
* 🔗 [阅读架构演进与设计复盘 ↗](https://notes.power8.top/)

---

## ⚡ 2. CloudCLI (灵犀)
> **跨端智能体编程容器与多 MCP 协同引擎 (Cross-Platform Agent Runtime)**

* **会话容器化**：基于 Claude Agent SDK 深度封装多会话智能体运行容器，自研基于 stdio 进程通信的多媒体与实时数据 MCP 服务，实现进程级隔离与工具链动态热插拔。
* **终端仿真管道**：基于 `node-pty` 与 `@xterm/xterm`（WebGL 硬件加速）构建高保真双向伪终端流，单架构多端交付 Web 网页工作台与 Electron 跨平台桌面端。

---

## 📖 3. Jie's Notes
> **持续沉淀的公开数字花园 (Open Digital Garden & Technical Codex)** `Open Source`
* **知识沉淀**：基于 VitePress 搭建的现代化体系化数字花园，深度沉淀关于 AI Agent 上下文工程、分布式系统高可用、底层内核技术与系统设计的实战笔记与架构思考。
* 🌐 线上站点：[notes.power8.top](https://notes.power8.top/) ｜ 源码：[KissFeng/Jie-s-Notes](https://github.com/KissFeng/Jie-s-Notes)
