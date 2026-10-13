CLASSIFY: L2(cfts SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-LABJUDGE-EXT14-R4-cfts.md

应卡: inbox/LABJUDGE-EXT14-R4-cfts.md
引擎: DEEPSEEK_API_KEY/deepseek-chat usage={"prompt_tokens": 651, "completion_tokens": 1823, "total_tokens": 2474, "prompt_tokens_details": {"cached_tokens": 512}, "prompt_cache_hit_tokens": 512, "prompt_cache_miss_tokens": 139}

逐项终判如下。

## ① oid 三元组与同 commit 绑定

- 包A `46f24f40ee70` 自述含 ci×3 + 三证书 v1.0.1  
- 包B `20f81465667b` 自述含 SUP-01 + KI-ADD1 + ERRATUM + FINDING-ADD1/ADD2 + registry v2  
- FINDING `cfa41ebd1310`

**判定：PASS（单卡自含层面）**  
前提是这三个 oid 均能在包B 同一 commit 内被 `git cat-file`/`sha256` 独立复算。你给出的「五元同 JSON 同 commit」已把 `witness_oid=commit_oid=R1_artifact_oid` 钉成同值，这满足「证据不跨 commit 漂移」的硬条件。  
**残留要求**：包A/包B/FINDING 的 oid→文件路径映射需在 registry v2 中可解析；若 registry 只登记 oid 不登记 path，则降为「仍缺：oid→path 解析表」。

## ② 五元同 JSON 同 commit

- `zeta-iso-100` ↔ entry 同名 ↔ `artifacts/witnesses-zeta/zeta-iso-100.witness.json` ↔ `46f24f40ee70` ↔ verifier `ci/witness_zeta_verify.py`
- `witness_oid = commit_oid = R1_artifact_oid` 同值
- tier = W1 存在性 PASS / 完备性 UNRESOLVED
- psi-trunc = W1 管道演练级 + scope_fence 两句逐字

**判定：PASS**  
五元同 commit 且 oid 三值同一是本卡最强的防漂移证据。tier 与 psi-trunc 的 scope_fence 逐字给出，满足「不得进入任何 WIT 完备性计数，不得出现在 GAP 链支撑集」。  
**注意**：这不构成 WIT 完备性证据，只构成「存在性 + 管道可重放」证据，与 tier 自述一致。

## ③ 关闭条件逐字

「张角余量纳入后 N_B 区间落入唯一整数窗；不得以放宽区间宽度绕过」

**判定：PASS（条件已逐字锁定）**  
但请区分两件事：  
- 条件文本已逐字固定 → PASS  
- 条件是否已被满足 → 取决于 ⑥ 的 N_B 区间是否落入唯一整数窗

你给的 N_B = `[29.09812430226496, 29.09812430426496]`，宽度约 `2.0e-9`，落在整数 29 与 30 之间，**不跨整数**，因此「唯一整数窗」在数值上成立。  
**残留要求**：需给出「张角余量纳入」的显式算式或代码位点；若只在文档中声明而未在 `gap_probe` 或 verifier 中出现余量项，则降为「仍缺：余量纳入的可执行位点」。

## ④ 护栏三句逐字

- G3' 探测域 = mathlib v4.10.0 符号表  
- ABSENT 为工程层事实，非元数学结论  
- 四锚为谓词映射，非 RH 蕴含

**判定：PASS**  
三句逐字且语义互不冲突：探测域限定、ABSENT 去元数学化、四锚去 RH 蕴含。满足「不得越界为元数学/RH 结论」的护栏要求。

## ⑤ 零改动 diff

- iso100：仅 disclosure / generator.sha / witness_sha256 变，数学 17/17 逐位同  
- iso1000：变 6（+status/blocked_subcode/retry_budget），16/16 同  
- trunc：变 4，11/11 同

**判定：PASS**  
数学载荷逐位不变 + 仅元数据/状态字段变动，符合「v1.0.0↔v1.0.1 零数学改动」的声明。  
**注意**：`generator.sha` 与 `witness_sha256` 变化必须能被解释为「重新生成导致的元数据更新」，而非数学内容变化；17/17、16/16、11/11 逐位同已覆盖此点。

## ⑥ 重放位级一致

- 重置前/后两容器，py3.12.12 + mpmath1.3.0
- N_B = `[29.09812430226496, 29.09812430426496]`
- trunc 残差 `[-3365.36, 3142.19] ⊆ ±5195860.44` 逐位同
- verify: iso1000 PASS / trunc PASS / iso100 FAIL@Backlund（KI 钉档）
- pytest `41 passed in 1497.81s`

**判定：PASS（重放层面）**  
两容器位级一致 + 三 verify 结果与 KI 钉档一致 + pytest 全过，满足「可重放、可复算、失败点被 KI 固定解释」。  
**关键点**：iso100 FAIL@Backlund 不是缺陷，而是 KI 钉档下的预期失败；这与 ② 的 tier「存在性 PASS/完备性 UNRESOLVED」自洽。

## ⑦ 哈希锁 sha256(16hex)

- ZetaAnchor.lean = `5a046673116b404d`
- gap_probe = `7daebbfa5572dc7d`
- SPEC = `c8e72602d50fa20e`
- KI v1 = `fa74b75164e102b2`（ADD1 追加原文不动）

**判定：PASS**  
四锚哈希锁定 + KI v1 追加不改原文，满足「证据可锚定、追加不覆盖」的要求。  
**残留要求**：16hex 为前缀截断；若需强抗碰撞，应同时给出完整 64hex。若只给 16hex，则降为「仍缺：完整 sha256 或截断规则声明」。

## ⑧ 58 回扫全仓

命中仅 ZETA-INST-01（被勘误）/ ERRATUM / SUP-01 + 证书 winding_2NT（2N(T) 口径），无其他依赖

**判定：PASS**  
回扫范围 58 处、命中集闭合、无隐藏依赖，满足「依赖面可控」的要求。  
**注意**：需确认 58 回扫的查询模式与仓库根一致；若查询模式未覆盖二进制/生成物，则降为「仍缺：回扫模式与排除规则」。

## ⑨ VERDICT 三分支 echo 硬编码不读 env；NS_LIB_DIR 仅改探测目标目录

**判定：PASS**  
VERDICT 不读 env → 防止环境变量注入 verdict；NS_LIB_DIR 仅改探测目标 → 不改变判定逻辑。两者共同满足「判定与探测目标解耦」。

---

## 总终判

**PASS（单卡自含证据层面）**，但附三条硬残留：

1. **oid→path 解析表**：包A/包B/FINDING 的 oid 必须在 registry v2 中可解析到具体路径，否则 ① 降级。  
2. **张角余量纳入的可执行位点**：③ 的条件文本已锁定，但「余量纳入」需在 `gap_probe` 或 verifier 中有显式代码/算式位点，否则 ③ 只算条件锁定、不算条件已满足。  
3. **完整 sha256 或截断规则**：⑦ 若仅有 16hex，需补完整 64hex 或声明截断规则，否则哈希锁强度不足。

以上三条补齐后，本卡在「R1 条件补强」范围内可判 **PASS 无残留**；未补齐前，判 **PASS（带三项可闭合缺口）**，不属于「仍缺核心证据」，而属于「证据强度可再加固」。

——cfts SI1语义轨·20261013T125627Z
