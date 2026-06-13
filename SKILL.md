---
name: investment-dd
description: Use for personal-investor pre-investment analysis of private or non-listed companies/projects, especially when the user relies on company-provided materials, frontline staff data collection, public data verification, financial/return recalculation, red-flag judgment, or asks whether current evidence supports an investment decision. Always start with a preflight information gate, then produce either a data request checklist or an evidence-graded HTML/PDF decision report with explicit conclusion downgrade rules.
---

# 个人投资者投前判断

**产出：前线数据采集清单，或完整 HTML/PDF 投前判断报告**。报告包含资料缺口、公开核验、收益测算、红旗动作、结论降级规则和 QA 记录。

本 skill 面向个人投资者分析非上市企业、项目公司、SPV、基金份额或非标准交易结构。默认假设用户不是专业投资机构，前线人员需要明确的数据清单，关键事实主要依赖公司材料和公开数据核验。

如果用户只需要资料清单，而不是投资判断或收益测算，只输出前线数据采集清单和替代资料清单，不生成完整报告。

## 触发条件

用户提供材料并且意图是**做投资判断**，例如：投资分析、能不能投、收益率测算、投资决策、分析这个标的、看看这个项目、判断这个非上市公司、做投委会材料、做项目 DD。

只要输入中出现以下任一类信息，就应使用本 skill：
- 财务数据：历史报表、盈利预测、估值、回购/差补、IRR/MOIC、现金流
- 非标准业务数据：产能、订单、客户、良率、价格、成本、库存、渠道、资质
- 公司治理信息：股权结构、实控人、董事会/投委会权利、关联交易、担保、诉讼、质押
- 交易结构：基金/SPV、GP/LP、跟投、分配瀑布、管理费、carry、退出条款

## 硬约束

1. **不把材料当事实。** 用户材料、FA 材料、企业 PPT、访谈纪要只能作为待验证输入。
2. **不把数据源清单当边界。** 免费公开数据源无法穷举；`references/public-data-sources.md` 是种子库和发现协议，不是完整清单。
3. **不心算。** 财务、收益率、差补、回购、DSCR、分红穿透均用 Python 或可复现表格重算。
4. **信息缺口必须传导到结论。** 每个关键缺口必须说明影响哪个投资判断，以及结论应降级到什么程度。
5. **不降低证据标准。** 找不到权威来源时，结论必须降级为“待验证”“无法验证”或“需线下尽调”。
6. **不跳过 QA。** 报告完成前必须执行 `references/qa-checklist.md` 的门禁检查。

## 四层工作流

### 第零层：前置判断

先读 `references/preflight-gate.md` 和 `references/info-checklist.md`。判断材料是否足够开工：

- 若核心数据全缺，不出投资判断报告，只输出前线数据请求清单。
- 若可初步分析，必须说明缺什么、替代资料是什么、哪些结论上限只能是“待验证”。
- 若涉及非标准交易结构，先读 `references/deal-type-checklist.md` 做轻量交易分类。
- 若涉及基金/SPV/GP/LP/管理费/carry/优先回报/分配瀑布，再读 `references/return-methodology.md`。

### 第一层：前线采数

先读 `references/frontline-data-collection-checklist.md`、`references/alternative-data-sources.md` 和 `references/industry-data-checklist.md`。给前线人员输出简单直接的资料清单、访谈问题和现场观察点。每项数据必须包含：理想资料、次优资料、最低替代、用途、缺失影响。

### 第二层：公开核验

先读 `references/public-data-verification-playbook.md` 和 `references/public-data-sources.md`。对公司材料中的关键声明建立 Source Card，标注 S/A/B/C/D 证据等级、冲突、局限性和访问日期。

### 第三层：个人投资者决策报告

先读 `references/individual-investor-report-template.md`、`references/conclusion-downgrade-rules.md` 和 `references/red-flag-playbook.md`。报告必须面向投资人本人，结论先行，明确写出：可推进、有条件关注、暂缓判断或不建议。`references/report-template.md` 只作为格式、Source Card 附录和 PDF 渲染规范参考，不作为内容结构主模板。

