---
name: daily-product-analysis
version: 1.0.0
description: 每日产品分析教练 — 从 TrustMRR + Toolify.ai + There's An AI For That 三源选品，8步框架深度分析3个关联产品，训练产品嗅觉。
triggers:
  - 产品分析
  - 分析产品
  - 产品教练
  - daily product
  - 今天分析
  - 选品分析
---

# 每日产品分析教练

训练 Bruce 的需求嗅觉。每次从三个来源选 3 个有逻辑关联的产品，执行 8 步分析框架。

## 核心约束

- **不重复**：每次分析前回顾已分析产品清单
- **三源结合**：必须从 TrustMRR / Toolify.ai / TAAFT 中至少 2 个来源选品
- **逻辑关联**：3 个产品之间必须有明确的对比/替代/纵向关系
- **4000 字以内**（8步框架+7项附加内容较多，单产品约1000-1200字是合理密度）
- **输出到 `~/产品分析/` 目录**（Markdown + YAML frontmatter）
- **Obsidian 兼容格式**

## 三个数据来源

| 来源 | URL | 价值 | 注意事项 |
|------|-----|------|----------|
| **TrustMRR** | https://trustmrr.com | 已验证 MRR 数据，真实标杆 | Feed 页面可直接抓取；产品详情页 `/startup/{name}` 有收入图表、定价、技术栈 |
| **Toolify.ai** | https://www.toolify.ai/zh/ | AI 工具目录，按类别发现 | ⚠️ **Cloudflare 防护**，必须用 Chrome DevTools MCP（headed 模式）绕过。见下方「数据源访问方案」 |
| **There's An AI For That** | https://theresanaiforthat.com | 按任务反向找 AI 工具 | 首页可直接抓取 trending + 最新工具；详情页 `/ai/{name}` 被 Cloudflare 拦截时用 DevTools MCP |

## 选品规律（三选一，轮流使用）

### 规律 1：锚点对比法
- **A**：TrustMRR 中等收入产品（MRR $5K–$50K）
- **B**：Toolify/TAAFT 与 A 解决同一问题的 AI 工具
- **C**：TAAFT 与 A 同类型任务的另一个 AI 工具

### 规律 2：收入验证 + AI 替代
- **A**：TrustMRR 非 AI 传统 SaaS
- **B**：Toolify/TAAFT 宣称替代传统 SaaS 的 AI 工具
- **C**：TAAFT 同一任务场景的最新 AI 工具

### 规律 3：纵向挖掘
- **A**：TrustMRR 高增长产品（MoM > 20%）
- **B**：Toolify/TAAFT 该类别 Top 3 中未被分析的
- **C**：TAAFT 该产品用户还搜索了什么其他任务

## 8 步分析框架（每个产品必做）

### Step 1：产品定位与体验
一句话定位、目标用户、核心功能（≤5）、用户路径（进入→核心价值到手）

### Step 2：问题与价值（禁止抽象）
- 之前怎么解决？
- 解决了什么痛苦？
- 没有它用什么替代？
- 为什么付费？（具体到哪个环节）

### Step 3：商业模式拆解
变现方式、谁付钱、收费点在哪

### Step 4：收入估算（必须用公式）
**月收入 ≈ 月流量 × 付费转化率 × 客单价**
- 每个参数一句话推理依据
- 输出低/中/高三个估值

### Step 5：技术实现路径
前端形态、后端核心、存储方案、AI 用法、最棘手的 2 个技术难点

### Step 6：增长方式（重点）
主要流量来源、为什么能获取流量、最值得复制的 1 个增长动作

### Step 7：对我的启发（必须具体）
- 最值得抄的 1 个点（思路不是代码）
- 我可以快速做一个什么类似产品？（名字+场景+一句话，不限技术栈）

### Step 8：程序员思维盲区
一句话戳破思维误区

## 附加要求：需求嗅觉训练（每个产品必做）

在每个产品的分析中，必须额外包含以下内容（可合并到对应步骤或独立成小节）：

### A1：用户原声
引用 1-2 条真实用户评论/抱怨原话及来源（如 Product Hunt、Reddit、G2、Twitter）。用搜索引擎查找。没有真实评论则标注"未找到真实原声"并写一句推测的用户抱怨。

