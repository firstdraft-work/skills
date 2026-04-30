---
date: "{{DATE}}"
pattern: "{{PATTERN_NAME}}"
source_A: "{{SOURCE_A}}"
source_B: "{{SOURCE_B}}"
source_C: "{{SOURCE_C}}"
theme: "{{THEME}}"
tags: [产品分析{{#EXTRA_TAGS}}, {{EXTRA_TAGS}}{{/EXTRA_TAGS}}]
---

# 产品分析 {{DATE}}：{{THEME}}

## 选品逻辑

**使用规律 {{PATTERN_NUM}}：{{PATTERN_NAME}}**

| 产品 | 来源 | 定位 |
|------|------|------|
| A: {{PRODUCT_A}} | {{SOURCE_A}} | {{ROLE_A}} |
| B: {{PRODUCT_B}} | {{SOURCE_B}} | {{ROLE_B}} |
| C: {{PRODUCT_C}} | {{SOURCE_C}} | {{ROLE_C}} |

**关联逻辑**：{{RELATIONSHIP_EXPLANATION}}

---

## 产品 A：{{PRODUCT_A}}

### Step 1：产品定位与体验

**一句话定位**：{{ONE_LINER}}

**目标用户**：{{TARGET_USERS}}

**核心功能**：
1. {{FEATURE_1}}
2. {{FEATURE_2}}
3. {{FEATURE_3}}
4. {{FEATURE_4}}
5. {{FEATURE_5}}

**用户路径**：{{USER_PATH}}

### Step 2：问题与价值

**之前怎么解决**：{{BEFORE_SOLUTION}}

**解决的痛苦**：{{PAIN_POINT}}

**替代方案**：{{ALTERNATIVES}}

**付费理由**：{{WHY_PAY}}

### Step 3：商业模式拆解

**变现方式**：{{MONETIZATION}}
**谁付钱**：{{WHO_PAYS}}
**收费点**：{{CHARGE_POINTS}}

### Step 4：收入估算

**公式**：月收入 ≈ 月流量 × 付费转化率 × 客单价

- 流量：{{TRAFFIC_EST}}（{{TRAFFIC_REASON}}）
- 转化率：{{CONVERSION_EST}}（{{CONVERSION_REASON}}）
- 客单价：{{ARPU_EST}}（{{ARPU_REASON}}）

| 估算 | 金额 | 依据 |
|------|------|------|
| 低估 | ${{LOW}} | {{LOW_REASON}} |
| 中估 | ${{MID}} | {{MID_REASON}} |
| 高估 | ${{HIGH}} | {{HIGH_REASON}} |

### Step 5：技术实现路径

- **前端**：{{FRONTEND}}
- **后端**：{{BACKEND}}
- **存储**：{{STORAGE}}
- **AI**：{{AI_USAGE}}
- **棘手点**：
  1. {{HARD_1}}
  2. {{HARD_2}}

### Step 6：增长方式

**主要流量**：{{TRAFFIC_SOURCE}}
**为什么能获取流量**：{{TRAFFIC_WHY}}
**最值得复制的增长动作**：{{GROWTH_ACTION}}

### Step 7：对我的启发

**最值得抄的点**：{{COPY_POINT}}

**我可以快速做一个什么类似产品**：{{IDEA_NAME}}——{{IDEA_ONE_LINER}}

### Step 8：程序员思维盲区

> {{BLIND_SPOT}}

### 需求嗅觉：{{PRODUCT_A}}

**A1 用户原声**：
- "{{USER_VOICE_1}}" —— {{USER_VOICE_SOURCE_1}}
- "{{USER_VOICE_2}}" —— {{USER_VOICE_SOURCE_2}}

**A2 痛点量化**：
- 时间成本：{{TIME_COST}}/周
- 金钱成本：{{MONEY_COST}}
- 情绪成本：{{EMOTION_COST}}/10（{{EMOTION_REASON}}）

**A3 需求风险**：{{DEMAND_FREQUENCY}} / {{DEMAND_Necessity}} / 平台消灭风险：{{PLATFORM_RISK}} / 技术迭代风险：{{TECH_RISK}}

**A4 价格锚点**：不买此产品时替代花费 {{ALTERNATIVE_COST}}，同类非AI工具定价 {{NON_AI_PRICING}}

**A5 最小验证方法**：{{VALIDATION_METHOD}}

**A6 定制盲区**（个人开发者）：{{SOLO_DEV_BLIND_SPOT}}

---

## 产品 B：{{PRODUCT_B}}

<!-- Same 8-step + A1-A6 structure as Product A -->

---

## 产品 C：{{PRODUCT_C}}

<!-- Same 8-step + A1-A6 structure as Product A -->

---

## A7：需求-收入关联

| 维度 | 产品A | 产品B | 产品C |
|------|-------|-------|-------|
| 痛点排序（1最痛） | {{PAIN_RANK_A}} | {{PAIN_RANK_B}} | {{PAIN_RANK_C}} |
| 收入排序（1最高） | {{REV_RANK_A}} | {{REV_RANK_B}} | {{REV_RANK_C}} |

**供需错配分析**：{{SUPPLY_DEMAND_ANALYSIS}}

**结论**：{{SD_CONCLUSION}}

---

## 已分析产品清单

| # | 日期 | 产品 | 来源 | MRR 估算 |
|---|------|------|------|----------|
| {{HISTORY_TABLE_ROWS}} |
