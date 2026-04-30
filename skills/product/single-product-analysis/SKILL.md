---
name: single-product-analysis
version: 2.0.0
description: 输入产品 URL，自动抓取信息并输出完整的 8 步深度分析 + 7 项需求嗅觉训练报告。
triggers:
  - 分析这个产品
  - 产品URL分析
  - 看看这个产品
  - analyze this product
  - single product
---

# 单产品深度分析

用户输入一个产品 URL，自动抓取产品信息，执行 8 步分析框架 + 7 项需求嗅觉训练，输出完整分析报告。

## Agent 兼容性

本技能设计为跨 Agent 通用。根据你使用的 Agent 框架，调整工具调用方式：

| 能力 | Claude Code | OpenCode | Codex | Hermes/OpenClaw |
|------|------------|----------|-------|-----------------|
| 网页抓取 | `WebFetch` / Playwright MCP | 内置 browser | 内置 web | `browser_navigate` |
| 搜索 | `web_search` / Tavily | 内置 search | 内置 search | `web_search` |
| 文件读写 | 内置 file tools | 内置 file | 内置 file | `write_file` / `read_file` |
| Cloudflare 绕过 | Chrome DevTools MCP | Chrome DevTools MCP | 无（降级搜索） | Chrome DevTools MCP |

## 输入

用户提供的任意格式，必须包含产品 URL。可能是：
- 单个 URL：`https://example.com`
- URL + 补充说明：`看看这个 https://example.com，是个做XX的`
- 产品名称（需要搜索找到URL）

## 执行流程

### 第一步：识别产品

1. 从用户输入中提取 URL
2. 如果只有产品名没有 URL，用搜索找到官网
3. 确认产品名称和官网地址

### 第二步：抓取产品信息（并行）

同时获取以下信息：

1. **官网**：访问产品官网，提取功能、定价、目标用户
   - 有 Cloudflare 防护 → 用 headed browser（Chrome DevTools MCP 或等效）
   - 无防护 → 直接用 browser

2. **TrustMRR 数据**：搜索 `site:trustmrr.com {产品名}`，看是否有 MRR 数据

3. **用户评论**：搜索以下关键词（并行）：
   - `{产品名} review site:reddit.com`
   - `{产品名} review site:producthunt.com`
   - `{产品名} review site:g2.com`
   - `{产品名} vs {竞品名}`

4. **竞品信息**：搜索同类产品定价，用于价格锚点分析

### 第三步：执行分析

对产品执行以下 **8 步框架 + 7 项附加**，每项必须包含具体数据和推理，禁止空话。

## 8 步分析框架

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
- 如果 TrustMRR 有数据，以 TrustMRR 为基准校准

### Step 5：技术实现路径
前端形态、后端核心、存储方案、AI 用法、最棘手的 2 个技术难点

### Step 6：增长方式（重点）
主要流量来源、为什么能获取流量、最值得复制的 1 个增长动作

### Step 7：对我的启发（必须具体）
- 最值得抄的 1 个点（思路不是代码）
- 我可以快速做一个什么类似产品？（名字+场景+一句话，不限技术栈）

### Step 8：程序员思维盲区
一句话戳破思维误区

## 7 项附加：需求嗅觉训练

### A1：用户原声
引用 1-2 条真实用户评论/抱怨原话及来源。用搜索引擎查找。没有真实评论则标注"未找到真实原声"并写一句推测的用户抱怨。

### A2：痛点量化
- **时间成本**：用户每周花多少小时在这问题上？
- **金钱成本**：替代方案花费多少？
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

### A7：需求机会评分
对这个产品做最终评分：
- **需求强度**：1-10（1=没人需要，10=不解决就活不下去）
- **市场大小**：1-10（1=极小众，10=人人需要）
- **竞争壁垒**：1-10（1=谁都能抄，10=有网络效应/数据壁垒）
- **个人开发者可行性**：1-10（1=需要大团队，10=一个人3个月能做出MVP）
- **综合推荐**：做/不做/观望，附理由

## 输出格式

### 交互式输出

分析完成后，先在聊天中给用户一个简洁摘要：
- 产品名 + 一句话定位
- 收入估算范围
- 最值得关注的 1 个洞察
- 需求机会评分
- A7 综合推荐

### 文件输出

如果用户要求保存，或分析内容较长，写入文件：

```yaml
---
date: YYYY-MM-DD
product: 产品名
url: 产品官网
pricing: 定价信息
mrr_estimate: 收入估算范围
demand_score: X/10
market_score: X/10
moat_score: X/10
solo_dev_score: X/10
recommendation: 做/不做/观望
tags: [产品分析, single, ...]
---
```

## 数据源访问方案

### Cloudflare 防护站点

部分产品官网有 Cloudflare Turnstile 防护。**Headless browser 会被拦截**。

**解决方案**：
- **Chrome DevTools MCP**：`npx -y chrome-devtools-mcp@latest --isolated`，不加 `--headless`
- **Playwright headed mode**：`chromium.launch(headless=False)`
- **降级**：搜索引擎 `site:{域名} {关键词}` 替代

### 无防护站点

大部分产品官网可以直接用 browser 访问。

## Pitfalls

- **产品官网可能加载慢**：设置合理 timeout（30-60s），不要死等
- **搜索评论可能找不到**：用多种来源（Reddit/G2/ProductHunt/Twitter），都找不到就诚实标注
- **定价信息可能隐藏**：有些产品需要登录才能看价格，用搜索补充
- **不要编造数据**：没有的数据标注"未找到"或"推测"，附上推理依据
- **TrustMRR 不一定有数据**：只覆盖一部分产品，没有就跳过
- **综合评分要诚实**：不要每个产品都给高分，烂产品就直说烂
- **搜索降级策略**：Google 被 CAPTCHA → 用 Bing（加 `ensearch=1`）→ Goodfirms/opentools.ai → DuckDuckGo HTML → 基于已有数据推理
