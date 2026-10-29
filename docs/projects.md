# 项目详情

[← 返回主页](../README.md)

---

## 个人项目

### NexusAgent

基于 LangGraph 的多智能体协作平台，个人独立开发。

- 用 LangGraph 的 StateGraph 编排 Agent 流程，配合 Checkpointer 持久化状态；高风险的工具调用前会暂停，等人工确认后再继续
- 检索部分把 Qdrant 向量检索和 BM25 结合起来，用 RRF 合并排序，改善专有名词的召回
- 做了一个 MCP 客户端，可以接入本地和远程的工具服务；前端是 React 写的三栏工作台，支持 SSE 流式输出

技术栈：Python / FastAPI、LangGraph、Qdrant、React、TypeScript、Docker

### CloudCLI（灵犀）

基于 Claude Agent SDK 的编程助手。

- 封装了多会话的 Agent 运行环境，自己写了几个 MCP 服务（行情数据、多媒体处理），通过 stdio 通信
- 用 node-pty + xterm.js + WebSocket 把命令行交互搬到网页上，同一套代码打包出 Web 版和 Electron 桌面版
- 会话数据存在 SQLite 里，不同工作区之间互相隔离

技术栈：Node.js、TypeScript、React、Electron、SQLite

### Jie's Notes

用 VitePress 搭的个人笔记站，记录学习 AI Agent、后端和系统设计的过程。

[在线访问](https://notes.power8.top/) · [源码](https://github.com/KissFeng/Jie-s-Notes)

---

## 实习与接单项目

> 以下项目代码不公开，只简单介绍做了什么。

### 模型聚合网关

自己搭的一个大模型 API 转发网关，日常一直在用。

- 统一了 OpenAI、Anthropic 等不同厂商的接口格式
- 加了失败重试、备用通道切换和限流，也研究了一下 Prompt Caching 怎么省成本

### 多租户 SaaS（实习）

在公司实习期间参与的企业定制系统开发。

- 负责租户权限、动态表单和部分业务模块
- 优化过一些慢查询（调整索引）并加了 Redis 缓存，核心接口的 P99 延迟降低了 45% 左右
- 对接过微信支付、银联支付和短信服务，用状态机 + 定时对账处理支付回调丢失的情况

### 美业多商户管理系统（接单）

一个独立完成的美业门店管理系统。

- Spring Boot + Vue 3，多个商户共用一套库表，通过租户 ID 做数据隔离
- 接入了大模型的 Function Calling，店长可以直接用自然语言查询流水、会员和业绩数据

---

## 其他

- 3 项实用新型专利（已授权）：移动监控平台、车辆追踪定位装置、多摄像头模组测试设备
- 4 项软件著作权
