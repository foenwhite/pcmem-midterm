# KG × RAG 对照结果

**状态**：待填（链路已跑通，全量未完成）
**更新于**：—
**运行**：`—`（命令与参数）
**模型**：answer = `—` · judge = `—`
**采样**：n = 639 / seed = 0 / sources = 5（MultiHop-RAG 1/4 分层抽样）

## MultiHop-RAG

| 条件 | 检索配置 | 答案正确率 | 证据支撑 | 配对 p |
|---|---|---:|---:|---:|
| plain | 不给检索，直接作答 | — | — | — |
| rag | 向量 + 关键字，RRF | — | — | — |
| kg | 五路全开（含图与社区） | — | — | — |
| kg − rag | exact McNemar | Δ — | Δ — | — |

备注（错误数、不一致对数、异常）：

-

## Victoria_Subset（真实文件树，11 题）

> RAG = `interactive`，KG = `deep`；四维均为 0–2 均分。n 小，只报差值，不做显著性检验。

**运行**：2026-11-10 · 语料 88 文档 / 2,328 段 · answer `Qwen3-30B-A3B-Instruct-2507` ·
judge `DeepSeek-V4.1-Flash` · compression disabled · graded 11/11

| 条件 | 证据支撑 | 引用准确 | 完整性 | 正确性 |
|---|---:|---:|---:|---:|
| RAG（interactive） | 1.36 | 1.55 | 1.36 | 1.00 |
| KG（deep） | 1.55 | 1.73 | 1.36 | 1.09 |
| KG − RAG | +0.19 | +0.18 | 0.00 | +0.09 |

读法：三个维度小幅上升，完整性持平；各维 95% CI 互相重叠
（例：正确性 RAG 1.00 [0.64, 1.36] vs KG 1.09 [0.73, 1.45]），
n = 11，只能作为方向参考，不能作为结论。

备注（会影响解释的口径）：

- KG 运行时 `communities = 0`，社区摘要层没有建；`deep` 实际是向量 + 关键字 + 图 + HyDE。
- RAG 运行时图谱只抽到 514 实体 / 509 关系（抽取尚未完成），KG 运行时为 9,480 / 11,845；
  `interactive` 不读图，这个差异不影响 B 表第一行，但记录在案。

## 自建个人语料（待标注）

> 12/01 出 gold 后再填；与上表同口径、同模型，不混表。

| 条件 | 检索配置 | 答案正确率 | 证据支撑 | 配对 p |
|---|---|---:|---:|---:|
| plain | 不给检索 | — | — | — |
| rag | 向量 + 关键字 | — | — | — |
| kg | 五路全开 | — | — | — |
| kg − rag | exact McNemar | Δ — | Δ — | — |

规模：— 个文件，— 道题；标注项：版本链 / 项目归属 / 文件间引用 / 时间线。

## 一句话结论

> 出数前不写。出数后只写这一句：差异方向、显著性，以及各自出现在哪类题；零差异照写。

---

## 填表来源

| 本表 | report 字段 |
|---|---|
| 答案正确率 | `summary[cond].accuracy` |
| 证据支撑 | `summary[cond].grounded_rate` |
| 配对 p | `comparisons.rag_vs_kg.p_value` |
| 不一致对数 | `comparisons.rag_vs_kg.a_only` / `b_only` |
| 有效作答 | `summary[cond].answered` / `errors` |

B 表字段见 `README.md` 的「第二组」一节（`groundedness_mean` 等四项，来自 `sci-rag eval answers`）。

口径与检查项见 `README.md`。
