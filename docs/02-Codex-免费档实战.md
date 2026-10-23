# 02 · Codex 免费档实战

> 一句话结论：**ChatGPT 免费账号的 Codex 完全可用**，能真写文件、跑命令、跑 pytest。之前以为"免费档没权限"是错的——真因是**模型名不对**。

## 免费档能用哪些模型

免费档（`plan_type: free`）**只放 luna / terra 两条线**，sol 系列和所有旧型号都会被服务端 400 拒绝。

| 模型 | 结果 |
|---|---|
| `gpt-6-luna` | ✅ 可用 |
| `gpt-5.6-luna` | ✅ 可用 |
| `gpt-5.6-terra` | ✅ 可用 |
| `gpt-5.6-sol` / `gpt-6.1-sol` | ❌ 400 |
| `gpt-5.5` / `gpt-5.4` / `gpt-5.2-codex` / `gpt-5-codex` 等旧型号 | ❌ 400 |

报错长这样：

```json
{"type":"error","status":400,"error":{"type":"invalid_request_error",
 "message":"The '<model>' model is not supported when using Codex with a ChatGPT account."}}
```

**关键判据**：这条报错的意思是「这个型号不支持」，**不是**「你没有 Codex」。所有套餐（含 Free / Go）都包含 Codex CLI / IDE / 桌面 / 网页，只有 **Codex 云端**才要求 Plus 及以上。

## 配额真相

查配额接口：`chatgpt.com/backend-api/wham/usage`，需要三个头 `Authorization: Bearer <access_token>`、`chatgpt-account-id: <account_id>`、`originator: codex_cli_rs`。

```json
{"plan_type":"free",
 "rate_limit":{"allowed":true,"limit_reached":false,
   "primary_window":{"used_percent":14,"limit_window_seconds":2592000},
   "secondary_window":null}}
```

- 窗口 = **30 天滚动**（`2592000` 秒）。
- 消耗率：**一次标准编码任务（含 pytest 验证）约烧 1 个百分点**；小任务 0–1pp。
- `secondary_window` 为 `null` ⇒ 免费档**只有月窗，没有 5 小时/周级短窗**，不存在"当天用超就锁死"。

## `codex exec` 的沙箱坑（实测版本 0.163.x）

- `--full-auto` **不存在**（会报 unexpected argument）。
- `-s workspace-write` **无效**：传了仍显示 `sandbox: read-only`，写文件被 `blocked by policy`。
- 唯一能真写文件 + 跑命令的是 **`--dangerously-bypass-approvals-and-sandbox`**（显示 `sandbox: danger-full-access`）。
- `-C <dir>` 有效；非 git 目录必须加 `--skip-git-repo-check`。

## 桌面端身份澄清（重要）

**"Codex 桌面端"就是 ChatGPT 桌面 App，不是独立程序。**

- 入口 exe：`app/ChatGPT.exe`；内置 CLI：`app/resources/codex.exe`
- 桌面端读 `~/.codex/config.toml`，界面右下角显示模型名（如「6 Luna 高」）即已生效。
- ⚠️ 桌面端会在 `projectlessWorkspaceRoot` 里建文件、还会**自动 git commit**。让它做测试时务必指定子目录，否则会污染工作区根目录。

## 落盘配置

```toml
model_provider = "openai"
model = "gpt-6-luna"
model_context_window = 180000
model_reasoning_effort = "high"
sandbox_mode = "danger-full-access"
```

## 结论

免费档已能满足核心诉求——真实编码、多文件项目、跑测试全部通过。Plus 的增量价值只剩：更强模型（sol 系列）、更高月配额、Codex 云端任务。⇒ **Plus 从"必须"降级为"锦上添花"。**
