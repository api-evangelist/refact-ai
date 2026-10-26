# Refact.ai (refact-ai)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Refact.ai is an open-source, local-first AI coding assistant and autonomous software-engineering agent built by Small Magellanic Cloud Ai Ltd. ("SmallCloud"). The product combines an IDE-integrated chat experience (Ask / Explore / Debug / Review / Plan / Agent modes), accurate code completion powered by Qwen2.5-Coder with RAG over the workspace, and the Refact Agent — an autonomous mode that plans, executes, and iterates on engineering tasks end-to-end, integrating with Git hosts, databases, shells, browsers, and MCP servers. The full agent stack — a Rust HTTP/LSP engine (`refact-lsp`), a React/Vite chat GUI, and VS Code + JetBrains plugins — is open source under BSD-3-Clause at [github.com/smallcloudai/refact](https://github.com/smallcloudai/refact) and is currently ranked #1 open-source agent on SWE-bench Lite (60.0%) and 93.3% on Aider's Polyglot benchmark with thinking mode.

**URL:** [Visit APIs.json](https://raw.githubusercontent.com/api-evangelist/refact-ai/refs/heads/main/apis.yml)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags

- AI, Artificial Intelligence, Coding Assistant, AI Agent, Autonomous Agents, Code Completion, Code Generation, Developer Tools, IDE, VS Code, JetBrains, Self-Hosting, On-Premise, Open Source, LSP, MCP, Model Context Protocol, Fine-Tuning, SWE-Bench, RAG

## Timestamps

- **Created:** 2026-05-25
- **Modified:** 2026-05-25

## APIs

### Refact Agent Engine API

Local HTTP/LSP API exposed by the Rust `refact-lsp` engine that runs inside the user's IDE or as a standalone server. Implements the agent runtime: provider/model capabilities, chat command queueing, SSE event streams, code completion, tool registry and confirmation rules, AST indexing, RAG/vector search over the workspace, integrations configuration, knowledge graph operations, task board management, and workspace checkpoint/rollback. The VS Code and JetBrains plugins and the React GUI all call this contract over `http://127.0.0.1:<port>/v1`.

Documented route groups under `/v1` include:

- `/ping`, `/caps` — health and capabilities discovery
- `/chats/{id}/commands`, `/chats/subscribe` — chat command queueing and SSE event streams
- `/code-completion` — completion requests
- `/tools`, `/tools-check-if-confirmation-needed` — tool registry and confirmation
- `/ast-status`, `/ast-file-symbols` — AST indexing
- `/rag-status`, `/vecdb-search` — semantic search over the workspace
- `/integrations` — provider, MCP, GitHub/GitLab, DB, Docker integration config
- `/knowledge/*`, `/knowledge-graph` — long-term memory and knowledge ops
- `/tasks/*` — agent task board
- `/checkpoints-preview`, `/checkpoints-restore` — workspace rollback

**Human URL:** [https://docs.refact.ai](https://docs.refact.ai)

- [Documentation](https://docs.refact.ai)
- [Engine source code](https://github.com/smallcloudai/refact/tree/main/refact-agent/engine)
- [Monorepo](https://github.com/smallcloudai/refact)

### Refact MCP Integration

Refact Agent acts as an MCP (Model Context Protocol) client, attaching local or remote MCP servers (`npx`, Python `-m`, `docker run`, or remote SSE) into the agent's tool surface with per-tool confirmation rules. This makes any MCP server an extension of Refact's capability set inside the IDE.

**Human URL:** [https://docs.refact.ai/features/autonomous-agent/integrations/mcp/](https://docs.refact.ai/features/autonomous-agent/integrations/mcp/)

- [MCP Integration Documentation](https://docs.refact.ai/features/autonomous-agent/integrations/mcp/)
- [Model Context Protocol](https://github.com/modelcontextprotocol)

## Pricing

| Plan | Price | Notes |
|---|---|---|
| Free | $0 | Limited daily agent usage, 32k context chat, unlimited completions |
| Pro | $10 / month | 40 agent requests/day, 64k context, premium models, Think Mode |
| Enterprise | Contact | On-premise, fine-tuning on customer code, SSO, dedicated support |
| BYOK | Your provider's rates | Bring your own Anthropic / OpenAI / Gemini / xAI / DeepSeek / Groq / OpenRouter / Copilot key |
| Self-Hosted | Free (BSD-3) | Run the open-source stack on your own infra; pay only for the models you choose |

> Note: Refact Cloud is being wound down — BYOK and self-hosting are now the recommended paths.

## Supported Models

**Cloud agent / chat:** GPT-4.1 (default), Claude 3.7 Sonnet, Claude 3.5 Sonnet, GPT-4o, GPT-4o-mini, o3-mini.

**Code completion:** Qwen2.5-Coder-1.5B.

**BYOK providers:** Anthropic, OpenAI, Google Gemini, xAI Grok, DeepSeek, Groq, OpenRouter, GitHub Copilot, plus any OpenAI-compatible endpoint.

**Local/self-hosted providers:** Ollama, LM Studio, vLLM, custom OpenAI-compatible endpoints.

**Self-hosted fine-tunable models:** Refact, StarCoder, DeepSeek-Coder, CodeLlama variants (20+ options across completion and chat).

## Open-Source Repositories

| Repo | Language | Description |
|---|---|---|
| [smallcloudai/refact](https://github.com/smallcloudai/refact) | Rust / TypeScript / Kotlin | Monorepo — engine, GUI, VS Code & JetBrains plugins, docs (BSD-3-Clause) |
| [smallcloudai/refact-bench](https://github.com/smallcloudai/refact-bench) | Dockerfile | SWE-Bench benchmarking harness for coding agents |
| [smallcloudai/rust-sdk](https://github.com/smallcloudai/rust-sdk) | Rust | MCP Rust SDK (fork of modelcontextprotocol/rust-sdk) |
| [smallcloudai/litellm](https://github.com/smallcloudai/litellm) | Python | LiteLLM proxy fork |
| [smallcloudai/refact-vscode](https://github.com/smallcloudai/refact-vscode) | TypeScript | VS Code plugin (archived — now in monorepo) |
| [smallcloudai/refact-intellij](https://github.com/smallcloudai/refact-intellij) | Kotlin | JetBrains plugin (archived — now in monorepo) |

## IDE Distribution

- [Refact for VS Code (Marketplace)](https://marketplace.visualstudio.com/items?itemName=smallcloud.codify)
- [Refact for JetBrains (Plugin Marketplace)](https://plugins.jetbrains.com/plugin/20647-refact-ai)
- Visual Studio, Neovim, and Sublime Text plugins documented at [docs.refact.ai](https://docs.refact.ai)
- [AWS Marketplace listing](https://aws.amazon.com/marketplace/seller-profile?id=seller-zb3svnusgaibm) for enterprise EC2 deployment

## Common Resources

- [Website](https://refact.ai)
- [Documentation](https://docs.refact.ai)
- [Quickstart](https://docs.refact.ai/introduction/quickstart/)
- [Enterprise](https://refact.ai/enterprise/)
- [Pricing](https://refact.ai/pricing)
- [Blog](https://refact.ai/blog/)
- [Contact / Demo](https://refact.ai/contact/)
- [Sign Up / Sign In](https://refact.smallcloud.ai/)
- [GitHub Organization](https://github.com/smallcloudai)
- [Discord](https://www.smallcloud.ai/discord)
- [Twitter / X](https://twitter.com/refact_ai)
- [LinkedIn](https://www.linkedin.com/company/smallcloud)
- [YouTube](https://www.youtube.com/@refactai)

## Maintainers

- **Kin Lane** — [kin@apievangelist.com](mailto:kin@apievangelist.com) — [@apievangelist](https://twitter.com/apievangelist) — [apievangelist.com](https://apievangelist.com)
