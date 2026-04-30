# 数据源访问笔记

## Cloudflare 防护站点 → Headed Browser

**适用站点：** Toolify.ai、TAAFT 详情页

### 为什么 headless browser 不行？
- Headless browser 的 UA 包含 `HeadlessChrome/xxx`
- Cloudflare Turnstile 检测 headless 指纹（WebGL、GPU、鼠标轨迹等），直接拒绝
- 表现为：显示"正在进行安全验证"页面，无限转圈

### 解决方案

**方案1：Chrome DevTools MCP（推荐）**
```bash
# 安装
npx -y chrome-devtools-mcp@latest --isolated
# ⚠️ 不要加 --headless 参数！
```
- 启动真实 Chrome 窗口（headed），完整渲染管线
- 通过 CDP (Chrome DevTools Protocol) 控制浏览器
- 工具：`new_page`、`take_snapshot`、`click`、`fill`、`evaluate_script`

**方案2：Playwright headed mode**
```python
from playwright.sync_api import sync_playwright
with sync_playwright() as p:
    browser = p.chromium.launch(headless=False)  # 关键：headless=False
    page = browser.new_page()
    page.goto("https://www.toolify.ai/zh/")
    content = page.content()
```

**方案3：手动降级**
- 搜索引擎 `site:toolify.ai {关键词}` 替代直接访问
- 用第三方评价站点（Goodfirms、opentools.ai）获取信息

---

## TrustMRR（✅ 可直接访问）

### 访问方式
- **首页/Feed**: `https://trustmrr.com` → 点击 "Feed" → 最新产品列表
- **产品详情**: `https://trustmrr.com/startup/{slug}` → 收入图表、MRR、定价、技术栈
- 无 Cloudflare 拦截，任何 browser 都可访问

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

## Toolify.ai（⚠️ 需要 Headed Browser）

- 首页：28,000+ AI 工具，459 个分类
- 用 headed browser 可正常访问
- 分类页、工具详情页均需 headed browser
- Headless browser 100% 被 Turnstile 拦截

---

## There's An AI For That（⚠️ 部分需要 Headed Browser）

### 可直接访问
- **首页**：trending + 最新发布工具，每个工具含名称、描述、收藏数

### 需要 Headed Browser
- `/trending` — 被 Cloudflare 拦截
- `/ai/{name}` — 详情页可能被拦截
- `/leaderboard` — 被 Cloudflare 拦截

---

## 通用建议

1. **并行抓取**：多个来源同时抓取，节省时间
2. **Headed browser 优先**：对已知有 Cloudflare 防护的站点，直接用 headed browser
3. **超时控制**：每个来源设置 30-60s timeout
4. **数据验证**：TrustMRR 数据最可靠（API 验证），其他来源数据标注「推测」
5. **搜索降级链**：Google → Bing(ensearch=1) → Goodfirms/opentools → DuckDuckGo HTML → 推理
