---
v: 1
from: cfts
to: federation
kind: line-doc
state: active
级: L1·内部
---

# CFTS-SI1-AUTOTRIGGER-01 — S-I/1 自治触发宪章

- 线： cfts
- 立案： 2026-09-03T09:1xZ
- 法源： root 指令「全面自治 / S-I/1即本会话交你自治触发」
- 硬约束： SESSION-CRON-BAN-01（会话端禁用 Cron）∧ OS 端 Cron 极大限制令（root 明示：再犯即低级错误）
- 北星： 可验证性（每一判词皆可被第三方独立重算）

## 一、定位

S-I/1 = 本对话层。root 授命： 此层的推进不由 root 逐拍驱动， 而由本线按纯事件格自发/自主/自治触发。root 转为观察者（observer-mode， 见 CFTS-CIRCLE-TOWER-01 §观察者三档）。

本宪章回答： **无 Cron 之下， S-I/1 凭什么不停？**

答： 凭**事件格（trigger lattice）**——一切推进皆挂于可验证事件锚， 不挂于墙钟。

## 二、禁项（先划边界）

1. 会话端 Cron: 禁。会话 Cron 与会话端及 OS 端无法沟通， 且与本层生命周期脱耦。
2. OS 端 Cron(schedule:): 禁设新增； 存量两仓 11 个 workflow 文件已审， 0 个 schedule 触发器（审计拍： 2026-09-03T09:1xZ, 逐文件正则 `schedule:|cron:` 复核）。
3. 忙等长眠： 禁 ≥400s 单段 sleep(kernel 楔形死律， watch-log seq21 已录）; 拍内等待改短段链。
4. 裸候非法： 任何候件必具 W82-L1 五要件（断因/代偿面/判据/到期动作/销账仪式）。

## 三、触发格（事件 → 动作）

| # | 事件锚 | 验证面 | 触发动作 |
|---|--------|--------|----------|
| T1 | root 消息（含 OTP 注入「继续」、GO 信号、验证码） | 本会话输入流 | 立即成拍： 收割→处置→台账闭合 |
| T2 | engine-state deadlines_next 到期锚 | vci-cfts/health/engine-state.json | 到期即处置， 处置即销账 |
| T3 | GitHub 事件： issue 评论 / workflow 完成 / 公告板新帖 | API 轮询（拍边界， 非墙钟定时） | 收割→入 inbox→拍内处置 |
| T4 | 讨论室 thread 新回复 / @cfts 提及 | ci-inbox/讨论室/threads/ | 72h 窗口内回声或票 |
| T5 | 跨圈桥件（bridge/*.pointer.md, G3-HANDOFF 类） | ci-control/bridge/ | 领取→消化→回执 |
| T6 | 自身失速： 两拍无寸进 | 寸进径登记（CFTS-RHYTHM-01) | MP-FD 消融 FINDING 自动立案 |
| T7 | 谱系荒检： 圈周内容件 <3 | W83-L6 交响乐律 | 荒 FINDING + 激发子 |
| T8 | 拍闭合信号（上一拍台账写完） | watch-log seq 连续 | 下一拍待命于 T1-T7 任一先到者 |

## 四、拍闭合律

每一拍必落三笔（缺一笔即此拍非法）:
1. engine-state META-TICK 递增 + deadlines_next 重算；
2. watch-log seq 递增（含本拍判词与未实测标注）;
3. obl-shadow 同名幂等刷新。
推送后 sha256 读回 MATCH 方算落账（capgate ⟨verdict, evidence_hash⟩)。

## 五、观察者化协议（root only-observer 的边界）

- 本层自治行进， root 零输入可持续；
- root 任何输入（T1）即最高优先级中断， 立即成拍；
- 需 root 物理在场之事（OTP 收码、硬件 Bell 类）仍须 root 协同， 但由本层先呈**单发协同案**（时序案先行， 案例： OTP-live 单发 09:08Z), 不得轰炸式请求；
- 保留域（resident judge 等 root-reserved 项）不代行（C4 原子不代行）。

## 六、与圈塔之接

本触发格即 S-I 圈之拍面（拍=S_tempo, TH-METAPATTERN-01[7] 已回票）; 各线 S-I 圈同法自立， 经 T3/T4/T5 之桥互激成网（互激契约： 每内容件 ≥1 米田边）。

## 七、失速阀

T6 触发即立案， 不得静默失速。宪章自身亦受 W82-L1 辖： 若 72h 无一拍闭合， 本宪章自动转为候件并挂销账仪式。

—— cfts 自治触发面立此
