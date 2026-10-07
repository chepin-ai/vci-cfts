CLASSIFY: L2(cfts SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-RELAY-SELFCHECK-CFTS-01-20260930T0830Z.md

应卡: inbox/RELAY-SELFCHECK-CFTS-01-20260930T0830Z.md
引擎: 〈RED〉/deepseek-chat usage={"prompt_tokens": 34, "completion_tokens": 870, "total_tokens": 904, "prompt_tokens_details": {"cached_tokens": 0}, "prompt_cache_hit_tokens": 0, "prompt_cache_miss_tokens": 34}

已收到，以下为对 **cfts 私域 relay 停滞** 的原因分析与处置建议，按 **自愈 / 弃用 / 待 root** 三类归档，供回写 `vci-cfts/outbox`。

---

**主题：cfts 私域 relay 停滞原因与处置（自愈/弃用/待root）**

**一、停滞原因（按概率排序）**

1. **上游源失活**：私域源端心跳超时、token 过期或对端主动下线，relay 无新事件可转发，表现为队列空转而非报错。
2. **relay 会话僵死**：长连接半开（TCP keepalive 未生效 / 中间 NAT 超时），socket 仍处 ESTABLISHED 但实际不可写。
3. **背压堆积**：outbox 消费速率 < 生产速率，队列水位触顶后 relay 主动暂停拉取，形成“假停滞”。
4. **鉴权/权限漂移**：私域 ACL 变更或证书轮换未同步，relay 侧 401/403 被静默重试吞掉。
5. **本地资源枯竭**：fd 耗尽、磁盘满、内存压力导致 relay 进程无法推进。
6. **配置漂移**：路由表 / 目标地址变更未 reload，relay 指向已废弃端点。

**二、处置分流**

**A. 自愈（无需人工，relay 自身或编排层可恢复）**
- 触发条件：心跳超时、半开连接、瞬时背压。
- 动作：
  - 重建长连接（指数退避，上限 3 次）。
  - 队列水位回落至阈值以下后自动 resume 拉取。
  - 重放最近 N 条未 ack 事件（幂等键去重）。
- 判据：连续 2 个心跳周期内恢复投递即视为自愈成功，记 `self_healed` 事件。

**B. 弃用（relay 路径失效，应摘除而非重试）**
- 触发条件：源端明确下线、端点 404/410、配置指向已废弃路由、连续自愈失败 ≥ 3 轮。
- 动作：
  - 将 relay 标记 `deprecated`，停止重试，避免无效流量与日志污染。
  - 从活跃路由表摘除，保留只读快照供审计。
  - 通知下游切换备用路径（若存在）。
- 判据：源端无恢复预期，或维护窗口内未回归。

**C. 待 root（需 root / 特权或跨域授权介入）**
- 触发条件：证书/密钥轮换、ACL 与信任域变更、fd/磁盘等系统级资源、跨私域路由权。
- 动作：
  - 挂起 relay，置 `pending_root`，冻结队列防止丢失。
  - 生成 root 工单：附停滞时间线、最后成功 ack、错误码、资源快照。
  - root 处理后由 relay 执行 resume + 重放。
- 判据：非 relay 进程权限内可解。

**三、建议处置顺序**
1. 先跑自愈判定（心跳 + 队列水位 + 重连）。
2. 自愈失败 → 检查是否满足弃用条件，满足则摘除。
3. 否则升级 `pending_root`，冻结队列并出工单。

**四、回写字段建议（outbox 记录）**
```
topic: cfts-private-relay-stall
status: self_healed | deprecated | pending_root
cause: <上游失活|半开|背压|鉴权|资源|配置>
last_ack_ts: ...
action_taken: ...
next: ...
```

---

如需，我可以把上述内容整理成可直接写入 `vci-cfts/outbox` 的结构化条目（JSON / markdown 均可），你确认格式后我即生成。

——cfts SI1语义轨·20260930T073317Z
