# Product Analysis Skills

两个产品分析技能，用于训练产品嗅觉和需求判断力。

## Skills

### [daily-product-analysis](product/daily-product-analysis/)

**每日产品分析教练** — 从 TrustMRR + Toolify.ai + There's An AI For That 三源选品，8步框架 + 7项需求嗅觉训练，深度分析3个关联产品。

- 三种选品规律轮换（锚点对比/收入验证+AI替代/纵向挖掘）
- 8步分析框架（定位→价值→商业模式→收入估算→技术路径→增长→启发→盲区）
- 7项附加训练（用户原声/痛点量化/需求风险/价格锚点/最小验证/定制盲区/需求-收入关联）
- 支持 Chrome DevTools MCP 绕过 Cloudflare 防护
- 可配置 Cron 每日自动执行

### [single-product-analysis](product/single-product-analysis/)

**单产品深度分析** — 输入产品 URL，自动抓取信息并输出完整的 8 步分析 + 7 项需求嗅觉训练报告。

- 支持任意产品 URL 输入
- 自动并行抓取官网/评论/竞品信息
- 5维需求机会评分（需求强度/市场大小/竞争壁垒/个人开发者可行性/综合推荐）
- 输出 Markdown 报告含 YAML frontmatter

## 安装

将 `product/` 目录复制到你的 Hermes skills 目录：

```bash
cp -r product/ ~/.hermes/skills/
```

## 数据源

| 来源 | URL | 说明 |
|------|-----|------|
| TrustMRR | https://trustmrr.com | 已验证 MRR 数据 |
| Toolify.ai | https://www.toolify.ai/zh/ | AI 工具目录（需 DevTools MCP） |
| There's An AI For That | https://theresanaiforthat.com | AI 工具按任务分类 |
