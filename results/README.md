# 对照实验数据（待填）

本目录只放**填表用的数字**与口径说明；原始报告留在项目主仓库的 `.context/benchmark-*/` 下，不复制进来。

- `kg-rag-comparison.md` — 与幻灯片第 4 页一一对应的记录表
- 出数后请在 `slides.html` 搜 `待填` 同步，然后重导 PDF

## 数字从哪来

```bash
uv run python scripts/run_benchmark_eval.py \
  --dataset ~/data/MultiHopRAG \
  --corpus-dir "$PCMEM_DATA_DIR/multihop" \
  --limit 0 --sources 5 --concurrency 32 \
  --output .context/benchmark-full
```

输出目录里的 `report.json` 是机读结果，`report.md` 是同内容的表格。
幻灯片只抄 `report.md` 的表，不自己二次算。

## 字段含义（别改口径）

| 幻灯片列 | report 字段 | 含义 |
|---|---|---|
| 答案正确率 | `summary[cond].accuracy` | 判官在 0–2 正确性上给 ≥ 2 的占比；**不是 exact match** |
| 证据支撑 | `summary[cond].grounded_rate` | 答案能否被检索到的证据支撑的通过率 |
| 配对 p | `comparisons.rag_vs_kg.p_value` | kg 与 rag 的 exact two-sided McNemar |
| — | `comparisons.rag_vs_kg.a_only` / `b_only` / `n` | 不一致对数与配对题数，写备注用 |
| — | `summary[cond].answered` / `errors` | 有效作答数与失败数 |

`kg − rag` 行：差值 = kg 减 rag（写成 `+0.021` 或 `−0.014`），p 用上面那个 `p_value`；
差值方向与 p 一起读，不要只报 p。

## 第二组：Victoria_Subset（真实文件树）

B 表用的是 `sci-rag eval answers --profile interactive|deep` 的输出，不是 benchmark runner：

| 幻灯片列 | report 字段（0–2 均分） | 含义 |
|---|---|---|
| 证据支撑 | `groundedness_mean` | 每条结论能否被检索到的段落支撑 |
| 引用准确 | `citation_accuracy_mean` | 引用编号是否指向真正支撑该句的段落 |
| 完整性 | `completeness_mean` | 参考答案的要点覆盖了多少 |
| 正确性 | `correctness_mean` | 判官对答案正确性的判定 |

- `interactive` = RAG（向量 + 关键字），`deep` = KG（加图与社区）；没有 plain 档。
- n = 11（Victoria_Subset 的标注题数），体量小，只报差值，不做显著性检验。
- 11 月 10 日的 n=1 pilot 记录在项目主仓库的 `.context/pcmem-pilot-20261110/`（未随本仓库分发），只作参照，不进表。

## 填表检查

- [ ] 三个条件同一 answer model、同一 judge、同一 `--sources`、同一采样 seed
- [ ] 记下 `n`、`seed`、`limit`、模型名，以及跑数的日期
- [ ] A 表只有 `kg − rag` 那一行填 p；上面三行的 p 留 `—`；B 表没有 p 列
- [ ] 结论区分「显著」与「更好」：p 显著但差值为负，照写
- [ ] 若报错题数不为 0，写进备注，不悄悄按 0 处理
- [ ] 自建语料的结果单独一张表，不与公开基准混表
