# 开源贡献记录

[← 返回主页](../README.md)

在日常使用开源工具的过程中，针对遇到的问题进行定位并提交修复。以下按项目整理目前的贡献。

| 项目 | 贡献数 | 状态 |
| :--- | :---: | :--- |
| modelcontextprotocol/servers | 1 | ✅ 方案被采纳并合并 |
| langgenius/dify | 3 | ✅ 全部合并 |
| datawhalechina/deepagents-in-action | 1 | ✅ 已合并 |
| colbymchenry/codegraph | 1 | 🔄 审查通过，待合并 |
| farion1231/cc-switch | 2 | 🔄 审查中 |

---

## modelcontextprotocol/servers

> Model Context Protocol（MCP）官方参考服务器仓库，包含 memory、filesystem、git 等服务实现。

### Memory 服务：单次调用中的重复观测数据被重复写入

- **问题**：`add_observations` 仅将新内容与实体已有的观测数据比较去重，未处理同一次请求内部的重复项。例如传入 `["x", "x"]` 时，`x` 会被写入两次，返回结果中也会重复报告。
- **方案**：使用 `Set` 同时记录已有数据与本次已接受的数据，逐条判断，在保持原始顺序的前提下去除重复项，并补充相应单元测试。
- **过程**：该仓库不接受外部 PR，仅通过 Issue 协作。我在 Issue 中提交了修复分支与测试结果，维护者参照相同思路实现并合并，在 PR 中注明了参考来源。
- **链接**：[Issue #5201](https://github.com/modelcontextprotocol/servers/issues/5201) · [PR #5357（已合并）](https://github.com/modelcontextprotocol/servers/pull/5357)

---

## langgenius/dify

> 开源大模型应用开发平台。

| 改动 | 链接 | 状态 |
| :--- | :--- | :--- |
| 数据集清理服务中的爬取缓存 key 改用 Pydantic 模型解析，校验 `provider` 与 `job_id`，并拒绝包含 `/`、`\` 等路径穿越字符的 `job_id` | [#44131](https://github.com/langgenius/dify/pull/44131) | ✅ 已合并 |
| 移除 MCP 工具中 `LLMUsage.from_metadata(...)` 调用里冗余的嵌套 `cast` | [#44132](https://github.com/langgenius/dify/pull/44132) | ✅ 已合并 |
| 修正 API 模块日志与文档字符串中的拼写错误 | [#44134](https://github.com/langgenius/dify/pull/44134) | ✅ 已合并 |

---

## datawhalechina/deepagents-in-action

> Datawhale 智能体开发实战教程。

- **问题**：第 7 章示例使用 `CodeInterpreterMiddleware(skills_backend=backend)`，而 `langchain-quickjs` 自 0.2.0 起已移除该参数，按原示例运行会抛出 `TypeError`。
- **改动**：将示例更新为当前可用的 `mode="call"` 写法并注明核对版本，补充解释器执行机制的说明，同时修订章节引言与小结中的相关表述。
- **链接**：[Issue #166](https://github.com/datawhalechina/deepagents-in-action/issues/166) · [PR #167（已合并）](https://github.com/datawhalechina/deepagents-in-action/pull/167)

---

## colbymchenry/codegraph

> 面向代码库的调用关系图分析工具，用于追踪函数间的调用链。

### 浏览器全局对象调用被错误关联至项目方法

- **问题**：分析前端代码时，`localStorage.getItem()`、`history.back()` 等浏览器内置对象的调用，会被错误关联到项目中同名的方法（如 `StorageService.getItem`），导致调用图中出现错误的边。
- **改动**：
  - 识别 `window`、`localStorage`、`history`、`location` 等浏览器全局对象，当调用方为此类对象时不再关联项目方法
  - 支持 `window.localStorage.getItem()`、`self.close()` 等链式调用形式
  - 若文件中存在同名的局部变量、参数或导入绑定（如参数名为 `location`），仍按项目代码正常解析，避免误判
  - 补充正向与反向测试用例
- **过程**：首轮审查中 Reviewer 提出了若干边界情况，修改后经复测确认无遗留问题。
- **链接**：[PR #2915](https://github.com/colbymchenry/codegraph/pull/2915)

---

## farion1231/cc-switch

> 用于切换 Claude Code、Codex 等 AI 编程工具配置的桌面应用（Tauri + React）。

### 会话搜索输入卡顿

- **问题**：会话数量较多时，搜索框每次输入都会触发整个列表的重新筛选与分组，导致明显的输入延迟。
- **改动**：为搜索输入增加 300ms 防抖；清空输入时跳过延迟，立即恢复完整列表，并补充防抖逻辑的单元测试。
- **链接**：[Issue #2376](https://github.com/farion1231/cc-switch/issues/2376) · [PR #9006](https://github.com/farion1231/cc-switch/pull/9006)

### 应用页将「版本读取失败」误显示为「未安装」

- **问题**：在 Windows 环境下，工具已被检测到安装路径，但因版本读取失败，版本列显示为「未安装」并提供「安装」按钮，容易诱导用户重复安装。
- **改动**：在检测到安装路径但未获取版本号时显示「未知」并附加提示，同时隐藏安装按钮；补充 5 种语言的文案及对应测试。
- **链接**：[Issue #8889](https://github.com/farion1231/cc-switch/issues/8889) · [PR #9007](https://github.com/farion1231/cc-switch/pull/9007)
