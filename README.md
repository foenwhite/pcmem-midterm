# PC-Mem 期中汇报材料

选题 1「帮助 Agent 的全 PC 文件管理记忆系统」的期中汇报材料。

本仓库只含汇报材料（幻灯片 / 逐字稿 / 结果位）；系统实现、原始数据与运行记录在项目主仓库，不随本仓库分发。

## 文件

| 文件 | 用途 |
|---|---|
| `slides.html` | 幻灯片源文件，单文件、无外链、离线可用。← → 翻页，F 全屏，⌘P 导出 |
| `slides.pdf` | 16:9 导出版，8 页 = 封面 + 5 页正文 + 备查 + 讨论 |
| `script.md` | 逐字稿，按页分；含时间轴、每页字数、超时先删哪句、Q&A 备答 |
| `reports-for-ref/` | 期中调研的四份独立 HTML；Victoria 浏览器因数据集许可未收录，见该目录 README |
| `results/` | 对照实验数据；现在为空，只放了填表说明 |
| `results/kg-rag-comparison.md` | 结果记录模板（待填） |

## 五页与时间

| 页 | 主题 | 时长 |
|---|---|---|
| 01 | 研究背景与核心问题 | 40 秒 |
| 02 | 系统架构与技术路线 | 60 秒 |
| 03 | 我们的主要工作与创新点 | 90 秒 |
| 04 | 当前进展与阶段性结果 | 90 秒 |
| 05 | 现存问题与后续计划 | 40 秒 |

第 4 页的两张对照表故意留空：A 是公开基准，B 是 Victoria 真实文件树；跑完再填，不在空表上写结论。

## 结果出来后怎么更新

1. 跑基准（命令与成本见项目主仓库的 `docs/benchmark-catalogue.zh.md`）：

   ```bash
   uv run python scripts/run_benchmark_eval.py \
     --dataset ~/data/MultiHopRAG \
     --corpus-dir "$PCMEM_DATA_DIR/multihop" \
     --limit 0 --sources 5 --concurrency 32 \
     --output .context/benchmark-full
   ```

2. 打开两份报告：A 用 `run_benchmark_eval.py` 的 `report.md`（`Accuracy` / `Grounded` /
   `exact McNemar p`）；B 用 `sci-rag eval answers` 的 `report.md`（四维 0–2 均分）。
   抄进 `results/kg-rag-comparison.md`，字段含义见 `results/README.md`。

3. 改 `slides.html`：搜 `待填`。
   - A 表填 `report.md` 的 accuracy / grounded_rate / McNemar p；
   - B 表填 `sci-rag eval answers` 的四维均分（证据支撑、引用准确、完整性、正确性）；
   - 删掉标题旁的 `<span class="pending">待填</span>`；
   - 自建语料出 gold 后，复制 B 表作为第三组；
   - 同时改第 4 页标题与导语（例如「系统已跑通，对照实验给出了第一组结果」）。

4. 重新导出 PDF：

   ```bash
   "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
     --headless=new --disable-gpu --no-pdf-header-footer \
     --run-all-compositor-stages-before-draw --virtual-time-budget=4000 \
     --print-to-pdf=slides.pdf "file://$PWD/slides.html"
   ```

5. 同步 `script.md` 第 4 页最后两句：把「这两张表都是空的，只能写待填」换成实测结论，
   并保留「我们不在空表上下结论」这句的姿态，除非数据真的出来了。

## 样式约定（改版时别破坏）

- 纯白底 `#fff`，发丝线 `#e3e5e7`，无阴影、无渐变、无图片。
- 文字只用三档灰 + 一个强调色：`#111` / `#333` / `#737b82`，强调色 `#1c4587`
  只出现在小标题、引用竖线、少量关键数字上。
- 字号：页标题 33、节标题 13.5、正文 13–15、脚注 11–12。
- 每页固定 1280×720，JS 按窗口等比缩放；打印为 13.333×7.5 英寸，一页一张。
- 表格只用横线，不用竖线、不用斑马纹；空数据用浅灰 `—` 与虚线底边标识。
- 标题写具体名词或陈述句；页内小标题同样避免反问式（用「普通 RAG 的缺点」，
  不写「普通 RAG 为什么答不了」；用「四类评测缺口」，不写「还没到能下结论的地方」）。

## 备注

- `slides.html` 不依赖网络或本地字体文件，拷走即可用。
- 页脚编号由 JS 按「有 footer 的页」自动生成，新增页时不用手改数字。
