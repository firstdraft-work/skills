---
name: daily-product-analysis
version: 2.0.0
description: 每日产品分析教练 — 从 TrustMRR + Toolify.ai + There's An AI For That 三源选品，8步框架+7项需求嗅觉训练，深度分析3个关联产品。
triggers:
  - 产品分析
  - 分析产品
  - 产品教练
  - daily product
  - 今天分析
  - 选品分析
---

# 每日产品分析教练

训练产品嗅觉和需求判断力。每次从三个来源选 3 个有逻辑关联的产品，执行 8 步分析框架 + 7 项需求嗅觉训练。

## Agent 兼容性

本技能设计为跨 Agent 通用。根据你使用的 Agent 框架，调整工具调用方式：

| 能力 | Claude Code | OpenCode | Codex | Hermes/OpenClaw |
|------|------------|----------|-------|-----------------|
| 网页抓取 | `WebFetch` / Playwright MCP | 内置 browser | 内置 web | `browser_navigate` |
| 搜索 | `web_search` / Tavily | 内置 search | 内置 search | `web_search` |
| 文件读写 | 内置 file tools | 内置 file | 内置 file | `write_file` / `read_file` |
| 并行任务 | `Task` tool | 内置 delegate | 内置 delegate | `delegate_task` |
| Cloudflare 绕过 | Chrome DevTools MCP | Chrome DevTools MCP | 无（降级搜索） | Chrome DevTools MCP |

## 核心约束

- **不重复**：每次分析前回顾已分析产品清单
- **三源结合**：必须从 TrustMRR / Toolify.ai / TAAFT 中至少 2 个来源选品
- **逻辑关联**：3 个产品之间必须有明确的对比/替代/纵向关系
- **4000 字以内**（8步框架+7项附加，单产品约1000-1200字）
- **输出为 Markdown + YAML frontmatter**
- **Obsidian 兼容格式**

## 三个数据来源

| 来源 | URL | 价值 | 注意事项 |
|------|-----|------|----------|
| **TrustMRR** | https://trustmrr.com | 已验证 MRR 数据，真实标杆 | 无 Cloudflare 防护，可直接抓取。详情页 `/startup/{name}` 有收入图表、定价、技术栈 |
| **Toolify.ai** | https://www.toolify.ai/zh/ | AI 工具目录，按类别发现 | ⚠️ **Cloudflare Turnstile 防护**，headless browser 会被拦截。需要 headed browser（如 Chrome DevTools MCP 不加 `--headless`）|
| **There's An AI For That** | https://theresanaiforthat.com | 按任务反向找 AI 工具 | 首页可抓取 trending + 最新工具。详情页 `/ai/{name}` 可能被 Cloudflare 拦截 |

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

### A1：用户原声
引用 1-2 条真实用户评论/抱怨原话及来源（如 Product Hunt、Reddit、G2、Twitter）。用搜索引擎查找。没有真实评论则标注"未找到真实原声"并写一句推测的用户抱怨。

### A2：痛点量化
- **时间成本**：用户每周花多少小时在这问题上？
- **金钱成本**：替代方案（没有这个产品时）花费多少？
- **情绪成本**：1-10 级 + 原因

### A3：需求风险
- 高频/低频？使用频率
- 刚需/痒点？没了它用户会怎样
- 是否可能被**平台方**消灭？
- 是否可能被**技术迭代**消灭？

### A4：价格锚点
- 用户不买这个产品会花多少钱解决问题？
- 同类非 AI 工具定价是多少？

### A5：最小验证方法
不写代码的情况下，如何用 **24 小时**验证这个需求有人愿意付费？具体到操作步骤。

### A6：定制盲区
针对**个人开发者/独立开发者**，指出会在这个产品上犯的**具体工程决策错误**。关注个人开发者的典型陷阱：过度工程化、忽略BD/运营、一个人想做全平台等。

### A7：需求-收入关联（最终总结中完成）
对比本次三个产品：**哪个需求更痛但收入更低？为什么？**
- 需求痛点排序（1→3，1 最痛）
- 收入排序（1→3，1 最高）
- 供需错配分析

## 输出格式

文件：`~/产品分析/YYYY-MM-DD-{主题}.md`（或用户指定目录）

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

文件末尾必须包含**已分析产品清单**表格（跨 session 累积）。

## 执行步骤

1. **回忆历史**：读取输出目录下所有文件，提取已分析产品清单
2. **抓取数据**（并行）：
   - **TrustMRR**：直接用 browser 抓取（无 Cloudflare 防护）
   - **Toolify.ai**：用 headed browser（Chrome DevTools MCP 或等效工具）
   - **TAAFT**：首页直接抓取；详情页用 headed browser
3. **选品**：按规律选出 3 个产品，说明逻辑
4. **深度分析**：对每个产品补充信息（官网/搜索），执行 8 步分析 + 7 项附加
5. **写入文件**：完整 Markdown + YAML frontmatter
6. **汇总**：更新已分析产品清单

## 数据源访问方案

### Cloudflare 防护站点

Toolify.ai 和 TAAFT 部分页面有 Cloudflare Turnstile 防护。**Headless browser 会被拦截**（UA 含 `HeadlessChrome` 被直接拒绝）。

**解决方案**：
- **Chrome DevTools MCP**（Hermes/OpenClaw/Claude Code）：`npx -y chrome-devtools-mcp@latest --isolated`，**不加 `--headless`**
- **Playwright headed mode**（通用）：`chromium.launch(headless=False)`
- **手动降级**：如果无法使用 headed browser，用搜索引擎 `site:toolify.ai {关键词}` 替代

### 无防护站点

TrustMRR 等无 Cloudflare 防护的站点，直接用任何 browser 工具抓取。

## Pitfalls（踩过的坑）

### 搜索引擎问题
- **Google Search**：headless browser 会被检测为机器人返回 CAPTCHA，不要用来搜 Google
- **Bing**：可能重定向到 cn.bing.com，加 `&ensearch=1` 获取国际版结果
- **ProductHunt / G2**：有 Cloudflare/DataDome 防护，用 headed browser 或放弃

### 效率控制
- TrustMRR scraping 较慢，给子任务明确指令（"只看 Feed 前 20 个产品"），不要让 agent 自由探索
- 三源并行总耗时约 5-10 分钟，完整流水线约 15-20 分钟
- 搜索工具可能大面积失败，准备降级方案

### 搜索工具降级策略

1. Headed browser 访问 Bing（`ensearch=1`）
2. Headed browser 直接访问评价站点（Goodfirms、opentools.ai、SaaSBrowser）
3. DuckDuckGo HTML 版（`html.duckduckgo.com`）
4. 都失败 → 基于已有数据推理，标注"未找到真实评论"

## 已分析产品索引

此 section 由 agent 在每次分析后更新。初始为空，安装后根据本地分析记录自动累积。

| # | 日期 | 产品 | 来源 | MRR |
|---|------|------|------|-----|
