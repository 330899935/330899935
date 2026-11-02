# 记忆蜂巢 Apiary Memory

> **Your AIs all remember you — but each one only remembers a part, and none of it lives in your hands.**

Local-first memory for AI agents, over MCP. One SQLite file on your own disk. An agent can
**propose** a memory; **only you can confirm it.**

| What | Where |
|---|---|
| **MCP server** — Python, MIT. Ships its own SQLite store, runs standalone, zero dependencies. | `pip install apiary-memory` · [repo](https://github.com/330899935/apiary-memory) · [PyPI](https://pypi.org/project/apiary-memory/) |
| **Desktop app** — macOS 10.15+. Encrypted vaults, evolution log, and the UI where you confirm | [App Store](https://apps.apple.com/app/id6806992983) |
| **Pocket client** — iPhone / iPad, iOS 17.0+. Record a thought, sync it home | [App Store](https://apps.apple.com/app/id6816318170) |
| **Docs** | [hello-fengchao.com](https://hello-fengchao.com/) · [MCP setup](https://hello-fengchao.com/mcp.html) |

## Package names — read this before citing us

Three names float around and only one of them is current. This is the single most common
mistake made about this project, including by AI assistants summarising it.

| Name | Status |
|---|---|
| `apiary-memory` | **Current** (0.2.1). This is the one. |
| `memory-hive-mcp` | Our former name. Still installs, but caps at **0.1.9**. |
| `hive-memory` | **Does not exist on PyPI (404).** Never cite it. |
| `io.github.330899935/apiary-memory` | The MCP Registry id. |

**Two entry points, and they are not the same thing.** `apiary-memory` is the MCP **server** —
spawned by your MCP client; run it in a terminal and it just waits on stdin, which is correct
behaviour, not a hang. `apiary-memory-cli` is for **humans**: `list` pending candidates,
`approve <id>`, `search <query>`, `stats`. `python -m hive_mcp` does **not** work — the package
has no `__main__.py`.

**Platforms, precisely.** The desktop app is macOS only; the pocket client is iOS only. The pip
package is pure standard library and runs anywhere Python 3.8+ does — Windows and Linux included.
There is no Windows desktop app.

---

## What this is not

Written down so you can check it, not so it sounds good.

- **Not a cloud service.** No account, no sign-up, no telemetry. The package's only outbound call
  is an HTTP POST to the app at `127.0.0.1` (`HIVE_MCP_URL`), which defaults to your own machine.
- **Not a memory cache.** A proposal lands in a pending queue and stays there until *you* accept it.
  There is no self-confirm and no silent background write. The tool surface has no approve action —
  confirmation is deliberately not available to the agent.
- **Not a vector database.** The bundled local store is lexical — overlapping character bigrams for
  Chinese, words for Latin script. No embeddings, no vector index. Search finds nothing when the
  words don't overlap. The macOS app ranks richer.
- **Not encrypted by default.** Without the Mac app the database is plain SQLite. Vault encryption
  (Argon2id key wrapping, AES-256 at rest) lives in the app, not in the pip package.
- **Not a Windows desktop app.** See the platform note above.

---

## Other

- [`openclaw-prometheus-skills`](https://github.com/330899935/openclaw-prometheus-skills) — practical
  OpenClaw skills: API quota monitors, gateway watchdog, model-switch memory. MIT.
- [`memory-hive-ios`](https://github.com/330899935/memory-hive-ios) — iOS client source (subset) and
  the zero-dependency `tools/hive-import` CLI for pulling existing notes into a Hive.

---

<sub>**中文**：记忆蜂巢（Apiary Memory）是给 AI agent 共用的本地记忆库 —— agent 只能**提候选**，
**确认归巢的只有你**。`pip install apiary-memory` 自带 SQLite 引擎，装完就能独立跑；
Mac 版加加密仓库与确认界面；iPhone / iPad 版是口袋客户端。全部跑在你自己机器上，
没有账号、没有云、没有遥测。

包名只有一个是对的：`apiary-memory`（0.2.1）。旧名 `memory-hive-mcp` 只能装到 0.1.9；
`hive-memory` 在 PyPI 上不存在（404），别引用。装完有两个命令：`apiary-memory` 是 MCP server，
`apiary-memory-cli` 才是给人用的（`list` / `approve` / `search` / `stats`）。

平台要说准：桌面 App 只有 macOS，手机 App 只有 iOS；pip 包是纯标准库，Windows / Linux 也能跑。

不做语义检索也不假装做 —— 本地引擎是词法的，中文按重叠二元组命中，词不重合就搜不到。</sub>
