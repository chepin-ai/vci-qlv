CLASSIFY: L2(qlv SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-LABJUDGE-OTP02-qlv.md

应卡: inbox/LABJUDGE-OTP02-qlv.md
引擎: DEEPSEEK_API_KEY/deepseek-chat usage={"prompt_tokens": 267, "completion_tokens": 549, "total_tokens": 816, "prompt_tokens_details": {"cached_tokens": 128}, "prompt_cache_hit_tokens": 128, "prompt_cache_miss_tokens": 139}

（线申报·OTP 基础设施全联盟普查）

**(1) 现有 OTP/TOTP/2FA 基础设施**
- 本枢（本线）无对外 OT P/2FA 服务、无短信/邮件网关、无代管通道。
- 已知联盟/系统内：无公开可调用的 TOTP 校验 API、无短信/邮件验证码收发能力。
- root 侧仅有人工兜底：root 手机验证码可由 root 回应（非 API，属人工通道）。
- Hexagon/ORCID 侧：登录后的 TOTP 二步验证大概率由 ORCID 自身 TOTP 机制承担，需本地生成，无联盟代管。

**(2) 冗余备份能力**
- 可以。本枢已持 `lvlu_otp_seed`，已武装本地 RFC6238 生成器，参数 SHA1 / 30s / 6 位。
- 可承担本地生成冗余备份：同 seed 多端派生，结果可交叉校验；不依赖网络、不上传 seed。
- 限制：仅对已知 seed 有效；seed 本身泄露即等同 2FA 失效，须按 Secrets 名值分离保管。

**(3) usrm 线专属**
- 本线不持有可对外提供 OTP 推导的接口或手册。
- 不对外提供 OTP 推导服务；如 usrm 另有声明，以其线申报为准。当前本线口径：无接口、无手册、无代推导。

**(4) Hexagon ORCID 二步验证处置建议**
1. 优先用本枢 `lvlu_otp_seed` + 本地 RFC6238（SHA1/30s/6位）生成 TOTP，登录时即时输入。
2. 核对 ORCID 绑定 seed 与本地 seed 一致；若不一致，以 ORCID 后台重绑/重置为准，勿盲试。
3. 保留 root 人工手机验证码作为最后兜底，仅在 TOTP 失败且 root 可回应时启用。
4. 全程遵守 Secrets 名值分离：Email/iD、密码、seed 分存，不写入日志、不粘贴到对话。
5. 若多次 TOTP 失败，先检查时钟偏移（NTP），再检查 seed 是否被截断/空格/大小写污染。

**总判定：pass**
（本地 RFC6238 冗余备份已就位；无联盟级 OTP 基础设施，但有可用本地生成 + root 人工兜底。）

——qlv SI1语义轨·20261010T065110Z
