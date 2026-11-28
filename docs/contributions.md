# 开源贡献记录

[← 返回主页](../README.md)

在日常使用开源工具的过程中，针对遇到的问题进行定位并提交修复。以下按项目整理目前的贡献。

最近核对：**2026-11-28**。状态依据 GitHub PR 页面及讨论记录；「已合并」指本人提交的 PR 直接合并，「方案被采纳」指维护者在其他 PR 中参考或整合了相关方案。

| 项目 | 贡献数 | 状态 |
| :--- | :---: | :--- |
| modelcontextprotocol/servers | 1 | ✅ Issue 中的方案被参考，维护者 PR 已合并 |
| langgenius/dify | 3 | ✅ 全部合并 |
| datawhalechina/deepagents-in-action | 1 | ✅ 已合并 |
| dgilland/pydash | 1 | ✅ 已合并 |
| python-mechanize/mechanize | 1 | ✅ 已合并 |
| click-contrib/click-option-group | 1 | ✅ 已合并 |
| jkroso/parse-duration | 1 | ✅ 已合并 |
| userfypp/plan-measure | 1 | ✅ 已合并 |
| himanshu231204/prompt-migrate | 1 | ✅ 已合并 |
| colbymchenry/codegraph | 2 | ✅ 方案被采纳；本人 PR 被替代关闭 |
| pingdotgg/t3code | 1 | 🔄 开放待审 |
| apostrophecms/apostrophe | 1 | 🔄 开放中，维护者已回复将纳入 12 月版本评估 |
| farion1231/cc-switch | 2 | 🔄 1 条解决冲突待复审；1 条因上游后端已修复而关闭 |
| NousResearch/hermes-agent | 1 | 🔄 开放中，已追加隔离测试提交，局部测试通过 |
| moleculerjs/moleculer | 1 | 🔄 开放待审 |
| jonaskello/tsconfig-paths | 1 | 🔄 开放待审 |
| MartinThoma/flake8-simplify | 1 | 🔄 开放待审 |
| openclaw/openclaw | 1 | ⚪ 因重复关闭，未合并（关联 PR 已合并） |

