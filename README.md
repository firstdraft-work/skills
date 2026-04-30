# Product Analysis Skills

通用产品分析技能包，支持多种 AI Agent 框架。

## 支持的 Agent

| Agent | 安装方式 |
|-------|---------|
| **Hermes / OpenClaw** | 复制 `skills/` 目录到 `~/.hermes/skills/` |
| **Claude Code** | 复制到项目 `.claude/skills/` 或通过 `CLAUDE.md` 引用 |
| **OpenCode** | 复制到 `~/.opencode/skills/` 或项目 `.opencode/skills/` |
| **Codex** | 在 `AGENTS.md` 或 `codex.md` 中引用指令内容 |
| **Cursor / Windsurf** | 在 `.cursorrules` 或 `.windsurfrules` 中引用 |

## Skills

### [daily-product-analysis](skills/product/daily-product-analysis/)

**每日产品分析教练** — 从 TrustMRR + Toolify.ai + There's An AI For That 三源选品，8步框架 + 7项需求嗅觉训练，深度分析3个关联产品。

- 三种选品规律轮换（锚点对比/收入验证+AI替代/纵向挖掘）
- 8步分析框架 + 7项附加训练（用户原声/痛点量化/需求风险/价格锚点/最小验证/定制盲区/需求-收入关联）
- Cloudflare 防护站点解决方案
- 可配置定时任务每日自动执行

### [single-product-analysis](skills/product/single-product-analysis/)

**单产品深度分析** — 输入产品 URL，自动抓取信息并输出完整的 8 步分析 + 7 项需求嗅觉训练报告。

- 支持任意产品 URL 输入
- 自动并行抓取官网/评论/竞品信息
- 5维需求机会评分（需求强度/市场大小/竞争壁垒/个人开发者可行性/综合推荐）
- 输出 Markdown 报告含 YAML frontmatter

## Examples

[examples/](examples/) 目录包含真实分析报告样例：

| 文件 | 类型 | 产品 | 说明 |
|------|------|------|------|
| `2026-04-30-短视频内容工具链.md` | daily（规律1） | Tokscript / Blotato / Docsio | 锚点对比法 |
| `2026-04-30-营销获客全链路.md` | daily（规律2） | Presscart / Mailmodo / Watermelon | 收入验证+AI替代 |
| `magic-omagic-ai.md` | single | Magic (omagic.ai) | AI产品视频生成 |

## 快速开始

### Hermes / OpenClaw

```bash
git clone https://github.com/firstdraft-work/product-analysis-skills.git
cp -r product-analysis-skills/skills/product ~/.hermes/skills/
```

### Claude Code

```bash
# 方式1：放入项目级 skills 目录
mkdir -p .claude/skills
cp -r product-analysis-skills/skills/product .claude/skills/

# 方式2：在 CLAUDE.md 中添加引用
echo "加载产品分析技能时，读取 skills/product/daily-product-analysis/SKILL.md 或 skills/product/single-product-analysis/SKILL.md" >> CLAUDE.md
```

### OpenCode

```bash
mkdir -p ~/.opencode/skills
cp -r product-analysis-skills/skills/product ~/.opencode/skills/
```

### Codex

```bash
# 将 SKILL.md 内容追加到 AGENTS.md 或 codex.md
cat skills/product/daily-product-analysis/SKILL.md >> AGENTS.md
cat skills/product/single-product-analysis/SKILL.md >> AGENTS.md
```

### Cursor / Windsurf

```bash
# Cursor
cat skills/product/daily-product-analysis/SKILL.md >> .cursorrules
cat skills/product/single-product-analysis/SKILL.md >> .cursorrules

# Windsurf
cat skills/product/daily-product-analysis/SKILL.md >> .windsurfrules
cat skills/product/single-product-analysis/SKILL.md >> .windsurfrules
```

## 分析框架

### 8 步分析（每个产品）
1. 产品定位与体验
2. 问题与价值
3. 商业模式拆解
4. 收入估算（公式推导）
5. 技术实现路径
6. 增长方式
7. 对我的启发
8. 程序员思维盲区

### 7 项需求嗅觉训练
- **A1** 用户原声（真实评论引用）
- **A2** 痛点量化（时间/金钱/情绪）
- **A3** 需求风险（频率/刚需度/平台威胁）
- **A4** 价格锚点（替代方案花费）
- **A5** 最小验证方法（24小时无代码验证）
- **A6** 定制盲区（个人开发者典型错误）
- **A7** 需求-收入关联 / 需求机会评分

## 数据源

| 来源 | URL | 说明 |
|------|-----|------|
| TrustMRR | https://trustmrr.com | 已验证 MRR 数据，无防护 |
| Toolify.ai | https://www.toolify.ai/zh/ | AI 工具目录，需 headed browser |
| There's An AI For That | https://theresanaiforthat.com | AI 工具按任务分类 |

## License

MIT
