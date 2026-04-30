# 数据源访问指南

> 访问 TrustMRR、Toolify.ai、TAAFT 的实用笔记。

## 所需能力

- **网页浏览/抓取**：访问各数据源站点
- **Headed 浏览器**（非 headless）：用于 Cloudflare 防护站点
- **搜索引擎**：补充数据验证

如缺少某项能力，请先安装对应工具。

---

## Cloudflare 防护站点 → Headed 浏览器模式

**适用站点：** Toolify.ai、TAAFT 详情页

### 为什么 headless 浏览器不行？
- Headless 浏览器 UA 包含 `HeadlessChrome/xxx`
- Cloudflare Turnstile 检测 headless 指纹（WebGL、GPU、鼠标轨迹等），直接拒绝
- 表现为：显示"正在进行安全验证"页面，无限转圈

### 解决方案：Headed 浏览器

**操作流程**：
1. 启动真实 Chrome/Chromium 浏览器窗口（非 headless）
2. 导航到目标 URL
3. 等待 Cloudflare 验证通过（通常 1-3 秒）
4. 获取页面内容（快照或 DOM 解析）

**为什么有效**：
- Headed 模式启动真实浏览器窗口（会弹出到前台）
- 完整渲染管线，Turnstile 无法区分自动化和正常用户

**注意事项**：
- 需要桌面环境（有显示器），服务器环境不适用
- 可以通过 Chrome DevTools Protocol (CDP) 或 Playwright/Puppeteer 的 headed 模式实现
- 完成抓取后记得关闭标签页释放资源

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

## Toolify.ai（✅ 需要 Headed 浏览器）

### 访问方式
- **首页**: `https://www.toolify.ai/zh/` — headed 浏览器可直接访问
- **分类页**: `https://www.toolify.ai/zh/category/{slug}` — 同上
- **工具详情**: `https://www.toolify.ai/zh/{tool-slug}` — 同上

### 数据提取
- 首页显示 AI 工具总数 + 分类总数
- 分类页按热门/最新排序
- 工具详情页包含：描述、定价、功能、替代品、评论

---

## There's An AI For That（⚠️ 部分需要 Headed 浏览器）

### 可直接访问（普通浏览器即可）
- **首页**: `https://theresanaiforthat.com` → 可直接抓取
  - Trending 工具（带 #N in Trending 标签）
  - 最新发布工具（Just released 区块）
  - 高收藏数工具
- 每个工具卡片包含：名称、描述、分类标签、收藏数

### 需要 Headed 浏览器
- **Trending 页**: `/trending` — 被 Cloudflare 拦截
- **详情页**: `/ai/{name}` — 被 Cloudflare 拦截
- **Leaderboard**: `/leaderboard` — 被 Cloudflare 拦截

### 提取技巧
- 首页内容足够获取热门工具列表（用于选品）
- 通过收藏数（saves）判断工具受欢迎程度
- 详情页需要时用 headed 浏览器

---

## 通用建议

1. **并行抓取**：如支持并行任务执行，同时从多个来源抓取，节省时间
2. **Headed 浏览器优先**：对已知有 Cloudflare 防护的站点，直接用 headed 浏览器，不要先试 headless 再降级
3. **超时控制**：每个来源设置 60s timeout，避免卡住
4. **数据验证**：TrustMRR 数据最可靠（API 验证），其他来源数据标注「推测」
