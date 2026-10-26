<div align="center">

<img src="./assets/banner.webp" alt="KissFeng Banner" width="100%" />

<br><br>

# Power (KissFeng)

**Systems & Agent Runtime Engineer**

致力于连接大语言模型的概率推理与工业级软件的确定性控制  
*Focused on Deterministic State Runtimes, Context Engineering, and High-Throughput Model Gateways.*

<p align="center">
  <a href="https://notes.power8.top/"><img src="https://img.shields.io/badge/Digital_Garden-notes.power8.top-0a0e17?style=flat-square&logo=gitbook&logoColor=38bdf8" alt="Digital Garden" /></a>
  <a href="https://github.com/KissFeng"><img src="https://img.shields.io/badge/GitHub-KissFeng-0a0e17?style=flat-square&logo=github&logoColor=white" alt="GitHub" /></a>
  <a href="mailto:kissfeng66@gmail.com"><img src="https://img.shields.io/badge/Email-kissfeng66%40gmail.com-0a0e17?style=flat-square&logo=gmail&logoColor=white" alt="Email" /></a>
</p>

</div>

---

### 🏛️ 核心架构主张 (Engineering Philosophy)

* **显式状态机与可恢复运行时 (Deterministic State Runtimes)**  
  摒弃黑盒 ReAct 隐式循环，采用基于有向状态图（StateGraph）对复杂多步工具流进行严格建模。通过外部持久化 Checkpointer 快照与中断机制（`interrupt` / `Command.resume`），实现高危操作的人机在回路（HITL）审批拦截与幂等断点续跑。

* **混合上下文工程与消歧长记忆 (Context Engineering & Hybrid Retrieval)**  
  深耕检索召回边界与长上下文治理。构建融合 Qdrant 稠密向量与 Rank-BM25 稀疏切片的双路混合检索体系（Reciprocal Rank Fusion 重排），结合置信度消歧与事实无感沉淀，有效遏制长会话膨胀与模型幻觉。

* **高吞吐生产网关与工程韧性 (Production Gateway & Resilience)**  
  主导自研模型聚合路由网关，沉淀月均承载数亿至数十亿级 Tokens 真实交互流量的生产实战。在流式降级、Prompt 缓存复用、多步 Tool Calling 全链路 Trace 打点与超时自纠偏沙箱方面具备成熟工程落地。

---

### 📦 核心系统与架构代表作 (Featured Systems & Case Studies)

#### ✦ NexusAgent `Proprietary`
> **企业级全栈智能体协同平台 (Multi-Agent Orchestration Platform)**
> 
> * **状态机编排**：基于 LangGraph 深度重构复杂 Agent 协同流，实现全流程状态外部持久化与人机审批在回路。
> * **双路混合检索**：融合稠密向量与稀疏切片（RRF 重排），动态注入会话事实偏好与长期记忆。
> * **MCP 网关与流式工作台**：落地标准 Model Context Protocol（MCP）客户端网关，集成 SSE 极速流式传输与思维链留痕。
> * 🔗 *[阅读架构演进与设计复盘 ↗](https://notes.power8.top/)*

#### ✦ CloudCLI (灵犀)
> **跨端智能体编程容器与多 MCP 协同引擎 (Cross-Platform Agent Runtime)**
> 
> * **会话容器化**：基于 Claude Agent SDK 封装多会话智能体运行容器，自研基于 stdio 进程通信的多媒体与实时数据 MCP 服务。
> * **终端仿真管道**：基于 `node-pty` 与 `@xterm/xterm`（WebGL 硬件加速）构建高保真双向伪终端流，单架构多端交付 Web 与 Electron 桌面端。

#### ✦ [Jie's Notes](https://notes.power8.top/) ｜ [Source](https://github.com/KissFeng/Jie-s-Notes) `Open Source`
> **持续沉淀的公开数字花园 (Open Digital Garden & Technical Codex)**
> 
> * 基于 VitePress 搭建的现代化体系化知识库，沉淀关于 AI Agent 上下文工程、分布式系统高可用、底层内核技术与系统设计的实战思考。

---

### ⚡ 技术图谱与工程能力 (Technical Focus)

```text
AI & Agent Core    :: LangGraph · Claude Agent SDK · Model Context Protocol (MCP) · Qdrant · RRF Hybrid Search
Backend & Systems  :: Python (FastAPI) · Java (Spring Boot 3) · Redis · MySQL · RabbitMQ
Frontend Workflows :: React 19 · Next.js · TypeScript · TailwindCSS · Electron · Vite
Infrastructure     :: Docker · Linux · Nginx · GitHub Actions · Vercel
```

---

<div align="right">
  <img src="./assets/signature.svg" alt="KissFeng Signature" width="220px" />
</div>
