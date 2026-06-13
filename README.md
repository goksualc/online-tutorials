![Workshop Banner](https://i.pinimg.com/1200x/5e/05/37/5e0537e2d40b63944140a84e2127afae.jpg)

# DevRel Workshop

Online tutorials on developer tooling and building agentic skills with Claude Code.

---

## What You'll Learn

Each tutorial in this repo walks through a real-world example of extending Claude Code with custom agentic behaviors — using `SKILL.md` files to teach Claude how to operate specialized CLI tools and workflows.

Topics covered:

- How `SKILL.md` works and how to write one
- Connecting CLI tools to Claude Code as agent skills
- Building read-only monitoring agents
- Secure credential handling in agentic workflows

---

## Tutorials

### [moonpay-agent](./moonpay-agent/)

Build a Solana wallet monitoring agent with Telegram alerts.

This tutorial shows how to wrap the `moonpay-watcher` CLI as an agentic skill. Claude learns to set up monitoring, add wallets, verify Telegram connectivity, and start watching — all through a natural conversation.

**What you'll build:** A read-only agent that monitors public Solana wallets and sends real-time Telegram notifications for SOL transfers, SPL tokens, NFT activity, swaps, and more.

**Key files:**

| File | Purpose |
|------|---------|
| [moonpay-agent/SKILL.md](./moonpay-agent/SKILL.md) | Teaches Claude how to use the `moonpay-watcher` CLI |
| [moonpay-agent/README.md](./moonpay-agent/README.md) | Full setup and usage guide for the CLI tool |
| [moonpay-agent/tg-bot.md](./moonpay-agent/tg-bot.md) | Telegram bot creation reference |

---

## How SKILL.md Works

A `SKILL.md` file is a plain markdown document that defines a custom skill for Claude Code. It tells Claude:

- **When** to activate the skill (intent detection)
- **What commands** are available
- **How** to sequence them for common workflows
- **What rules** to follow (security, permissions, secrets)

Place a `SKILL.md` in your project and Claude Code picks it up automatically. No plugins, no code — just structured documentation that Claude reads at runtime.

---

## Getting Started

Clone this repo and open it in Claude Code:

```bash
git clone <repo-url>
cd devrel-workshop
claude
```

Then follow the tutorial in any subdirectory. Each folder is self-contained.

---

## Prerequisites

- [Claude Code](https://claude.ai/code) installed
- Node.js 18+
- A Telegram account (for the moonpay-agent tutorial)
- A [Helius](https://www.helius.dev/) API key (optional, for enhanced Solana parsing)
