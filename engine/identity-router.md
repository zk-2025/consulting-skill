# 身份识别与问题路由

> **解决什么问题**：不同用户需要完全不同的语言、深度和切入点；追问出的真问题需要映射到对应知识模块。
> **什么时候用**：对话开始时识别身份（第一步）；追问完成后做问题路由（第三步）。
> **联动文件**：`problem-dissolving.md` 追问出真问题后 → 本文件路由 → `modules/` 对应文件

---

### 第一步：用户身份识别与适配

**不同用户需要完全不同的语言、深度和切入点。**

#### 身份分类与适配策略

| 身份 | 典型特征 | 语言风格 | 切入角度 | 深度控制 |
|------|----------|----------|----------|----------|
| **企业老板/CEO** | 关心全局、结果、钱；说大词但可能没想透 | 直接、数据驱动、少废话 | 从ROI和竞争切入 | 战略层→战术层 |
| **创业者** | 资源有限、焦虑、什么都想抓；问题可能很散 | 共情+务实、避免空话 | 从优先级和聚焦切入 | 先砍再做、少即是多 |
| **市场/营销人员** | 有执行经验但缺框架；问题偏战术 | 专业术语可用、需框架 | 从框架和漏斗切入 | 框架→填充→验证 |
| **管理者/总监** | 夹在上下级之间；问题常是"人的问题" | 结构化、给工具 | 从领导梯队和OKR切入 | 诊断→工具→行动 |
| **学生/学习者** | 想理解概念；可能问空泛问题 | 教学式、多举例 | 从定义和案例切入 | 概念→案例→练习 |
| **个人/IP创作者** | 想做个人品牌/自媒体；需求模糊 | 接地气、给模板 | 从传播机制和说服原则切入 | 模板→填空→迭代 |

**识别方法**：
1. 看用户用的词（"战略"/"怎么做"/"帮我理解"→不同身份）
2. 看问题粒度（大而空→老板/学生；细而实→执行者）
3. 看情绪信号（焦虑→创业者；好奇→学生；急切→管理者）

**关键原则**：**不要假设用户知道自己要什么。** 大多数人说的不是真需求，是他们对需求的**第一层描述**——往往模糊、偏颇、甚至方向错误。

---

### 第二步：问题消解

**追问出真问题。详见 `engine/problem-dissolving.md`。** 本文件不重复消解流程，消解完成、确认真问题后回到本文件做路由。

---

### 第三步：问题分类路由

**将追问出的真问题，映射到对应知识模块。**

> ⚠️ 本文件是**唯一权威路由表**。SKILL.md、quick-scan.md 等文件的路由均引用本表，不重复定义。

| 真问题的特征词 | P1 主路由 | P2 补充路由 |
|----------------|-----------|-------------|
| 竞争、差异化、定位、优势构建 | `modules/strategy.md` | `modules/brand-and-marketing.md` |
| 问题不明、方向不清、同时追多个目标 | `modules/strategy.md` | `modules/organization.md` |
| 传播、口碑、爆款、裂变、引流 | `modules/spread-and-growth.md` | `modules/influence.md` |
| 增长、获客、留存、漏斗优化 | `modules/spread-and-growth.md` | `modules/brand-and-marketing.md` |
| 说服、成交、谈判、定价心理 | `modules/influence.md` | `modules/brand-and-marketing.md` |
| 目标对齐、绩效、执行力 | `modules/organization.md` | `modules/operations.md` |
| 人才、梯队、转型、培养、领导力 | `modules/organization.md` | `modules/operations.md` |
| 市场、客户、渠道、营销体系 | `modules/brand-and-marketing.md` | `modules/strategy.md` |
| 品牌、认知、忠诚、资产、IP | `modules/brand-and-marketing.md` | `modules/influence.md` |
| 变现、商业模式、付费转化 | `modules/business-model.md` | `modules/influence.md` |
| 产品、功能、体验、迭代、PMF、MVP | `modules/product.md` | `modules/business-model.md` |
| 定价、盈利、现金流、毛利率、单位经济、"卖得越多越亏" | `modules/finance.md` | `modules/business-model.md` |
| 目标模糊、想搞清楚目标、说"我想做X但不知从何开始" | `modules/goal.md` | `modules/operations.md` |
| 想找对标、想模仿谁、说"我该学谁" | `modules/benchmark.md` | `modules/spread-and-growth.md` |
| 想保存诊断、说"保存""记下来" | `engine/save.md` | — |
| 想继续诊断、说"继续""之前的" | `engine/restore.md` | — |
| 想生成报告、说"出报告""打包" | `engine/report.md` | — |

**兜底规则**：如果真问题特征词不明确、跨多个模块、或拿不准 →
1. 先进 `modules/strategy.md` 用论点思考锁定核心问题
2. 锁定后再路由到具体模块

**路由执行规则**：
- 每次只进 **1个P1模块** 诊断，诊断完毕后再决定是否需要P2补充
- 不要同时调用多个模块一次性输出

---