## 分析流程

### 阶段 1：素材提取与数据字典

- PPT/PDF/DOCX/XLSX 提取全文和表格；图片用 OCR 或逐张描述。
- 聊天记录、访谈纪要提取关键数据点，但标注为低等级来源，并转成待核验假设。
- 建立数据字典：字段、数值、单位、币种、期间、来源、页码/URL、原始表述。
- 将非标准业务数据拆成经营、商业、单位经济、治理、合规五类。

### 阶段 2：公开数据源发现与外部交叉核验

先读 `references/public-data-sources.md`。

对材料中的关键声明逐项核验：
- 并行检索市场/竞对/技术/政策/法律与治理信息。
- 优先寻找官方、监管、交易所、法院、工商、知识产权、统计局、行业主管部门等原始来源。
- 对未覆盖行业执行“未知行业模式”：识别主管部门、许可资质、行业标准、行政处罚、上市/发债可比公司、招投标、地方规划。
- 每个新增来源必须建立 Source Card。
- 结论标注：已验证、部分验证、无法验证、相互矛盾、需线下尽调。

### 阶段 3：独立财务核算

必须用 Python 或可复现表格独立重算：
- 资产负债表、利润表、现金流和关键经营数据勾稽。
- 收入拆分到产品、产能、销量、单价、客户或项目，而不是只用一个增长率。
- 成本拆分固定/可变成本，形成盈亏平衡和敏感性分析。
- DSCR 使用实际还本付息计划；没有计划时标注待确认，不能假设。
- 分红链条逐级穿透，不能用单一分配系数替代。

### 阶段 4：收益测算

先读 `references/return-methodology.md`。

收益测算前必须明确：
- 我方身份：GP、LP、跟投、直接持股或其他安排。
- 年度分配和退出分配是否走不同瀑布。
- 管理费、carry、税费、优先回报、回购/差补、退出时点。
- 三情景假设必须独立验证合理性，不能照搬材料。

### 阶段 5：报告输出与 QA

先读 `references/individual-investor-report-template.md`，按个人投资者模板输出 HTML。再读 `references/report-template.md` 的格式、来源附录和 PDF 规范；如需 PDF，用 Playwright 导出。

报告完成前必须执行 `references/qa-checklist.md`：
- 数据一致性检查
- 来源和证据等级检查
- 财务模型重算检查
- 情景假设检查
- 结论降级和信息缺口传导检查
- PDF/HTML 渲染检查

QA 不通过时，不得输出“已完成”结论；必须列出失败项、影响范围和修复动作。

## 结论表达规则

- 证据充分且模型通过 QA：可写“初步具备推进价值/建议进入下一阶段”。
- 关键商业或财务假设只有企业口径：只能写“有条件关注，需线下核验”。
- 关键事实无权威来源或来源相互矛盾：不能写“可投”，只能写“暂缓判断”。
- 收益率对单一未经验证变量高度敏感：必须把该变量列为 CP 条件或投决前置事项。
- 核心收入、利润、退出路径或回购偿付能力无法验证：不得输出正面投资判断。

## 格式规范

- 标题不用 emoji。
- 正文 Georgia 衬线体 + 中文宋体，标题 sans-serif。
- 段落 3 句以上拆 bullet。
- 专业术语首次出现加中文解释。
- KPI 固定列数，数字不换行。
- 表格列宽手动指定。
- PDF 页眉空白，页码居右。

## 使用工具

| 工具 | 用途 |
|------|------|
| Web search / Browse | 发现并核验公开来源 |
| Agent (Explore) × 3-4 | 市场、竞对、技术、政策/法律并行核验 |
| Python | 财务、收益率、差补、敏感性重算 |
| Playwright | HTML 渲染和 PDF 导出 |
| Manual QA | 按 QA checklist 逐项确认 |
