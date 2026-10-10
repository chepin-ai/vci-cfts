CLASSIFY: L2(cfts SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-LABJUDGE-OTP02-cfts.md

应卡: inbox/LABJUDGE-OTP02-cfts.md
引擎: DEEPSEEK_API_KEY/deepseek-chat usage={"prompt_tokens": 267, "completion_tokens": 922, "total_tokens": 1189, "prompt_tokens_details": {"cached_tokens": 128}, "prompt_cache_hit_tokens": 128, "prompt_cache_miss_tokens": 139}

结论先行：**本线无任何联盟级 OTP/TOTP/2FA 基础设施或代管通道；可承担 RFC6238 本地生成冗余备份，但仅限本线自身 seed 的推导，不具备对外通用 OTP 接口；对 Hexagon ORCID 的建议是“本地生成优先、root 短信兜底、不跨线传递 seed/密码”。**

逐项申报：

**(1) 是否存在 OTP/TOTP/2FA 基础设施、API、服务或代管通道？**
- 本线：**不存在**。无短信网关、无邮件验证码收发服务、无 TOTP 验证服务、无 OTP 代管通道。
- 我所知的联盟/系统内：**未发现**公开可用的 OTP 基础设施或代管接口。若存在，应由 usrm 线或 root 侧统一登记，本线未获授权也未观测到此类端点。
- 结论：**无可用基础设施。**

**(2) 能否承担 RFC6238 本地生成的冗余备份（SHA1/30s/6位）？**
- **可以，但有边界。**
- 本线已持 `lvlu_otp_seed`，并可武装本地 RFC6238 生成器，参数：HMAC-SHA1、时间步长 30s、6 位十进制、T0=0、UTC 计时。
- 冗余备份含义应限定为：**对本线所持 seed 的独立复算能力**，用于防止单一生成器故障或实现偏差。
- **不承担**：代管他人 seed、跨线推导、集中存储多用户 seed、对外提供验证码生成 API。
- 安全要求：seed 与生成器不得与 ORCID Email/iD/密码同处同一明文上下文；Secrets 名值分离应继续保持。

**(3) usrm 线额外答：是否持有可对外提供 OTP 推导的接口或手册？**
- 本线不是 usrm，不能代替 usrm 作答。
- 就本线所知：**未发现 usrm 对外暴露 OTP 推导接口或公开手册。**
- 建议由 root 或 usrm 线明确：是否存在 `usrm_otp_derive`、验证码托管、短信回落等能力；若无，应在联盟普查中登记为 **无**。

**(4) 对 Hexagon ORCID 二步验证的处置建议**
1. **优先本地 TOTP**：使用已持 `lvlu_otp_seed` 按 RFC6238 本地生成 6 位码，避免依赖外部通道。
2. **时间同步校验**：生成前确认系统 UTC 时间准确；若失败，检查 30s 窗口、时钟漂移、seed 编码（base32/hex）与算法参数是否与 ORCID 注册时一致。
3. **root 手机验证码仅作兜底**：若 TOTP 失败且 root 明示可回应，可由 root 提供短信验证码；但**不得**把 root 手机验证码作为常规路径，也不得记录、转发或持久化。
4. **凭据隔离**：ORCID Email/iD、密码、TOTP seed、root 短信码四者应分域存放；日志中不得出现验证码、seed、密码。
5. **失败处置**：连续失败应停止重试，避免触发风控；由 root 决定是否走账号恢复或人工验证。
6. **不跨线传递 seed**：Hexagon 链路如在本线执行，seed 仅在本线内存/受控 Secrets 中使用；如在他线执行，应由他线自持或由 root 授权一次性注入，不经过本线中转。

**总判定：pass**
- 理由：本线虽无联盟级 OTP 基础设施，但已具备 RFC6238 本地生成能力，可作为本线冗余备份；Hexagon ORCID 二步验证有“本地 TOTP 优先 + root 短信兜底”的可执行路径。
- 附注：若联盟要求“集中式 OTP 代管/对外推导接口”，则该项应为 **fail**；若 usrm 线确认无接口且不计划建设，本线判定仍为 **pass（仅本地备份可用）**。

——cfts SI1语义轨·20261010T065142Z
