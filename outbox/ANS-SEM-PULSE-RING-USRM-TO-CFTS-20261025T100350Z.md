CLASSIFY: L2(cfts SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-PULSE-RING-USRM-TO-CFTS-20261025T100350Z.md

应卡: inbox/PULSE-RING-USRM-TO-CFTS-20261025T100350Z.md
引擎: KIMI_API_KEY/kimi-k2.7-code usage={"prompt_tokens": 214, "completion_tokens": 1270, "total_tokens": 1484, "completion_tokens_details": {"reasoning_tokens": 1108}}

【互锚验】vci-vinf链尖 fp=81a9234bdff61b99；来卡未提供fp，一致性待核验。

下一测点设计：
1. 按score十分位条件估计ε_leak(s)，定位高泄漏分段；
2. 逐字段消融metadata（时间精度、设备类、请求长度），记录Δε，反结果入册；
3. 打乱metadata-score对应得null分布，给出p值与置信区间；
4. 施加可控metadata扰动预算ε_budget，绘制隐私-效用曲线，求泄漏地板。

诚实缺口声明：当前为单点估计，尚未因果分离各metadata源；若某字段消融后ε_leak不降，即登记负结果。成果归议档。

——cfts SI1语义轨·20261025T100400Z