### A2：痛点量化
- **时间成本**：用户每周花多少小时在这问题上？
- **金钱成本**：替代方案（没有这个产品时）花费多少？
- **情绪成本**：1-10 级 + 原因（如"手动重复操作，7级，枯燥到想砸键盘"）

### A3：需求风险
分析该需求是：
- 高频/低频？使用频率
- 刚需/痒点？没了它用户会怎样
- 是否可能被**平台方**（如大厂内置功能）消灭？
- 是否可能被**技术迭代**（如 GPT-6 免费做到）消灭？

### A4：价格锚点
- 用户不买这个产品会花多少钱解决问题？（人工/外包/竞品）
- 同类非 AI 工具定价是多少？

### A5：最小验证方法
不写代码的情况下，如何用 **24 小时**验证这个需求有人愿意付费？具体到操作步骤。

### A6：定制盲区
针对**个人开发者/独立开发者**，指出会在这个产品上犯的**具体工程决策错误**。不是泛泛的"过度设计"，而是具体到"你会花3周搭基础设施但应该先手动接单验证需求"这种级别。关注个人开发者的典型陷阱：过度工程化、忽略BD/运营、一个人想做全平台等。

### A7：需求-收入关联（最终总结中完成）
对比本次三个产品：**哪个需求更痛但收入更低？为什么？**
- 需求痛点排序（1→3，1 最痛）
- 收入排序（1→3，1 最高）
- 供需错配分析：痛点高但收入低 = 机会？还是痛点高但付费意愿低 = 伪需求？

## 输出格式

文件：`~/产品分析/YYYY-MM-DD-{主题}.md`

```yaml
---
date: YYYY-MM-DD
pattern: 使用的规律名称
source_A: 来源
source_B: 来源
source_C: 来源
theme: 主题关键词
tags: [产品分析, ...]
---
```

文件末尾必须包含**已分析产品清单**表格（跨 session 累积）：

```markdown
## 已分析产品清单

| # | 日期 | 产品 | 来源 | MRR 估算 |
|---|------|------|------|----------|
```

## 执行步骤

1. **回忆历史**：读取 `~/产品分析/` 下所有文件，提取已分析产品清单
2. **抓取数据**：
   - **TrustMRR**：用 Hermes browser（无防护）
   - **Toolify.ai**：用 `mcp_chrome_devtools_new_page` + `mcp_chrome_devtools_take_snapshot`（Cloudflare 防护）
   - **TAAFT**：首页用 Hermes browser；详情页用 DevTools MCP
   - 用 `delegate_task` 并行抓取多个来源
3. **选品**：按规律选出 3 个产品，说明逻辑
4. **深度分析**：对每个产品补充信息（官网/搜索），执行 8 步分析。产品官网如有 Cloudflare 防护，也用 DevTools MCP
5. **写入文件**：完整 Markdown + YAML frontmatter
6. **汇总**：更新已分析产品清单

## 数据源访问方案

### Cloudflare 防护站点 → Chrome DevTools MCP（headed 模式）

Toolify.ai 和 TAAFT 部分页面有 Cloudflare Turnstile 防护。**Hermes 内置 browser（headless）会被拦截**，需要用 Chrome DevTools MCP 的 headed 模式绕过。

**操作流程：**
1. 用 `mcp_chrome_devtools_new_page` 打开目标 URL
2. 用 `mcp_chrome_devtools_take_snapshot` 获取页面内容（带 uid）
3. 用 `mcp_chrome_devtools_click` / `mcp_chrome_devtools_fill` 交互
4. 用 `mcp_chrome_devtools_evaluate_script` 提取结构化数据（比 snapshot 更可靠）

**为什么有效：** Headed 模式启动真实 Chrome 窗口，有完整渲染管线（WebGL、GPU、鼠标轨迹），Turnstile 无法区分自动化和正常用户。HeadlessChrome 的 UA 会被直接拒绝。

**配置前提：** `~/.hermes/config.yaml` 中 `mcp_servers.chrome-devtools` 已配置（`npx -y chrome-devtools-mcp@latest --isolated`，**不加 `--headless`**）。

### 无防护站点 → Hermes browser / delegate_task

