# Product Analysis Skills

通用产品分析技能包，用于训练产品嗅觉和需求判断力。适用于任意 AI Agent 框架。

## 所需能力

使用本技能前，请确保你的 Agent 具备以下能力（缺少则需安装对应工具/插件）：

| 能力 | 用途 | 替代方案 |
|------|------|----------|
| **网页浏览/抓取** | 访问产品官网、数据源站点 | curl、Playwright、Puppeteer 等 |
| **搜索引擎** | 搜索产品评论、竞品、定价 | 任意 search API 或浏览器搜索 |
| **Cloudflare 绕过** | 部分站点有 Turnstile 防护 | headed 浏览器（非 headless）、专用 MCP server |
| **文件写入** | 输出 Markdown 分析报告 | 任意本地文件操作能力 |
| **并行任务执行** | 同时抓取多个数据源（可选） | 串行执行，速度较慢 |

> ⚠️ **Cloudflare 防护提示**：Toolify.ai、TAAFT 部分页面有 Cloudflare Turnstile 防护。headless 浏览器会被拦截，需要使用 headed 模式（真实浏览器窗口）或专门的绕过工具。

## Skills

### [daily-product-analysis](product/daily-product-analysis/)

**每日产品分析教练** — 从 TrustMRR + Toolify.ai + There's An AI For That 三源选品，8步框架 + 7项需求嗅觉训练，深度分析3个关联产品。

- 三种选品规律轮换（锚点对比/收入验证+AI替代/纵向挖掘）
- 8步分析框架（定位→价值→商业模式→收入估算→技术路径→增长→启发→盲区）
- 7项附加训练（用户原声/痛点量化/需求风险/价格锚点/最小验证/定制盲区/需求-收入关联）
- 支持 Cron 定时每日自动执行

### [single-product-analysis](product/single-product-analysis/)

**单产品深度分析** — 输入产品 URL，自动抓取信息并输出完整的 8 步分析 + 7 项需求嗅觉训练报告。

- 支持任意产品 URL 输入
- 自动并行抓取官网/评论/竞品信息
- 5维需求机会评分（需求强度/市场大小/竞争壁垒/个人开发者可行性/综合推荐）
- 输出 Markdown 报告含 YAML frontmatter

## 安装

将 `product/` 目录复制到你的 Agent skills 目录：

```bash
# 示例：Hermes Agent
cp -r product/ ~/.hermes/skills/

# 示例：自定义目录
cp -r product/ /path/to/your/agent/skills/
```

## 目录结构

```
product/
├── daily-product-analysis/
│   ├── SKILL.md                          # 技能主文件
│   ├── templates/
│   │   └── daily-analysis.md             # 每日分析报告模板
│   └── references/
│       └── data-source-access.md         # 数据源访问指南
└── single-product-analysis/
    ├── SKILL.md                          # 技能主文件
    └── templates/
        └── single-analysis.md            # 单产品分析报告模板
```

## 数据源

| 来源 | URL | 说明 |
|------|-----|------|
| TrustMRR | https://trustmrr.com | 已验证 MRR 数据，收入标杆 |
| Toolify.ai | https://www.toolify.ai/zh/ | AI 工具目录（⚠️ Cloudflare 防护） |
| There's An AI For That | https://theresanaiforthat.com | AI 工具按任务分类（⚠️ 部分页面有防护） |

## 许可

MIT
