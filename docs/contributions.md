# 开源贡献记录 (Open Source Contributions Track Record)

本项目清单收录了在主流开源生态、AI Agent 基础设施及工具链中的代码贡献、架构优化与缺陷修复记录。

---

## 🏛️ 核心贡献项目 (Key Repositories)

### 1. [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers) (Anthropic / MCP 官方参考实现)
> Model Context Protocol (MCP) 官方开源参考服务器套件，连接大语言模型与本地工具/数据源的标准协议实现。

* **问题背景**：Memory 服务在单次 `add_observations` 批处理调用中，如果传入同批重复的 observation 实体观测数据，由于原有过滤逻辑仅对比实体已有数据，导致同批内重复记录被全量多次写入，造成图谱数据冗余污染。
* **技术方案**：在 `KnowledgeGraphManager.addObservations` 中采用 `Set` 集合维护当次批处理与既有观测全集，实现同批传入数据的 O(1) 保序去重与状态一致性保障。
* **官方采纳**：解决方案原型被官方核心维护者 `@cliffhall` 完整采纳并署名致谢合入主线。
* **关联证明**：
  * 官方修复 PR：[#5357 fix(memory): store an observation repeated in one add_observations call once](https://github.com/modelcontextprotocol/servers/pull/5357)（**已合并 Merged**）
  * 官方跟踪 Issue：[#5201 memory: add_observations stores a repeated observation twice](https://github.com/modelcontextprotocol/servers/issues/5201)（**已解决 Closed**）

---

### 2. [langgenius/dify](https://github.com/langgenius/dify) (全球领先的开源 LLMOps 平台)
> 生产级大模型应用编排与 Agent 基础设施平台，GitHub 60k+ Stars。

* **贡献点**：
  * 重构 MCP 工具调用中的类型转换逻辑，消除冗余嵌套 Cast，提升工具执行管道鲁棒性：[PR #44132](https://github.com/langgenius/dify/pull/44132)（**已合并 Merged**）
  * 引入 Pydantic 严格校验 Web 爬取缓存键，防范非法键导致的缓存击穿与未定义行为：[PR #44131](https://github.com/langgenius/dify/pull/44131)（**已合并 Merged**）
  * 修正核心 API 模块日志警告拼写及文档规范：[PR #44134](https://github.com/langgenius/dify/pull/44134)（**已合并 Merged**）

---

### 3. [colbymchenry/codegraph](https://github.com/colbymchenry/codegraph) (代码知识图谱分析引擎)
> 专为大型工程代码库设计的符号图谱定位、调用链与架构拓扑分析引擎。

* **贡献点**：
  * 解决代码分析中浏览器全局方法调用与项目符号同名绑定的误链接问题，构建接收者作用域隔离保护与链路过滤守卫，保持图谱关系纯净。
  * 方案通过核心维护团队严格的多场景集成复测：[PR #2915](https://github.com/colbymchenry/codegraph/pull/2915)（**技术验收通过**）

---

### 4. [datawhalechina/deepagents-in-action](https://github.com/datawhalechina/deepagents-in-action) (Datawhale 智能体实战体系)
> 聚焦多智能体协同、工具调用与生产级架构实战的权威开源教学与实践体系。

* **贡献点**：
  * 纠正代码解释器技能中间件配置规范与运行链路说明，完善开发者实战文档闭环：[PR #167](https://github.com/datawhalechina/deepagents-in-action/pull/167)（**已合并 Merged**）

---

### 5. [farion1231/cc-switch](https://github.com/farion1231/cc-switch) (跨平台多模型 CLI 与桌面端助手)
> 跨平台 AI CLI 工具与模型聚合桌面端网关。

* **贡献点**：
  * 为长会话检索与动态分组接入 300ms 智能防抖机制，保障输入即刻重置与极端输入下的渲染性能：[PR #9006](https://github.com/farion1231/cc-switch/pull/9006)
  * 修复跨平台应用安装路径探测中版本号缺失时的误判逻辑，完善多语言状态回显并隐藏误导性安装操作：[PR #9007](https://github.com/farion1231/cc-switch/pull/9007)
