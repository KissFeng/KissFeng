# 开源贡献记录

[← 返回主页](../README.md)

平时用到的开源工具遇到问题，会顺手看看能不能修。下面是目前提过的贡献，按项目整理。

| 项目 | 贡献数 | 状态 |
| :--- | :---: | :--- |
| modelcontextprotocol/servers | 1 | ✅ 方案被采纳并合并 |
| langgenius/dify | 3 | ✅ 全部合并 |
| datawhalechina/deepagents-in-action | 1 | ✅ 已合并 |
| colbymchenry/codegraph | 1 | 🔄 审查通过，等待合并 |
| farion1231/cc-switch | 2 | 🔄 审查中 |

---

## modelcontextprotocol/servers

> MCP（Model Context Protocol）官方的参考服务器仓库，包含 memory、filesystem、git 等服务。

### Memory 服务：同一次调用里的重复内容会被写入两次

- **问题**：`add_observations` 写入前只会和实体已有的内容比较去重，同一次请求里自己重复的内容不会被过滤。比如传入 `["x", "x"]`，`x` 会被存两次，返回结果里也会报告两次。
- **方案**：用一个 `Set` 记录「已有内容 + 本次已接受的内容」，逐条判断，保持原有顺序的同时去掉重复项，并补了对应的单元测试。
- **过程**：这个仓库不接受外部 PR，只接受 Issue。我把修复分支、测试结果整理后发在了 Issue 下面，维护者按相同思路实现并合并，在 PR 中注明了参考来源。
- **链接**：[Issue #5201](https://github.com/modelcontextprotocol/servers/issues/5201) · [PR #5357（已合并）](https://github.com/modelcontextprotocol/servers/pull/5357)

---

## langgenius/dify

> 开源的大模型应用开发平台。

| 改动 | 链接 | 状态 |
| :--- | :--- | :--- |
| 数据集清理服务里的爬取缓存 key 改用 Pydantic 模型解析，校验 `provider` 和 `job_id`，并拒绝包含 `/`、`\` 等路径穿越字符的 `job_id` | [#44131](https://github.com/langgenius/dify/pull/44131) | ✅ 已合并 |
| 去掉 MCP 工具里 `LLMUsage.from_metadata(...)` 调用中一层多余的 `cast` | [#44132](https://github.com/langgenius/dify/pull/44132) | ✅ 已合并 |
| 修正 API 模块日志和文档字符串里的拼写错误 | [#44134](https://github.com/langgenius/dify/pull/44134) | ✅ 已合并 |

---

## datawhalechina/deepagents-in-action

> Datawhale 的智能体开发实战教程。

- **问题**：第 7 章示例使用 `CodeInterpreterMiddleware(skills_backend=backend)`，但 `langchain-quickjs` 从 0.2.0 起已移除这个参数，照着运行会直接报 `TypeError`。
- **改动**：把示例改成当前可运行的 `mode="call"` 写法，注明核对的版本，补充解释器的执行方式说明，并同步修改章节引言和小结里的相关描述。
- **链接**：[Issue #166](https://github.com/datawhalechina/deepagents-in-action/issues/166) · [PR #167（已合并）](https://github.com/datawhalechina/deepagents-in-action/pull/167)

---

## colbymchenry/codegraph

> 给代码库建立调用关系图的工具，用来分析函数之间的调用链。

### 浏览器全局对象的调用被错误关联到项目方法

- **问题**：分析前端代码时，`localStorage.getItem()`、`history.back()` 这类浏览器自带对象的调用，会被关联到项目里恰好同名的方法上（比如某个 `StorageService.getItem`），导致调用图出现错误的边。
- **改动**：
  - 识别 `window`、`localStorage`、`history`、`location` 等浏览器全局对象，调用者是它们时不再关联项目方法
  - 处理 `window.localStorage.getItem()`、`self.close()` 这种链式写法
  - 如果文件里有同名的局部变量、参数或导入（例如函数参数就叫 `location`），仍然按项目代码正常解析，避免误伤
  - 补充了正反两类测试用例
- **过程**：Reviewer 第一轮指出了几个边界情况，修改后重新验证，确认没有遗留问题。
- **链接**：[PR #2915](https://github.com/colbymchenry/codegraph/pull/2915)

---

## farion1231/cc-switch

> 用来切换 Claude Code、Codex 等 AI 编程工具配置的桌面应用（Tauri + React）。

### 会话搜索输入卡顿

- **问题**：会话较多时，搜索框每输入一个字都会重新筛选、分组整个列表，打字明显卡顿。
- **改动**：给搜索加了 300ms 防抖；清空搜索框时跳过等待，立即恢复完整列表。补了防抖逻辑的单元测试。
- **链接**：[Issue #2376](https://github.com/farion1231/cc-switch/issues/2376) · [PR #9006](https://github.com/farion1231/cc-switch/pull/9006)

### 应用页把「读不到版本」显示成「未安装」

- **问题**：在 Windows 上，工具明明已经检测到了安装路径，但因为读取版本失败，版本列显示「未安装」，还给出一个「安装」按钮，容易让人重复安装。
- **改动**：检测到安装路径但没拿到版本号时，显示「未知」并加上提示，同时隐藏安装按钮；补充了 5 种语言的文案和对应测试。
- **链接**：[Issue #8889](https://github.com/farion1231/cc-switch/issues/8889) · [PR #9007](https://github.com/farion1231/cc-switch/pull/9007)
