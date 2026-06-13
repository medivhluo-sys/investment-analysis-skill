# Investment DD Skill

个人投资者非上市项目投前判断 skill。

## 定位

本 skill 用于把公司材料、前线人员采集资料和公开数据，整理成可供个人投资者决策的投前判断报告。默认目标不是机构级完整尽调，而是回答：

- 当前资料是否足够启动分析？
- 前线人员还需要收集哪些数据？
- 公司材料中哪些事实能被公开数据验证？
- 收益测算是否依赖未验证假设？
- 现有证据支持可推进、有条件关注、暂缓判断还是不建议？

## 核心流程

1. 第零层：前置判断门禁
2. 第一层：前线数据采集
3. 第二层：公开数据核验
4. 第三层：个人投资者决策报告

## 硬约束

- 不把公司材料当事实。
- 关键事实必须做来源分级和公开核验。
- 财务、收益率、回购、差补和敏感性必须用 Python 或可复现表格重算。
- 信息缺口必须传导到结论降级。
- 高影响缺口未关闭时，不输出正面投资判断。

## 主要 reference

```text
references/
├── preflight-gate.md
├── info-checklist.md
├── deal-type-checklist.md
├── frontline-data-collection-checklist.md
├── alternative-data-sources.md
├── industry-data-checklist.md
├── public-data-verification-playbook.md
├── public-data-sources.md
├── conclusion-downgrade-rules.md
├── red-flag-playbook.md
├── individual-investor-report-template.md
├── return-methodology.md
├── report-template.md
└── qa-checklist.md
```
