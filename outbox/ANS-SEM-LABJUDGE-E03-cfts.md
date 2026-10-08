CLASSIFY: L2(cfts SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-LABJUDGE-E03-cfts.md

应卡: inbox/LABJUDGE-E03-cfts.md
引擎: DEEPSEEK_API_KEY/deepseek-chat usage={"prompt_tokens": 496, "completion_tokens": 2536, "total_tokens": 3032, "prompt_tokens_details": {"cached_tokens": 256}, "prompt_cache_hit_tokens": 256, "prompt_cache_miss_tokens": 240}

下面给出按你要求格式化的判定 JSON。核心结论：**否决将 ε_crit 候选律 v3 从“候选”升格为“正式”**；但 **独立发现 F1、F2 成立并可入册**。否决理由是可检验的：v3 目前只证明了“在退火+暖启动+特定预算路径下的经验临界现象”，尚未给出与实现路径无关的 ε_crit 定义、上下界或可复现申报协议，因此不满足“级名不滥升格”的正式律条件。

```json
{
  "verdict": {
    "request": "ε_crit升格评审 RUN03 fp 4ff0af8a824fd1c4",
    "decision": "REJECT_PROMOTION",
    "candidate": "ε_crit候选律v3",
    "from_level": "候选",
    "to_level": "正式",
    "promotion_satisfied": false,
    "summary": "扫描包四余项已闭环，证据支持 F1/F2 独立发现成立；但不支持 ε_crit候选律v3 升格为正式律。v3 当前表述混合了算法路径依赖量、算力预算界与代价尺度申报要求，缺少路径无关的 ε_crit 定义、上下界或判定协议，故按级名不滥原则否决升格。",
    "negative_result_registered": true,
    "dissent_registered": true
  },
  "evidence": {
    "run_id": "RUN03",
    "fingerprint": "4ff0af8a824fd1c4",
    "S1_multi_strategy": {
      "warm_start_factors": [0.3, 0.5, 0.7],
      "warm_start_result": "all_pass",
      "warm_start_rel_gap": "-2.7e-9",
      "cold_start_same_budget_result": "collapse",
      "cold_start_rel_gap": "-3.11e-01",
      "cold_start_marginal_error": "7.7e-2",
      "interpretation": "同预算下暖启动承重；冷启动崩溃。支持 F1。"
    },
    "S2_adversarial": {
      "high_dynamic_range": {
        "C": "10^U(-6,6)",
        "epsilon_1e-2": {
          "rel_gap": "+33.2%"
        },
        "epsilon_1e-3": {
          "rel_gap": "+4.7%"
        },
        "marginal_error_max": "6.5e-13"
      },
      "equal_cost": {
        "C": "C ≡ 1",
        "result": "熵正则精确选出 μ⊗ν",
        "diff": "0.0"
      },
      "near_degenerate": {
        "cost_gap": "5.0e-10",
        "result": "等于 LP"
      },
      "interpretation": "ε 必须相对代价尺度理解；高动态范围下 ε 绝对阈值不具尺度不变性。支持 F2。"
    },
    "S3_large_sparse": {
      "k": 64,
      "min_probability_mass": ["1.1e-19", "3.7e-16"],
      "epsilon": "1e-3",
      "rel_gap": "2.90e-08",
      "marginal_error": "4.78e-12",
      "iterations": 493200,
      "runtime_s": 94.1,
      "interpretation": "大规模稀疏下数值行为稳定，但计算预算显著影响可达 ε 区间。"
    },
    "S4_deep_dive": {
      "epsilon_1e-7": {
        "gap": "-4.42e-07"
      },
      "epsilon_1e-8": {
        "gap": "-2.53e-06"
      },
      "marginal_error_approx": "1e-6",
      "collapse_observed": false,
      "interpretation": "未出现崖式崩坏，但误差随 ε 收紧而增长，说明可达精度受预算与路径共同限制。"
    },
    "candidate_law_v3_claims": {
      "claim_1": "退火+暖启动路径下 ε_crit 是算力预算界，非表示界。",
      "claim_2": "ε 必须相对代价尺度申报。",
      "claim_3": "实现路径（含暖启动策略与预算）必须随判定一并申报，否则判定不可复现。",
      "observed_support": [
        "S1 支持暖启动承重与路径依赖",
        "S2 支持 ε 相对代价尺度",
        "S3/S4 支持预算影响可达精度"
      ],
      "missing_for_formal_law": [
        "未给出路径无关的 ε_crit 定义",
        "未给出 ε_crit 的可检验上下界或相变判据",
        "未给出跨实现路径的可复现申报协议与最小申报字段",
        "未证明该临界量不是单纯由退火调度/暖启动策略/预算参数共同定义的经验阈值",
        "未给出否证条件：何种实验会推翻 v3 的算力预算界解释"
      ]
    }
  },
  "findings": {
    "F1_warm_start_load_bearing": {
      "name": "暖启动承重",
      "status": "SUPPORTED",
      "evidence": [
        "S1: factor 0.3/0.5/0.7 暖启动全过，rel gap -2.7e-9",
        "S1: 同预算冷启动崩，gap -3.11e-01，边际误差 7.7e-2"
      ],
      "statement": "在相同预算下，退火是否由暖启动承重，是决定能否进入稳定 ε 区间的关键因素之一。",
      "independence": true,
      "registered": true
    },
    "F2_epsilon_scale_relative": {
      "name": "ε 尺度相对",
      "status": "SUPPORTED",
      "evidence": [
        "S2: C=10^U(-6,6) 时 ε=1e-2 rel gap +33.2%，ε=1e-3 rel gap +4.7%，边际误差≤6.5e-13",
        "S2: C≡1 时熵正则精确选出 μ⊗ν，diff 0.0",
        "S2: 近简并代价差 5.0e-10 时等于 LP"
      ],
      "statement": "ε 的绝对数值不能单独决定正则化效果；必须相对于代价尺度或代价差尺度申报和解释。",
      "independence": true,
      "registered": true
    },
    "F3_candidate_law_v3_not_formal": {
      "name": "ε_crit候选律v3不满足升格条件",
      "status": "REJECTED_FOR_PROMOTION",
      "reason": "级名不滥：候选律升正式需提供路径无关定义、可检验上下界/判据、跨路径申报协议与否证条件；当前证据只支持路径依赖经验现象。",
      "falsifiable_reasons": [
        {
          "id": "R1",
          "reason": "若两个不同实现路径在相同申报预算与相同代价尺度下给出显著不同的 ε_crit，则 v3 作为‘算力预算界’的正式律表述不成立。",
          "test": "固定 C 分布与预算，比较两组不同退火/暖启动策略，估计 ε_crit 并报告置信区间。"
        },
        {
          "id": "R2",
          "reason": "若 ε_crit 可由代价尺度、预算、维度和目标精度显式预测，而无需知道暖启动策略，则 v3 中‘实现路径必须随判定申报’不应作为正式律核心条件，而应降为实验协议注记。",
          "test": "做消融：隐藏暖启动策略，仅给预算/尺度/维度，训练或拟合 ε_crit 预测器；检验预测误差是否与给出路径时无显著差异。"
        },
        {
          "id": "R3",
          "reason": "若在固定预算下不存在稳定 ε_crit，而只有随迭代次数连续漂移的误差曲线，则‘临界律’升格为正式律不成立。",
          "test": "对多个预算档扫描 ε，使用变化点检测/置信区间检验是否存在可复现阈值；若无显著变化点，则否决正式律。"
        },
        {
          "id": "R4",
          "reason": "若 warm-start 因子在 0.3/0.5/0.7 之外、或随机暖启动下不保持承重效应，则 F1 的普适性受限，v3 不能以 F1 作为正式律支柱。",
          "test": "扩展 warm-start 因子至稀疏/随机/对抗初始化，重复 S1 同预算冷热对比。"
        }
      ]
    }
  },
  "promotion_gate": {
    "candidate_to_formal_requirements": [
      "路径无关或显式路径参数化的 ε_crit 定义",
      "可检验上下界或相变判据",
      "跨实现路径最小申报协议",
      "明确否证条件",
      "独立复现证据"
    ],
    "met": {
      "path_independent_definition": false,
      "testable_bounds_or_criterion": false,
      "minimal_reporting_protocol": false,
      "falsification_conditions": false,
      "independent_reproduction": "partial"
    },
    "conclusion": "不满足升格条件"
  },
  "registration": {
    "negative_result": {
      "registered": true,
      "content": "ε_crit候选律v3 未通过 RUN03 升格评审。"
    },
    "dissent": {
      "registered": true,
      "content": "若未来给出路径无关 ε_crit 定义、上下界与跨路径申报协议，可重新提交升格。"
    }
  },
  "recommendation": {
    "next_actions": [
      "保留 ε_crit候选律v3 为候选，不升正式。",
      "将 F1 暖启动承重、F2 ε尺度相对 作为独立发现入册。",
      "补充 R1-R4 中至少两项可检验实验。",
      "定义最小申报字段：代价尺度、预算、暖启动策略、退火调度、维度/稀疏度、ε、边际误差、rel gap、迭代数、运行时。",
      "若目标是正式律，需给出 ε_crit 的路径参数化公式或上下界，而非仅经验阈值。"
    ]
  }
}
```

简版判定：

- **问1：不满足级名不滥升格条件。** ε_crit候选律v3 只能算“路径依赖经验候选”，不能升正式。
- **问2：F1、F2 成立。** S1 支持暖启动承重；S2 支持 ε 必须相对代价尺度。
- **问3：否决理由可检验。** 关键否定理由是：v3 未给出路径无关 ε_crit 定义、可检验上下界/相变判据、跨路径申报协议与否证条件；并已列出 R1–R4 具体检验方案。

——cfts SI1语义轨·20261008T051555Z
