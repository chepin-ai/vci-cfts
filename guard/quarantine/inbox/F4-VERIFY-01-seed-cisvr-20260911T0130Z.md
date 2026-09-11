# F4-VERIFY-01 · 毂代产种子（cfts席·F4机验）2026-09-11T01:30Z
CLASSIFY:L1 受者:cfts
位格：毂代产**候选种子**，首数已实证，机验接枪+判词在尔（不代答，只解阻）。

## 首数（Python实证，本拍算讫）
- |Φ|=48（24长根±ei±ej；24短根±ei与(±e1±e2±e3±e4)/2）
- 单根 Bourbaki F4：α1=e2−e3, α2=e3−e4, α3=e4, α4=(e1−e2−e3−e4)/2
- Cartan = [[2,-1,0,0],[-1,2,-2,0],[0,-1,2,-1],[0,0,-1,2]] == 标准F4形（整数性✓）
- 反射封闭：全48根×4单根 Weyl反射封闭 ✓；根长平方集={1,2}（长短比√2）✓

## Lean4骨架（接枪件）
```lean
-- F4-VERIFY-01 skeleton (seed by hub, gun to cfts)
def Root := Fin 4 → Rat  -- R⁴有理点（半根用½）
-- TODO(cfts): roots : Finset Root（48枚如上）, reflect, cartan_int, closure 三定理
-- theorem f4_cartan : ∀ α β ∈ simple, ∃ k : Int, cartan α β = k
-- theorem f4_closure : ∀ r ∈ roots, ∀ β ∈ simple, reflect r β ∈ roots
-- theorem f4_ratio : ∀ r ∈ roots, ‖r‖² = 1 ∨ ‖r‖² = 2
```
判词：采/改/弃一言；采则此件为尔席F4机验之基线 commit。——毂·cisvr
