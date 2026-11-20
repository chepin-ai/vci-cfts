CLASSIFY: L2(cfts SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-TASK-BEAT171-ANSWER-SELF-CHECK-02-cfts-20261120.md

应卡: inbox/TASK-BEAT171-ANSWER-SELF-CHECK-02-cfts-20261120.md
引擎: DEEPSEEK_API_KEY/deepseek-chat usage={"prompt_tokens": 64, "completion_tokens": 821, "total_tokens": 885, "prompt_tokens_details": {"cached_tokens": 0}, "prompt_cache_hit_tokens": 0, "prompt_cache_miss_tokens": 64}

我先确认一下你说的“cfts线补证”具体指哪条线：是 **CFTS（Causal/Fault/…?）** 某个仓库里的 deterministic counterexample search box？为避免我臆造，我需要你提供以下最小信息，否则无法给出真实 commit / run / SHA256：

1. **仓库 URL 或本地路径**（以及默认分支）
2. **cfts 的完整展开名**（例如 “counterexample fault-tolerance search”？）
3. **“补证盒子”对应的现有入口**：脚本路径/函数名/CLI 名
4. **outbox 路径 `outbox/ANS-BEAT171-ANSWER-SELF-CHECK-02-cfts`** 是本地相对路径还是某个远端（GitHub/内部 CI）路径？期望的回卡格式（Markdown/JSON/YAML）？
5. **正控和负控的定义**：你希望正控用什么已知存在反例的输入？负控用什么已知无反例的输入？（或允许我从仓库内已有 fixtures 选）

---

在你补齐信息前，我先把**可执行的交付清单**列清楚，等参数一到我就能直接跑并回卡：

**交付物（回卡内容）**
- 固定 `commit`：`git rev-parse HEAD` + 简短说明分支/tag
- 真实 `run`：完整命令 + 起止时间戳 + exit code
- `artifact SHA256`：对每个产物（反例 JSON、日志、回卡）分别 `sha256sum`
- **正控**：已知存在反例的输入 → 期望 `FOUND` + 反例指纹
- **负控**：已知无反例的输入 → 期望 `NOT_FOUND` + 搜索空间上界/超时说明
- **独立重放**：在干净目录 `git clone` 固定 commit → 同命令 → 比对 SHA256 一致
- **确定性证据**：同一输入跑 ≥2 次，反例字节级一致；给出 `diff` 为空

**我会执行的骨架命令（待你确认路径后替换）**
```bash
set -euo pipefail
REPO=<repo>; COMMIT=<sha>
cd "$(mktemp -d)" && git clone "$REPO" . && git checkout "$COMMIT"
git rev-parse HEAD | tee commit.txt

# 正控
<CFTS_BOX_CMD> --input fixtures/pos_control --out out/pos | tee run_pos.log
# 负控
<CFTS_BOX_CMD> --input fixtures/neg_control --out out/neg --bound <N> | tee run_neg.log
# 确定性重放
<CFTS_BOX_CMD> --input fixtures/pos_control --out out/pos2 | tee run_pos2.log
diff -r out/pos out/pos2

sha256sum out/pos/* out/neg/* run_*.log commit.txt | tee SHA256SUMS
```

**回卡模板（写入 `outbox/ANS-BEAT171-ANSWER-SELF-CHECK-02-cfts`）**
```
commit: <sha>
run: <cmd>  exit=<0>  start=<ts> end=<ts>
artifact_sha256:
  <file>  <hash>
pos_control: FOUND  fingerprint=<...>
neg_control: NOT_FOUND  bound=<...>
determinism: rerun diff = empty
independent_replay: clone@<sha> → sha256 match = YES
```

请把 **1–5** 补上（尤其仓库位置和盒子入口命令），我就按上面流程真实执行、产出 SHA256，并直接把回卡写到指定 outbox。若仓库在远端但我无网络/权限，也请说明可用镜像或本地路径。

——cfts SI1语义轨·20261120T052230Z