TrustMRR 等无 Cloudflare 防护的站点，直接用 Hermes 内置 browser 或 `delegate_task` 抓取。

## Pitfalls（踩过的坑）

### 数据源访问问题
- **Toolify.ai**：用 Chrome DevTools MCP（headed 模式）即可正常访问，2026-04-30 已验证成功
- **TAAFT 详情页** (`/ai/{name}`)：被 Cloudflare 拦截时，同样用 DevTools MCP
- **TrustMRR**：直接访问即可，无需特殊处理
- **产品官网** 可能加载超时（尤其是新站），不要死等，用已有数据+搜索补充
- **搜索引擎**（Google/Bing/DuckDuckGo）可能返回 JS 渲染页面或空结果

### 推荐：用 delegate_task 并行抓取
- 每个来源分配一个子任务并行抓取，节省时间
- **Cloudflare 防护站点**（Toolify/TAAFT详情页）：子任务中用 `mcp_chrome_devtools_*` 工具
- **无防护站点**（TrustMRR/TAAFT首页）：子任务中用 Hermes browser
- 用 `mcp_chrome_devtools_evaluate_script` 提取结构化数据比 `mcp_chrome_devtools_take_snapshot` 更可靠
- 设置合理的 timeout，避免单个来源卡住整个流程

### ⚠️ 效率与 Token 控制（2026-04-30 实测）
- **TrustMRR scraping 很慢**：delegate_task 搜索/浏览 TrustMRR 耗时 326s、50 次 API 调用、1.5M input tokens，最终还 hit max_iterations。**对策**：给子任务明确指定"只看 Feed 前 20 个产品"或"直接导航到某个分类页面"，不要让 agent 自己探索
- **三源并行总耗时约 10 分钟**（TrustMRR 326s + Toolify 105s + TAAFT 224s），产品调研再 346s。整条流水线约 15-20 分钟
- **Token 消耗大**：单次完整分析消耗约 2-3M input tokens（主力模型 glm-5.1 成本低所以可接受）
- **TrustMRR 的分类页面和 Top 100 链接经常 404**，搜索下拉框只返回 10 条且无法筛选 MRR 上限——直接用 Feed 页面更稳

### Obsidian Vault
- Bruce 的机器上**未找到** Obsidian vault（2026-04-30 确认）
- 当前输出到 `~/产品分析/` 目录，纯 Markdown 文件
- 如果后续配置了 Obsidian，需要迁移文件到 vault 内

### 搜索工具降级策略（实测踩坑 2026-04）

搜索用户评论和竞品信息时，工具可能大面积失败：
1. **Tavily API** → 可能 429 (Insufficient balance)
2. **Google Search** → headless browser 被检测返回 CAPTCHA
3. **Bing (Hermes browser)** → 可能重定向 cn.bing.com，结果解析不到
4. **ProductHunt / G2** → Cloudflare Turnstile 防护

**推荐搜索顺序**：
1. Chrome DevTools MCP 访问 Bing（`ensearch=1`）+ `evaluate_script`
2. Chrome DevTools MCP 直接访问评价站点（Goodfirms、opentools.ai、SaaSBrowser）
3. Hermes browser 访问 DuckDuckGo HTML 版（`html.duckduckgo.com`）
4. 都失败 → 基于已有数据推理，标注"未找到真实评论"

### 报告字数
- 8步框架 + 7项附加，三产品实际约3500-4500字
- 单产品控制在1000-1200字（Step 1-8 约600字 + A1-A6 约400-500字）
- 总体控制在 4000 字以内

## 已分析产品索引

此 section 由 agent 在每次分析后更新。

| # | 日期 | 产品 | 来源 | MRR |
|---|------|------|------|-----|
| 1 | 2026-04-30 | Tokscript | TrustMRR | $7,101 |
| 2 | 2026-04-30 | Blotato | TAAFT | $4K-$37.5K |
| 3 | 2026-04-30 | Docsio | TAAFT | $9K-$60K |
| 4 | 2026-04-30 | Presscart | TrustMRR | $12,989 |
| 5 | 2026-04-30 | Mailmodo AI | Toolify.ai | $40K-$96K |
| 6 | 2026-04-30 | Watermelon | TAAFT | $44K-$123K |
