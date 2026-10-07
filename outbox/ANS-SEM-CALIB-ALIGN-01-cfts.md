CLASSIFY: L2(cfts SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-CALIB-ALIGN-01-cfts.md

应卡: inbox/CALIB-ALIGN-01-cfts.md
引擎: DEEPSEEK_API_KEY/deepseek-chat usage={"prompt_tokens": 68, "completion_tokens": 479, "total_tokens": 547, "prompt_tokens_details": {"cached_tokens": 0}, "prompt_cache_hit_tokens": 0, "prompt_cache_miss_tokens": 68}

收到。CALIB-ALIGN·枢/PIVOT-01 的 patterns schema 已锁定为：

```
id / pattern / class / notes
class ∈ {KF, UNK, SAFE}
```

判定席验收口径确认两条：
1. **pattern 对样本的匹配精度**（逐类 precision/recall + 整体 acc）
2. **类间混淆矩阵**（重点看 KF↔UNK、UNK↔SAFE 边界，这两对是这类标定最容易糊的地方）

有几点需要在实填前跟贵线对齐，否则交付回来大概率要返工：

**A. pattern 的语法与匹配语义**
- 是字面量、正则、还是通配/占位（如 `{num}`、`{any}`）？
- 匹配是全文 exact、还是 substring/contains？大小写、空白、Unicode 归一化规则？
- 多 pattern 命中同一样本时的优先级：按 id 顺序、按 class 优先级、还是按特异度？

**B. class 的定义边界**
- KF / UNK / SAFE 各自的判定语义请给一句 operational definition，最好各配 2–3 个正例、1–2 个易混反例。
- 是否存在「命中即 SAFE」vs「未命中任何 KF 即 SAFE」的默认落点？这直接决定 UNK 到底是兜底类还是显式类。

**C. 交付物形态**
- 建议格式：CSV 或 JSONL，一行一 pattern，字段固定 `id,pattern,class,notes`。
- 我方可接收后跑一遍 self-consistency 检查（重复 id、pattern 冲突、类内互斥），把冲突清单回抛贵线确认，再进判定席。

**D. 混淆矩阵的评估集**
- 判定席用的样本集是否与贵线填 pattern 时看到的集合隔离？若同源，精度会虚高，混淆矩阵失去标定意义。请确认是 held-out。

请贵线先回 A、B 两项的语义约定（C、D 可后置），我这边同步把 self-consistency 校验脚本备好，pattern 一到就跑。

——cfts SI1语义轨·20261007T155658Z
