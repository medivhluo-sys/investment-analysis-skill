# Investment Analysis Skill

Claude Code Skill — 基于公开信息的投资项目分析报告生成。

**产出**：完整的 HTML+PDF 投资分析报告（含收益率测算、情景分析、风险矩阵、尽调清单、独立 QA 验证）。

**不需要任何 API 接口**，仅用 Web 搜索 + Python 独立计算 + Playwright PDF 导出。

## 安装

```bash
# 克隆到 Claude Code skills 目录
git clone https://github.com/medivhluo-sys/investment-analysis-skill.git ~/.claude/skills/investment-dd
```

## 怎么用

1. 把项目材料（PPT/PDF/图片/聊天记录）拖给 Claude Code
2. 告诉它你的投资额度和预期收益率底线
3. 说一句"帮我分析一下这个项目"

Skill 会自动加载，先扫描信息缺口，再按 5 阶段出完整报告。

**最简单的用法：**
> 这是项目的 PPT，我额度 4,000 万，预期年化 ≥10%。帮我分析能不能投。

**你需要给的材料：**
- 项目 PPT/PDF/商业计划书（有就提供）
- 投资额度
- 预期年化收益率底线
- 你的角色（GP/LP/跟投？从谁的份额出？）

## 前置依赖

```bash
pip install playwright python-pptx
playwright install chromium
```

## 适用场景

- 非上市企业或项目结构的早期投资
- 有 PPT/PDF/聊天记录等材料，但无公开财务数据
- 需要独立于融资方的收益率测算和风险判断

## 与 private-equity:dd-checklist 的区别

| | 本 Skill | dd-checklist |
|------|---------|-------------|
| 产出 | 完整投资分析报告 | 仅尽调清单 |
| 用法 | "能不能投？收益率多少？" | "出个尽调清单" |

## 技能结构

```
SKILL.md                     ← 主工作流（缺口扫描 + 5 阶段分析）
references/
├── info-checklist.md        ← 8 项信息收集清单（给前台团队）
├── return-methodology.md    ← 收益率测算方法（分配瀑布 + 分红链条）
└── report-template.md       ← 报告结构模板（前端/正文/后端）
```

## 工作流

1. **信息缺口扫描** — 对照 8 项清单，明确缺什么、用什么替代
2. **素材提取** — PPT/PDF/聊天记录 → 结构化数据
3. **外部交叉核验** — 3-4 路并行 Web 搜索，42 项声明逐条验证
4. **独立财务核算** — Python 重算所有指标，绝不允许心算
5. **报告输出 + QA** — HTML/PDF 双输出 + 独立 Agent 核验
