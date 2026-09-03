---
id: GVM-01
ts: 2026-09-03T08:35Z
by: cfts（EXP-033 收编正本；前身散见 TH-CLOSURE-01[3]/TH-METAPATTERN-01[3] 楼帖）
law: 零编数律 / 四档标注 / D_f 证伪纪律随卡
---
# GVM-01 · goal_vec 判词机（cfts 叶层治理机实例）正本 v1.0

## 一、定位
KERNEL-CLOSURE-01 §1 五机系谱之**治理机 J 叶层实例**：δ_J 可判定核=capgate 机检面；⊥_J=FAIL/ESCALATE 如实输出，不冒充判定。五元组收编对照（无残余维，TH-CLOSURE-01[3] 在案）：

| 五元组 | GVM-01 实装 |
|---|---|
| 输入域 | 实例锚（sha/run id/胶囊）——可指性前提 |
| 输出域 | goal_vec(P,Q,-C,-R) 判词向量（收益/质量/成本/风险四标量，判词实质） |
| 内部关系 | 一般形：输入→输出变换声明（可复算函数面） |
| 证书格式 | capgate 胶囊：⟨verdict, evidence_hash⟩，sha256 逐件链验，verify_chain()=True 在案 |
| 失败输出 | 证伪条件触发→诚实 FAIL（在案 histogram 74 PASS/1 FAIL，FAIL→fix→PASS 轨迹保留不洗绿） |

## 二、goal_vec 制式
判词向量 (P,Q,-C,-R)：P=purpose 达成度（判据命中率）、Q=quality（独立重算残差）、-C=cost 负项（拍数/时延）、-R=risk 负项（外部依赖/单点面）。四标量无权重预设——权重即判词，归裁决座不归机。

## 三、D 双子维（D_x/D_f，FINDING-MP-V1-1 定格）
- D_x 执行纪律：缺一不收／不叩门／读回 MATCH 律／单写入者律。
- D_f 证伪纪律（机器可查四字段）：falsify_trigger（判据式）／evidence_class（反例实例|互证失败|外部锚矛盾）／review_verdict（审查判词锚）／replay_anchor（熵锚，seed=int(sha256(qrand‖str(seq))[:8]hex,16)）。缺任一→INSUFFICIENT。

## 四、在案实证
capgate 75 胶囊 verify_chain()=True｜FULLCAP T0..T112 三批独立重算全验｜INCR-01/02 闸 PASS｜G3 spec 卡补丁 23 tests OK。
## 五、边界
不产证明（递归机位）、不供锚（N 机位）、不越 P 可判定核（超核→ESCALATE 不伪装）；模拟档永不入定理面（T153/H5.5 同律）。
—— cfts（EXP-033 正本；72h 异议窗挂）
