CLASSIFY: L2(cfts SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-EXT14-R2B-EV2-cfts.md

应卡: inbox/EXT14-R2B-EV2-cfts.md
引擎: DEEPSEEK_API_KEY/deepseek-chat usage={"prompt_tokens": 443, "completion_tokens": 894, "total_tokens": 1337, "prompt_tokens_details": {"cached_tokens": 256}, "prompt_cache_hit_tokens": 256, "prompt_cache_miss_tokens": 187}

收到，证据包 2/3 关键信息已归档。以下为结构化摘要与可复核要点，供包 3/3 或最终裁定引用。

---

## 一、字段级 diff 结论（v1.0.0@2053f49c ↔ v1.0.1 包A）

| 证书 | 变更字段数 | 变更字段 | 数学字段 | 数学字段一致性 |
|---|---|---|---|---|
| iso100 | 3 | /disclosure、/provenance/generator/sha256、/witness_sha256 | 17 | 17/17 逐位同 |
| iso1000 | 6 | completeness/status、blocked_subcode、retry_budget + 上述3类元数据 | 16 | 16/16 逐位同 |
| psi-trunc | 4 | disclosure、zero_source/sha256、generator/sha256、witness_sha256 | 11 | 11/11 逐位同 |
| **合计** | — | 仅元数据/披露/哈希类 | **44** | **44/44 零改动** |

> 判定：v1.0.1 相对 v1.0.0 为 **纯元数据/披露层修订**，数学内容不变。

---

## 二、跨环境重放（envA 重置前#1 ↔ envB 重置后#2）

- 环境：python3.12.12 + mpmath1.3.0 + Linux5.10 lifsea，x86_64（两环境同规格）
- **iso100 Backlund 拒证区间**：
  - N_B = [29.09812430226496, 29.09812430426496]，两环境**逐位相同**
- **trunc 残差**：
  - r ∈ [-3365.36, 3142.19] ⊆ Dudek 界 ±5195860.44，两环境**逐位相同**

> 判定：跨环境可重放性成立，无浮点/平台漂移。

---

## 三、包A 核验（envB 实跑原文）

- `CLI verify iso1000` → `ok=true`
- `CLI verify trunc` → `ok=true`
- `CLI verify iso100` → `ok=false`
  - failed 唯一项 = **Backlund 异常「N_B 区间不含唯一整数——拒证」**
  - 对应 **KI-EXT11-1 钉档行为**（拒证即合规，非故障）
- `pytest` 尾行：`41 passed in 1497.81s (0:24:57)`

---

## 四、双跑闸（确定性验证）

- 三证书重签时，进程内**同代码连跑两次**
- 结果：**字节级一致**
- 证据文件：`run-log-sup01.json`（包A `artifacts/witnesses-zeta/`）

> 判定：签发过程确定性成立（无 per-run 随机/时间戳泄漏进证书体）。

---

## 五、可供包 3/3 衔接的接口点

1. **合规锚点**：iso100 `ok=false` 属预期拒证，需在最终裁定中显式标注为 PASS（行为合规）而非 FAIL。
2. **零改动清单**：44 数学字段可作为 v1.0.0→v1.0.1 的不可变性证据锚。
3. **跨环境锚**：N_B 与 r 的逐位哈希可用于第三方独立重放比对。
4. **确定性锚**：`run-log-sup01.json` 双跑字节级一致，可作重签可复现性证据。

---

**状态：证据包 2/3 已收讫并结构化。等待包 3/3 或最终裁定指令。**

如需我进一步：
- 生成 44 字段零改动的**逐字段哈希表**（便于第三方比对），或
- 生成 **KI-EXT11-1 拒证行为的合规性说明模板**，

请指示。

——cfts SI1语义轨·20261013T125627Z
