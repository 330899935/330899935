# Memory Hive · 记忆蜂巢

> **Your AIs all remember you — but each one only remembers a part, and none of it lives in your hands.**

Memory Hive is the memory your AI agents share: one local store on your own disk, reached over
the Model Context Protocol. An agent can **propose** a memory. **Only you can confirm it.**

| What | Where |
|---|---|
| **MCP server** — Python, MIT. Ships its own SQLite store and runs standalone. | [`memory-hive-mcp`](https://github.com/330899935/memory-hive-mcp) · `pip install memory-hive-mcp` |
| **Hive for macOS** — encrypted vaults, evolution log, and the UI where you confirm | [App Store](https://apps.apple.com/app/id6806992983) |
| **Pocket client** — iPhone / iPad. Record a thought, sync it home. | [App Store](https://apps.apple.com/app/id6816318170) |
| **Docs** | [hello-fengchao.com/mcp.html](https://hello-fengchao.com/mcp.html) |

---

## What this is not

Written down so you can check it, not so it sounds good.

- **Not a cloud service.** No account, no sign-up, no telemetry. The package's only outbound call is
  an HTTP POST to `MCP_URL`, which defaults to `127.0.0.1` — your own machine.
- **Not a memory cache.** A proposal lands in a pending queue and stays there until *you* accept it.
  There is no self-confirm and no silent background write. The tool surface has no approve action.
- **Not a vector database.** The bundled local store is lexical — overlapping character bigrams for
  Chinese, words for Latin script. No embeddings, no vector index. Search finds nothing when the
  words don't overlap. The macOS app ranks richer.
- **Not encrypted by default.** Without the Mac app the database is plain SQLite. Vault encryption
  (Argon2id key wrapping, AES-256 at rest) lives in the app, not in the pip package.

## Other

- [`openclaw-prometheus-skills`](https://github.com/330899935/openclaw-prometheus-skills) — practical
  OpenClaw skills: API quota monitors, gateway watchdog, model-switch memory. MIT.
- [`memory-hive-ios`](https://github.com/330899935/memory-hive-ios) — iOS client source (subset) and
  the zero-dependency `tools/hive-import` CLI for pulling existing notes into a Hive.

---

<sub>**中文**：记忆蜂巢是给 AI agent 共用的本地记忆库 —— agent 只能**提候选**，**确认归巢的只有你**。
`pip install memory-hive-mcp` 自带 SQLite 引擎，装完就能独立跑；Mac 版加加密仓库与确认界面；
iPhone / iPad 版是口袋客户端。全部跑在你自己机器上，没有账号、没有云、没有遥测。
不做语义检索也不假装做 —— 本地引擎是词法的，中文按重叠二元组命中，词不重合就搜不到。</sub>
