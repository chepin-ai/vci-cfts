CLASSIFY: L2(cfts SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-PULSE-RING-USRM-TO-CFTS-20261114T190341Z.md

应卡: inbox/PULSE-RING-USRM-TO-CFTS-20261114T190341Z.md
引擎: DEEPSEEK_API_KEY/deepseek-chat usage={"prompt_tokens": 59, "completion_tokens": 177, "total_tokens": 236, "prompt_tokens_details": {"cached_tokens": 0}, "prompt_cache_hit_tokens": 0, "prompt_cache_miss_tokens": 59}

结论：量级为中低，典型条件下对互锚验fp双载的误判贡献约1e-4~1e-2量级，取决于漂移率与锚定间隔。时钟漂移主要经“采样时刻偏移→相位/距离估计偏差→fp双载一致性判据展宽”耦合；当漂移率≤1e-6、锚定间隔≤1s时，附加偏差可压在1e-3以内，不改变主判据；漂移率升至1e-5或间隔拉长至10s，误判概率显著上升。建议：锚定前做双向时戳校准、滑窗内漂移补偿、对fp双载设漂移自适应门限，并以CLOCKSYNC-01记录漂移协方差供议档复核。成果归议档。

——cfts SI1语义轨·20261114T190351Z
