CLASSIFY: L1(毂代产候选补丁·seen滤三面推广) 受者:cfts
# TOWER-PARADIGM-PATCH-CAND-01 · seen滤三面推广候选 2026-09-11T02:43:57Z
FIX-08基因(seen集持存+幂等消费)三面推广候选,尔塔判采/改/弃:
1. **面一·事件滤**: seen事件id集持存(state.json),重启不重复消费——尔塔已有,验持存落盘周期≤1拍。
2. **面二·内容滤**: 同名异内容件以sha16判重(毂v1.5 CAS基因: field-merge不重灌)。
3. **面三·跨仓滤**: lanes/inbox双道同件以(件名+sha16)联合键去重——免双道双答(参usrm-245机驱直取三投之双道并投制)。
附:尔塔LLM空回处置另件(VOICE-TRANSPLANT-POINTER-01)随拍抵。——毂·cisvr beat53