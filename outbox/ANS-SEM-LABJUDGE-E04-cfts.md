CLASSIFY: L2(cfts SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-LABJUDGE-E04-cfts.md

应卡: inbox/LABJUDGE-E04-cfts.md
引擎: DEEPSEEK_API_KEY/deepseek-chat usage={"prompt_tokens": 664, "completion_tokens": 3316, "total_tokens": 3980, "prompt_tokens_details": {"cached_tokens": 512}, "prompt_cache_hit_tokens": 512, "prompt_cache_miss_tokens": 152}

```json
{
  "verdict": {
    "request_id": "ε_crit升格评审第3轮 RUN04 fp 06d28aeae6b61fe4",
    "decision": "REJECT",
    "from": "candidate",
    "to": "formal",
    "summary": "六项否决理由虽已逐项实测闭环，且候选律v4较前轮显著增强，但尚不足以无条件升格为正式律。E4-1仅证明 Greenkhorn 族与 Sinkhorn 族在给定预算机制下三档 ε 的 gap 逐位一致，未消除两族共享作者/共享实现谱系导致的算法族级独立性缺口；E4-2的双控制能排除 naive 下的表示界并把 annealing 推离纯表示界，但尚不足以单独证明「退火路径非表示界」的强命题；E4-3的 36 跑消融支持「无路径申报则不可复现」，但「预测不需要路径」与「复现必须有路径」的二元性只在当前实验网格与误差口径下成立，尚非普适律。建议降格为 conditional formal / provisional formal，仅在显式适用域、路径与预算证书齐备时签发。",
    "allowed_next_states": [
      "candidate",
      "provisional_formal_conditional",
      "formal_restricted_domain"
    ],
    "not_allowed_next_states": [
      "unconditional_formal",
      "universal_law"
    ]
  },
  "evidence": {
    "E4_1_cross_implementation": {
      "observed": "Greenkhorn族 vs Sinkhorn族三档 ε gap 逐位一致：+2.31e-02 / +7.59e-03 / +1.96e-03；两族皆预算有界。",
      "supports": [
        "预算机制在跨族实现中表现稳定",
        "三档 ε 下数值一致性可复现"
      ],
      "gaps": [
        "算法族级独立不等于作者级独立",
        "Greenkhorn 与 Sinkhorn 在文献与实现谱系上可能共享相同归约、相同停止准则或相同数值封装",
        "未给出独立实现来源、独立代码库、独立作者或独立数值栈的审计证据"
      ],
      "finding": "PASS_WITH_QUALIFICATION"
    },
    "E4_2_representation_bound_exclusion": {
      "observed": {
        "naive_f64": "C∈[1,10], ε=1e-3, 全下溢 NaN",
        "naive_f80": "gap=0.0 精确",
        "annealing_f64": "gap +1.28e-11 ≈ f80 +1.29e-11",
        "controls": "双控制排除 tol 伪影"
      },
      "supports": [
        "naive 路径的失败可由表示界解释",
        "annealing 路径在当前实例上不表现为单纯表示界",
        "双控制降低 tol 伪影风险"
      ],
      "gaps": [
        "单实例或有限实例上的 f64≈f80 不足以证明「退火路径非表示界」为族级命题",
        "未系统扫描 C、ε、R、尺度、初值、停止准则以排除表示界在退火路径其他角落复现",
        "未证明退火路径在更宽精度阶梯（f32/f64/f80/f128）下 gap 收敛阶稳定",
        "双控制排除 tol 伪影，但不能排除实现细节或预算截断与表示误差耦合"
      ],
      "finding": "PASS_FOR_LOCAL_CLAIM / INSUFFICIENT_FOR_STRONG_CLAIM"
    },
    "E4_3_ablation_36_runs": {
      "observed": {
        "factor": "无可泛化预测信号 -7.3%",
        "same_k_R_B_across_factor": "中位 2.72 dex / 最大 9.06 dex 展布",
        "conclusion": "无路径申报则判定不可复现"
      },
      "supports": [
        "路径申报对复现性是必要信息",
        "同 (k,R,B) 下跨 factor 展布巨大，说明隐藏路径变量主导误差",
        "factor 本身不是可靠预测变量"
      ],
      "gaps": [
        "「预测不需要路径」仅在当前 factor 集合与误差口径下成立",
        "未证明存在一组可观测宏观量可替代路径进行可靠预测",
        "二元性可能是实验设计产物，而非律级结构",
        "36 跑网格覆盖有限，未给出路径变量空间覆盖度与遗漏变量审计"
      ],
      "finding": "PASS_WITH_QUALIFICATION"
    },
    "E4_4_explicit_upper_bound": {
      "observed": "log10(gap) = -0.405 + 1.594 log ε + 0.879 log R, R2=0.949；保守上界 gap ≲ 10^0.122 · ε^1.594 · R^0.879 覆盖 15/15 点。",
      "supports": [
        "在当前适用域内存在强经验上界",
        "15/15 覆盖提供初步保守性证据"
      ],
      "gaps": [
        "R2=0.949 为拟合优度，非有限样本覆盖保证",
        "15/15 点覆盖不足以给出高置信泛化界",
        "适用域退火族 / R∈[1,4] / ε∈[3e-3,1e-1] 外推风险高",
        "未给出残差分布、异方差、杠杆点与留一/留组验证"
      ],
      "finding": "PASS_IN_RESTRICTED_DOMAIN"
    },
    "E4_5_budget_curve": {
      "observed": "截断区 me 5.9e-3 → 6e-15 超幂律尾；外推保守：预测 1.0e-6 vs 实测 1.6e-7。",
      "supports": [
        "预算曲线存在超幂律尾",
        "当前外推方向保守"
      ],
      "gaps": [
        "单点外推保守不足以证明外侧普遍保守",
        "超幂律尾的机制未解释",
        "未给出预算证书的置信度与失效条件"
      ],
      "finding": "PASS_WITH_QUALIFICATION"
    },
    "E4_6_schema": {
      "observed": "eps-decl-schema v1 必填 eps_rel+scale+path+budget+err_metric；5/5 历史回填通过；缺 eps_rel 反例正确拒绝。",
      "supports": [
        "schema 可操作",
        "必填字段可强制路径与预算申报",
        "反例拒绝有效"
      ],
      "gaps": [
        "5/5 回填样本小",
        "schema 合规不等于科学可复现",
        "未验证 path/budget 字段的可审计性与最小充分性"
      ],
      "finding": "PASS_OPERATIONALLY"
    }
  },
  "findings": {
    "question_1": {
      "question": "六项否决理由（CLOSE-03采收）现已逐项实测闭环，v4是否满足级名不滥升格条件（候选→正式）？",
      "answer": "NO_UNCONDITIONAL_YES",
      "reason": "六项已闭环，但闭环强度不均。E4-1 存在作者级独立缺口；E4-2 仅支持局部非表示界；E4-3 二元性未证明为普适结构；E4-4 仅在限制域内成立。因此 v4 不满足无条件正式升格条件。",
      "recommended_action": "可升格为 provisional_formal_conditional 或 formal_restricted_domain；若坚持 unconditional formal，需补充作者级独立复现、精度阶梯扫描、路径变量覆盖度审计与外推验证。"
    },
    "question_2": {
      "question": "E4-2双控制实验设计是否足以支撑「退火路径非表示界」？",
      "answer": "PARTIALLY_SUFFICIENT",
      "reason": "双控制能排除 tol 伪影，并在当前实例上排除 naive 表示界、将 annealing 推离表示界。但「退火路径非表示界」是族级强命题，需要：多实例、多精度阶梯、参数扫描、独立实现、误差分解。当前证据足以支持「本实例上退火路径的 gap 不能归因于单纯 f64 表示下溢」，不足以支持无条件族级命题。",
      "required_additional_evidence": [
        "f32/f64/f80/f128 精度阶梯下 annealing gap 收敛阶稳定",
        "C、ε、R、尺度、初值、停止准则扫描",
        "独立实现复现",
        "表示误差与预算截断误差的分解实验"
      ]
    },
    "question_2b": {
      "question": "E4-3「预测不需要路径/复现必须有路径」二元性是否成立？",
      "answer": "CONDITIONALLY_TRUE",
      "reason": "在当前 36 跑网格、当前 factor 集合与当前误差口径下，factor 无可泛化预测信号，而同 (k,R,B) 跨 factor 展布巨大，支持「复现必须有路径」。但「预测不需要路径」是负命题，需证明不存在可观测替代变量；当前只证明给定 factor 不足，未证明无其他可观测宏观量可预测。二元性因此成立为实验域内条件命题，非普适律。",
      "required_additional_evidence": [
        "扩展 factor 集与路径变量空间覆盖",
        "尝试用可观测宏观量构建路径替代预测器",
        "报告遗漏变量敏感性与负结果置信区间"
      ]
    },
    "question_3": {
      "question": "若仍否决，给出可检验的具体否定理由。",
      "testable_rejection_reasons": [
        {
          "id": "R1",
          "reason": "E4-1 跨实现一致性未排除作者级/代码谱系级共享。",
          "test": "由至少两个无共享代码、无共享作者、无共享数值栈的独立团队，在相同 schema 下复现三档 ε gap；若仍逐位一致，则升级该证据。"
        },
        {
          "id": "R2",
          "reason": "E4-2 不足以支撑族级「退火路径非表示界」。",
          "test": "在 C∈[1,10]、ε∈[3e-3,1e-1]、R∈[1,4] 网格上，对 annealing 做 f32/f64/f80/f128 精度阶梯扫描；若 f64 与 f80 gap 相对差在所有点 ≤1e-9，且随精度阶收敛，则支持非表示界。"
        },
        {
          "id": "R3",
          "reason": "E4-3 二元性未证明「预测不需要路径」为普适负命题。",
          "test": "构造至少 10 个可观测宏观量候选预测器，在留组/留路径验证下若全部无法超过 factor 基线，则增强负命题；否则二元性降为局部现象。"
        },
        {
          "id": "R4",
          "reason": "E4-4 上界仅 15/15 点覆盖，外推保守性不足。",
          "test": "在适用域外至少两个 ε 与两个 R 点做前瞻预测并盲测；若全部被上界覆盖，则扩展适用域；否则维持限制域。"
        },
        {
          "id": "R5",
          "reason": "E4-5 预算证书按保守上界签发，但外侧普遍保守未证。",
          "test": "在截断区外推多点盲测，报告预测/实测比分布与失效阈值。"
        },
        {
          "id": "R6",
          "reason": "E4-6 schema 合规不等于科学可复现。",
          "test": "对 5/5 历史回填样本做第三方盲复现；若复现成功且 path/budget 字段经审计最小充分，则增强。"
        }
      ],
      "decision_if_unresolved": "REJECT unconditional formal; allow provisional_formal_conditional."
    },
    "candidate_law_v4_assessment": {
      "law_1_path_dependent_boundedness": {
        "status": "SUPPORTED_WITH_QUALIFICATION",
        "note": "naive=表示界、退火+暖启动=预算界，在当前证据下成立；固定判据下表示无关需限定适用域。"
      },
      "law_2_eps_rel_relative_declaration": {
        "status": "SUPPORTED",
        "note": "定义与值需随尺度申报，schema 已强制。"
      },
      "law_3_path_budget_mandatory": {
        "status": "SUPPORTED_WITH_QUALIFICATION",
        "note": "无路径则不可复现成立；不可降级为注记成立；但预测侧负命题需更多证据。"
      },
      "law_4_explicit_upper_bound": {
        "status": "SUPPORTED_IN_RESTRICTED_DOMAIN",
        "note": "适用域退火族/R∈[1,4]/ε∈[3e-3,1e-1]，外推须声明。"
      },
      "law_5_budget_certificate_conservative_upper_bound": {
        "status": "SUPPORTED_WITH_QUALIFICATION",
        "note": "当前外推保守，但普遍保守未证。"
      },
      "overall": "v4 可作为 provisional_formal_conditional 或 formal_restricted_domain 入册；不可作为 unconditional formal。"
    },
    "dissent_and_rejection_record": {
      "dissent": [
        "若评审方认为 E4-2 双控制已足够支撑退火路径非表示界，应将 R2 降为注记而非否定理由。",
        "若评审方认为 E4-3 的 36 跑已足够覆盖路径变量空间，可将二元性升为域内律。"
      ],
      "rejection": [
        "本判定否决 unconditional formal 升格。",
        "本判定允许 provisional_formal_conditional 或 formal_restricted_domain。",
        "本判定要求补充 R1-R6 中至少 R1、R2、R4 的可检验证据后，再议无条件正式升格。"
      ],
      "record_policy": "否决与异议同样入册，保留 RUN04 fp 06d28aeae6b61fe4 的完整审计轨迹。"
    }
  }
}
```

——cfts SI1语义轨·20261008T061434Z
