<div align="center">

<img src="./assets/banner.svg" alt="KissFeng Header" width="100%" />

<br>

<p align="center">
  <a href="https://notes.power8.top/"><img src="https://img.shields.io/badge/Digital_Garden-notes.power8.top-0a0e17?style=flat-square&logo=gitbook&logoColor=38bdf8" alt="Digital Garden" /></a>
  <a href="https://github.com/KissFeng"><img src="https://img.shields.io/badge/GitHub-KissFeng-0a0e17?style=flat-square&logo=github&logoColor=white" alt="GitHub" /></a>
  <a href="mailto:kissfeng6699@gmail.com"><img src="https://img.shields.io/badge/Email-kissfeng6699%40gmail.com-0a0e17?style=flat-square&logo=gmail&logoColor=white" alt="Email" /></a>
</p>

<!-- Dynamic Architectural Motto -->
<a href="https://git.io/typing-svg">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=500&size=16&pause=1200&color=38BDF8&center=true&vCenter=true&width=720&lines=Designing+deterministic+runtimes+for+probabilistic+intelligence.;StateGraph+%C2%B7+Human-in-the-Loop+%C2%B7+Model+Context+Protocol+(MCP).;Architecting+production+model+gateways+across+billions+of+tokens.;First+principles.+Explicit+abstractions.+Production+resilience." alt="Typing SVG" />
</a>

</div>

---

### 🏛️ 核心架构主张 (Architectural Philosophy)

专注于探索**自主智能体（Autonomous Agents）**、**显式状态机**与**生产级系统工程闭环**。致力于连接大语言模型的概率推理与工业级软件的确定性控制：

* **显式状态机与可恢复运行时 (Deterministic State Runtimes)**  
  主张摒弃黑盒 ReAct 隐式循环，采用基于有向状态图（StateGraph）对复杂多步工具流进行严格建模。通过外部持久化 Checkpointer 快照与中断机制（`interrupt` / `Command.resume`），实现高危操作的人机在回路（HITL）审批拦截与幂等断点续跑。

* **混合上下文工程与消歧长记忆 (Context Engineering & Hybrid Retrieval)**  
  深耕检索召回边界与长上下文治理。构建融合 Qdrant 稠密向量与 Rank-BM25 稀疏切片的双路混合检索体系（Reciprocal Rank Fusion 重排），结合置信度消歧与事实无感沉淀，有效遏制长会话膨胀与模型幻觉。

* **高吞吐生产网关与工程韧性 (Production Gateway & Resilience)**  
  主导自研模型聚合路由网关，月均承载 **20~50 亿 Tokens** 真实交互流量。在流式降级、Prompt 缓存利用率优化、多步 Tool Calling 全链路 Trace 打点与超时自纠偏沙箱方面沉淀深度生产实战。

---

### 📦 核心系统代表作 (Featured Systems)

#### 🤖 [NexusAgent](https://github.com/KissFeng/NexusAgent)
> **企业级全栈智能体协同平台 (Multi-Agent Orchestration Platform)**
* **状态机编排**：基于 LangGraph 深度重构复杂 Agent 协同流，实现全流程状态外部持久化与人机审批在回路。
* **双路混合检索**：融合稠密向量与稀疏切片（RRF 重排），动态注入会话事实偏好。
* **MCP 网关与流式工作台**：落地标准 Model Context Protocol（MCP）客户端网关，集成 SSE 极速流式传输与思维链留痕。

#### ⚡ CloudCLI (灵犀)
> **跨端智能体编程容器与多 MCP 协同引擎 (Cross-Platform Agent Runtime)**
* **会话容器化**：基于 Claude Agent SDK 封装多会话智能体运行容器，自研基于 stdio 进程通信的多媒体与实时数据 MCP 服务。
* **终端仿真管道**：基于 `node-pty` 与 `@xterm/xterm`（WebGL 硬件加速）构建高保真双向伪终端流，单架构多端交付 Web 与 Electron 桌面端。

#### 📖 [Jie's Notes (个人公开知识库)](https://notes.power8.top/) ｜ [Source](https://github.com/KissFeng/Jie-s-Notes)
> **持续生长的个人数字花园 (Open Digital Garden & Technical Codex)**
* 基于 VitePress 搭建的现代化体系化知识库，沉淀关于 AI Agent 上下文工程、分布式系统高可用、底层内核技术与系统设计的实战思考。

#### 🛡️ [Scene-Port-Hider-by-eBPF](https://github.com/KissFeng/Scene-Port-Hider-by-eBPF)
> **基于 Linux eBPF 的内核态网络观测与隐蔽实践**
* 探索 Linux 内核态可编程网络包过滤、底层可观测性与网络安全前沿机制。

---

### ⚡ 核心技术栈 (Core Technologies)

```text
  Autonomous Agents  │ LangGraph · Claude Agent SDK · MCP Protocol · Hybrid RAG · Qdrant
  Systems & Backend  │ Python (FastAPI) · Java (Spring Boot) · Linux / eBPF · Redis · MySQL · RabbitMQ
  Frontend & Desktop │ React 19 · TypeScript · Next.js · Electron · Tailwind CSS · Vite
  Infrastructure     │ Docker · Nginx · Linux System Engineering · GitHub Actions CI/CD
```

---

### 🔬 研发与知识产权沉淀 (Research & Systems)

* **国家实用新型专利（已授权）**：
  * 《一种移动监控平台》
  * 《一种车辆追踪定位装置》
  * 《一种多摄像头模组测试设备》
* **计算机软件著作权登记**：
  * 4 项系统级软件著作权（涵盖工业 MES 数字孪生平台、智能视觉检测等）

---

### 📈 活跃度与工程节奏 (Activity & Metrics)

<div align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/KissFeng/KissFeng/output/github-contribution-grid-snake-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/KissFeng/KissFeng/output/github-contribution-grid-snake.svg">
    <img alt="GitHub contribution grid snake" src="https://raw.githubusercontent.com/KissFeng/KissFeng/output/github-contribution-grid-snake.svg" width="100%">
  </picture>
</div>

<br>

<div align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=KissFeng&show_icons=true&theme=radical&hide_border=true&bg_color=080c14&title_color=38bdf8&icon_color=38bdf8&text_color=94a3b8" alt="KissFeng's GitHub stats" height="155" />
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=KissFeng&layout=compact&theme=radical&hide_border=true&bg_color=080c14&title_color=38bdf8&text_color=94a3b8" alt="Top Langs" height="155" />
</div>

---

<div align="right">
  <img src="./assets/signature.svg" alt="KissFeng Signature" width="260px" />
</div>
