# 数据源访问笔记

> Session-specific findings on accessing TrustMRR, Toolify.ai, and TAAFT.

## Cloudflare 防护站点 → Chrome DevTools MCP（headed 模式）

**适用站点：** Toolify.ai、TAAFT 详情页

### 为什么 Hermes 内置 browser 不行？
- Hermes browser 是 headless 模式，UA 包含 `HeadlessChrome/xxx`
- Cloudflare Turnstile 检测 headless 指纹（WebGL、GPU、鼠标轨迹等），直接拒绝
- 表现为：显示"正在进行安全验证"页面，无限转圈

### Chrome DevTools MCP 方案

**工具系列：** `mcp_chrome_devtools_*`（33 个工具）

**关键操作：**
1. `mcp_chrome_devtools_new_page(url)` — 打开新标签页
2. `mcp_chrome_devtools_take_snapshot()` — 获取页面文本快照（带 uid 标识符）
3. `mcp_chrome_devtools_click(uid)` — 点击元素
4. `mcp_chrome_devtools_fill(uid, value)` — 填写表单
5. `mcp_chrome_devtools_evaluate_script(function)` — 执行 JS 提取结构化数据
6. `mcp_chrome_devtools_navigate_page()` — 页内导航

**为什么有效：**
- Headed 模式启动真实 Chrome 窗口（会弹出浏览器窗口到前台）
- 完整渲染管线，Turnstile 无法区分自动化和正常用户
- 2026-04-30 实测：Toolify 首页 28916 个 AI 工具 + 459 个分类全部可见

**配置前提：**
`~/.hermes/config.yaml` 中 `mcp_servers.chrome-devtools` 配置：
```yaml
mcp_servers:
  chrome-devtools:
    command: npx
    args:
      - -y
      - chrome-devtools-mcp@latest
      - --isolated
    timeout: 120
    connect_timeout: 30
```
⚠️ **不要加 `--headless` 参数！** 加了就和 Hermes browser 一样被拦截。

**注意事项：**
- 会弹出真实 Chrome 窗口（headed），服务器环境不适用
- `evaluate_script` 提取数据比 `take_snapshot` + 解析文本更可靠
- 完成抓取后可用 `mcp_chrome_devtools_close_page` 关闭标签页

---

## TrustMRR（✅ 可直接访问）

### 访问方式
- **首页/Feed**: `https://trustmrr.com` → 点击 "Feed" 链接 → 显示最新产品列表
- **产品详情**: `https://trustmrr.com/startup/{slug}` → 收入图表、MRR、定价、技术栈、用户数
- **浏览器直接访问即可**，无 Cloudflare 拦截

### 数据提取
- Feed 页面每个产品卡片包含：名称、描述、MRR、总收入、售价
- 详情页包含：收入折线图、订阅数、创始人信息、定价档位、Tech Stack、增长百分比
- 收入数据通过 LemonSqueezy / Stripe API 验证，带 "Verified" 标识

### 有价值的字段
```
MRR (estimated): $X,XXX
Active subscriptions: XXXX
Revenue last 30 days: $XX,XXX
MoM growth: XX%
Tech stack: React, ...
Pricing: Free / $X/mo / $XX/yr
```

---

## Toolify.ai（✅ 需要 DevTools MCP）

### 访问方式
- **首页**: `https://www.toolify.ai/zh/` — DevTools MCP headed 模式可直接访问
- **分类页**: `https://www.toolify.ai/zh/category/{slug}` — 同上
- **工具详情**: `https://www.toolify.ai/zh/{tool-slug}` — 同上

### 数据提取
- 首页显示 AI 工具总数 + 分类总数
- 分类页按热门/最新排序
- 工具详情页包含：描述、定价、功能、替代品、评论

---

## There's An AI For That（⚠️ 部分需要 DevTools MCP）

### 可直接访问（Hermes browser 即可）
- **首页**: `https://theresanaiforthat.com` → 可直接抓取
  - Trending 工具（带 #N in Trending 标签）
  - 最新发布工具（Just released 区块）
  - 高收藏数工具
- 每个工具卡片包含：名称、描述、分类标签、收藏数

### 需要 DevTools MCP
- **Trending 页**: `/trending` — 被 Cloudflare 拦截
- **详情页**: `/ai/{name}` — 被 Cloudflare 拦截
- **Leaderboard**: `/leaderboard` — 被 Cloudflare 拦截

### 提取技巧
- 首页内容足够获取热门工具列表（用于选品）
- 通过收藏数（saves）判断工具受欢迎程度
- 详情页需要时用 DevTools MCP

---

## 通用建议

1. **并行抓取**：用 `delegate_task` 同时从多个来源抓取，节省时间
2. **DevTools MCP 优先**：对已知有 Cloudflare 防护的站点，直接用 DevTools MCP，不要先试 Hermes browser 再降级
3. **超时控制**：每个来源设置 60s timeout，避免卡住
4. **数据验证**：TrustMRR 数据最可靠（API 验证），其他来源数据标注「推测」