以上包含 **10 条本人 PR 直接合并、3 项方案被参考或整合、7 条 PR 开放待审、2 条 PR 因上游已修复或重复而关闭**。个人仓库及 fork 内的测试 PR 不计入。

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
- **过程**：首轮审查中 Reviewer 提出了若干边界情况，修改后经复测确认无遗留问题。维护者随后在 PR [#3026](https://github.com/colbymchenry/codegraph/pull/3026) 中参考并重新实现该修复，注明了原 PR 来源；本人 PR #2915 被替代关闭，未直接合并。
- **链接**：[PR #2915（被替代关闭）](https://github.com/colbymchenry/codegraph/pull/2915) · [维护者 PR #3026（已合并）](https://github.com/colbymchenry/codegraph/pull/3026)

### 索引构建期间执行 status 命令触发数据库锁异常

- **问题**：在后台执行 `codegraph index` 或大批量边加载时运行 `codegraph status`，由于 status 命令以读写模式打开数据库，会触发打开时的索引自愈操作并修改 SQLite schema，导致正在运行的写入事务被中断，抛出 `SQLITE_BUSY_SNAPSHOT (517) / database is locked`。
- **方案**：在 status 命令中传入 `{ readOnly: true }`，使连接在只读模式下立即返回，跳过迁移、批量加载自愈及 WAL 维护；增加模拟索引重构与 status 命令并发调用的测试用例。
- **过程**：维护者在 PR [#2930](https://github.com/colbymchenry/codegraph/pull/2930) 中整合了同类修复，并纳入本人测试中「写事务期间运行 status」的交错场景，在 Changelog 中注明致谢。本人 PR #2916 被替代关闭，未直接合并。
- **链接**：[Issue #2913](https://github.com/colbymchenry/codegraph/issues/2913) · [PR #2916（被替代关闭）](https://github.com/colbymchenry/codegraph/pull/2916) · [维护者 PR #2930（已合并）](https://github.com/colbymchenry/codegraph/pull/2930)

---

## farion1231/cc-switch

> 用于切换 Claude Code、Codex 等 AI 编程工具配置的桌面应用（Tauri + React）。

### 会话搜索输入卡顿

- **问题**：会话数量较多时，搜索框每次输入都会触发整个列表的重新筛选与分组，导致明显的输入延迟。
- **改动**：为搜索输入增加 300ms 防抖；清空输入时跳过延迟，立即恢复完整列表，并补充防抖逻辑的单元测试。
- **进展**：11 月 2 日因缺少 PR 模板要求的「Human Note / 本人说明」被暂时关闭，补齐并回复后由维护者重新开启。随后维护者 `@funkpopo` 指出开启「搜索消息正文」时存在输入闪烁与双防抖竞态，统一复用单个 `useDebouncedValue` 后于 11 月 21 日获得 **LGTM** 复核；同日因合入上游搜索报错提示与重试逻辑重新解决冲突并推送最新提交，目前等待复审，尚未合并。
- **链接**：[Issue #2376](https://github.com/farion1231/cc-switch/issues/2376) · [PR #9006（开放待复审）](https://github.com/farion1231/cc-switch/pull/9006)

### 应用页将「版本读取失败」误显示为「未安装」

- **问题**：在 Windows 环境下，工具已被检测到安装路径，但因版本读取失败，版本列显示为「未安装」并提供「安装」按钮，容易诱导用户重复安装。
- **改动**：在检测到安装路径但未获取版本号时显示「未知」并附加提示，同时隐藏安装按钮；补充 5 种语言的文案及对应测试。
- **过程**：维护者指出配置目录指向 WSL 时若 WSL 内未安装需保留安装按钮的边界情况；已补充 `installedButUnknown` 判定与 WSL 单测。11 月 2 日因缺少「Human Note / 本人说明」被暂时关闭，补齐后重新开启；11 月 16 日维护者说明 `main` 分支已在后端（`e78f641ca`）修复该问题（找到可执行文件但读取不到版本时直接提示「无法运行」并隐藏安装按钮），前端兜底基本不再触发，因此关闭该 PR，**未合并**。
- **链接**：[Issue #8889](https://github.com/farion1231/cc-switch/issues/8889) · [PR #9007（上游已修复而关闭，未合并）](https://github.com/farion1231/cc-switch/pull/9007)

---

## NousResearch/hermes-agent

> 开源自主 AI Agent 框架与运行时环境。

### 单进程运行测试套件时上下文状态与环境变量跨测试泄漏

- **问题**：在单一 pytest 进程下运行 `tests/tui_gateway/` 全量测试套件时，由于 `test_agent_rebuild_keeps_pre_compression_process_owners` 模拟 `_release_build_profile_scopes` 时未执行实际释放，导致 `_SECRET_SCOPE` ContextVar 泄露到后续用例中，引发 8 个 fail-closed 用例因未捕获到预期的 `UnscopedSecretError` 而失败；同时 `_HERMES_BEHAVIORAL_VARS` 缺少对 `HERMES_PROFILE` 等环境变量的屏蔽，宿主环境容易渗入单测。
- **改动**：
  - 在会话重构测试中恢复调用真实的 profile scope 释放逻辑，并在用例结束时显式断言上下文干净；
  - 在 `tests/conftest.py` 中为 `_SECRET_SCOPE` 与 `_MULTIPLEX_CONTEXT` 注入独立 `ContextVar`，确保每个用例拥有隔离的上下文环境；
  - 在 `tests/_fixtures/env_filter.py` 中补充 `HERMES_PROFILE` 与 `HERMES_PROFILE_NAME` 过滤项；
  - 11 月 16 日追加提交 `d2d9dd32`，进一步隔离 TUI 广播状态与 fallback 存储相关单测。
- **进展**：11 月 1 日，贡献者 whyyagswhy 反馈在提交 `613c8a27` 上运行 `test_detached_process_notify_keepalive.py`，结果为 **21 passed、0 failed**，三个改动文件的 Ruff 检查也通过；11 月 16 日已推送后续测试隔离提交。PR 目前仍开放，尚无正式 Review，也未合并。
- **链接**：[Issue #147198](https://github.com/NousResearch/hermes-agent/issues/147198) · [PR #147223（开放待审）](https://github.com/NousResearch/hermes-agent/pull/147223)

---

## openclaw/openclaw

> 开源自主多平台 AI Agent 框架。

### read 工具拒绝模型显式传入的 optional: false 参数

- **问题**：`read` 工具的输入 Schema 将 `optional` 字段硬编码为 `Type.Optional(Type.Literal(true))`，当模型显式传入 `"optional": false` 表示文件必须存在时，会触发 Schema 校验错误 `optional: must be equal to constant` 并导致多余的模型轮次重试。
- **改动**：
  - 将输入 Schema 中的 `optional` 属性放宽为 `Type.Optional(Type.Boolean())`，与底层文件读取的语义判定保持一致；
  - 同步更新 Code Mode 的提示词签名预期（由 `optional?: true` 调整为 `optional?: boolean`）；
  - 补充通过参数校验层到读取执行的回归测试。
- **过程**：机器人审查认可放宽输入 Schema 的修复方向，但认为更早的 [PR #189494](https://github.com/openclaw/openclaw/pull/189494) 已覆盖同一问题，且有更完整的 Gateway 行为证据。因此本人 PR #189497 于 11 月 1 日以重复／被替代为由关闭，**未合并**；关联 PR #189494 已于 11 月 19 日合并进入主分支（`1039d56001`）。
- **链接**：[Issue #189440](https://github.com/openclaw/openclaw/issues/189440) · [PR #189497（重复关闭，未合并）](https://github.com/openclaw/openclaw/pull/189497) · [关联 PR #189494（已合并）](https://github.com/openclaw/openclaw/pull/189494)

---

## pingdotgg/t3code

> 面向 Claude Code、Codex 等 AI 编程代理的桌面与 Web 协同控制端。

### Codex 探针超时误杀本地状态库回填进程导致 Provider 长期锁死

- **问题**：当 `codex app-server` 面对包含大量历史会话的 `CODEX_HOME` 启动时，会在响应 `initialize` 前执行本地 SQLite 状态库（`state_5.sqlite`）回填。若回填耗时超过 T3 Code 默认的 20 秒探针超时，`probeCodexAppServerProvider` 会立即关闭 `processScope` 并在回填中途杀死进程，留下 15 分钟有效期的 `backfill_state.status = 'running'` 租约，导致后续每次探针最多阻塞 30 秒后再次在 20 秒时被杀，Provider 持续锁死为不可用。
- **改动**：
  - 仅在 `initialize` 完成前发生探针超时时，通过 `node:sqlite` 只读检查 `<codexHome>/state_<N>.sqlite` 的 `backfill_state`（正常路径零开销）；
  - 通过 `onSpawn` 记录子进程句柄，若当前探针确实持有正在进行的回填，则将 `processScope` 移交至有界后台协程（`stopCodexAfterBackfill`，最长等待 5 分钟）直至回填结束或进程退出；其余等待型探针与真正卡死的探针仍立即关闭；
  - 对齐 Codex `sqlite_home` 解析优先级与启动参数分词逻辑，并在超时处于回填中时向前端返回可操作的提示信息；补充多组确定性回归测试。
- **进展**：11 月 28 日提交 Issue 与 PR，目前开放待审。
- **链接**：[Issue #44629](https://github.com/pingdotgg/t3code/issues/44629) · [PR #44640（开放待审）](https://github.com/pingdotgg/t3code/pull/44640)

---

## dgilland/pydash

> Python 函数式工具库（对标 JavaScript Lodash）。

### 有限坐标差值溢出导致 `slope` 返回 `NaN` 或错误结果

- **问题**：计算两点斜率时（如 `slope((1e308, 1e308), (-1e308, -1e308))`），分子或分母的浮点差值会先发生溢出，导致本应为有限值 `1.0` 的斜率返回 `NaN`、零或无穷大。
- **改动**：当浮点差值溢出且坐标均为有限 `int` / `float` 时，改用 `Fraction` 计算比值后再转回 `float`；保持普通数值、`Decimal`、`Fraction`、垂直线及非有限数输入原有路径，并补充 6 组回归用例与对照组测试。
- **链接**：[PR #467（已合并）](https://github.com/dgilland/pydash/pull/467)

---

## python-mechanize/mechanize

> 经典 Python 编程式 Web 浏览器库。

### 响应末尾存在零填充时 gzip 解压抛出 `struct.error`

- **问题**：`UnzipWrapper.read()` 将 deflate 流之后缓冲区中的所有剩余字节一并传入 `struct.unpack`，而 `struct.unpack` 严格要求 8 字节尾部，导致带零填充字节的 gzip 响应在特定读取分片边界下抛出 `struct.error`。
- **改动**：改为仅解包 8 字节 gzip 尾部，保留 CRC 校验及尾部截断报错行为，并补充覆盖空响应体、0/1/2048 填充字节、短读与截断尾部的测试用例。
- **链接**：[PR #106（已合并）](https://github.com/python-mechanize/mechanize/pull/106)

---

## click-contrib/click-option-group

> Click 命令行框架的选项组扩展库。

### `AllOptionGroup` 未统计环境变量提供的选项值

- **问题**：`AllOptionGroup` 校验时仅检查命令行参数，未计入通过环境变量传入的值，导致部分或全部选项由环境变量提供时被误判为不完整，或反过来在仅环境变量提供部分选项时错误放行。
- **改动**：在保留命令行参数优先级与忽略默认值约束的前提下，将 Click 通过显式 `envvar`、自动前缀、多值与布尔假值开关等环境变量机制注入的选项纳入校验计数，并补充 Click 7.1.2 / 8.5.1 回归测试。
- **链接**：[PR #74（已合并）](https://github.com/click-contrib/click-option-group/pull/74)

---

## apostrophecms/apostrophe

> 基于 Node.js 的开源全栈 CMS 框架（含 `sanitize-html` 核心包）。

### `sanitize-html` 复用全局或粘性正则时 `lastIndex` 状态污染

- **问题**：在 `allowedClasses` 或 `allowedStyles` 中传入带 `g` 或 `y` 标志的正则表达式时，每次匹配会推进其 `lastIndex`，导致同一组规则在后续类名或样式值校验中意外失效，或受到调用前遗留非零 `lastIndex` 的影响。
- **改动**：每次匹配前重置为从索引 `0` 开始校验，并在匹配结束后（包括抛出异常时）恢复调用方原始 `lastIndex`，同时保持粘性正则仅从起始位置匹配的语义；补充测试用例与 changeset。
- **进展**：11 月 16 日维护者 `@boutell` 回复确认将进行评估，若通过将纳入 12 月版本发布。
- **链接**：[PR #5745（开放待审）](https://github.com/apostrophecms/apostrophe/pull/5745)

---

## 其他开源项目贡献

| 项目 | 改动 | 链接 | 状态 |
| :--- | :--- | :--- | :--- |
| **jkroso/parse-duration** | 在文档与测试中明确自定义本地化单位须按从大到小排序以维持前缀推断与查找性能 | [#78](https://github.com/jkroso/parse-duration/pull/78) | ✅ 已合并 |
| **userfypp/plan-measure** | 在浏览器 PDF 测量工具中实现外部页面导航后同步更新 Pages 面板选中态与 ARIA 状态 | [#522](https://github.com/userfypp/plan-measure/pull/522) | ✅ 已合并 |
| **himanshu231204/prompt-migrate** | 为 Python 3.10/3.12/3.13 CI 增加构建后 wheel / sdist 独立虚拟环境安装冒烟测试 | [#67](https://github.com/himanshu231204/prompt-migrate/pull/67) | ✅ 已合并 |
| **moleculerjs/moleculer** | 为 `Context.call`、`ServiceBroker.call` 与 `callWithoutBalancer` 参数类型补充默认 `unknown`，支持仅指定返回值泛型 | [#1380](https://github.com/moleculerjs/moleculer/pull/1380) | 🔄 开放待审 |
| **jonaskello/tsconfig-paths** | 将相对路径过滤收窄至 `.` 与 `..` 段，支持通过 `baseUrl`/`paths` 解析以 `.` 开头的非相对目录名（如 `.foo/bar`） | [#293](https://github.com/jonaskello/tsconfig-paths/pull/293) | 🔄 开放待审 |
| **MartinThoma/flake8-simplify** | 将 SIM906 对嵌套 `os.path.join` 的扁平化限制在首参数安全前缀，避免破坏 Windows 盘符语义与 `*args` 异常行为 | [#227](https://github.com/MartinThoma/flake8-simplify/pull/227) | 🔄 开放待审 |
