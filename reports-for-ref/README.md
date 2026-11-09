# 参考资料（HTML）

期中调研阶段产出的四份独立页面，答辩追问时用。都是单文件，离线可开。

| 文件 | 内容 |
|---|---|
| `competitor-research.html` | 五个选题的同类项目、已有人做的部分与空白点 |
| `dataset-benchmark-compare.html` | A1–A8 覆盖矩阵、8 个候选 benchmark、分层候选与许可 |
| `eval-playbook.html` | GPU / API / 笔记本三套评测方案与估时 |
| `sandbox-infra-for-agent-training.html` | Agent 训练沙箱基础设施调研：能借什么、不借什么 |

## 未收录

- `victoria-subset-explorer.html`：内嵌 HippoCamp `Victoria_Subset` 的原始目录、137 个文件清单与 11 道标注问答，含人物姓名与邮箱。该数据集为 HippoCamp Research License v1（仅非商业研究，不可再分发），且页面含可识别的个人信息，因此不随公开仓库分发，只保留在本地。

## 发布前清理记录

- 删除调研记录中的内部会话 ID（`dataset-benchmark-compare.html`）。
- 已检查并确认不含：API key、访问令牌、主机地址、账号 ID、本地绝对路径、SSH 密钥信息。
