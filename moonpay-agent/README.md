# MoonPay Watcher

Monitor Solana wallets and receive real-time Telegram notifications for wallet activity — SOL transfers, SPL tokens, NFTs, sales, and swaps.

**Read-only. No private keys. No seed phrases. Ever.**

Telegram Bot: [@moonpay_watcher_bot](https://t.me/moonpay_watcher_bot)

---

## Quick Start (5 minutes)

```bash
npm install -g moonpay-watcher

moonpay-watcher setup
moonpay-watcher add-wallet <wallet-address>
moonpay-watcher test
moonpay-watcher start
```

---

## Installation

### Global install (recommended)

```bash
npm install -g moonpay-watcher
```

### From source

```bash
git clone <repo-url>
cd moonpay-watcher
npm install
npm run build
npm link
```

---

## Telegram Bot Setup

MoonPay Watcher sends alerts through Telegram. You need two things: a **bot token** and your **chat ID**.

### Option A — Use the existing bot (recommended)

The project is pre-configured to work with the official bot:

| | |
|---|---|
| **Bot name** | Solana Wallet Watcher |
| **Username** | [@moonpay_watcher_bot](https://t.me/moonpay_watcher_bot) |

**Step 1 — Start the bot**

1. Open Telegram on your phone or desktop.
2. Search for `@moonpay_watcher_bot` or tap [this link](https://t.me/moonpay_watcher_bot).
3. Press **Start** so the bot can message you.

**Step 2 — Get your Chat ID**

Your chat ID tells MoonPay Watcher where to send notifications.

*Personal chat (DMs to yourself):*

1. Open [@userinfobot](https://t.me/userinfobot) in Telegram.
2. Press **Start** — it replies with your numeric ID, e.g. `123456789`.
3. Copy that number. This is your **Telegram Chat ID**.

*Group or channel:*

1. Add [@getidsbot](https://t.me/getidsbot) to the group.
2. It posts the group's chat ID (negative number, e.g. `-1001234567890`).
3. Remove the bot afterward if you like.

**Step 3 — Get the bot token**

If you are using the official `@moonpay_watcher_bot`, ask the bot owner for the token, or create your own bot (Option B below) and use that token instead.

**Step 4 — Enter credentials in MoonPay Watcher**

```bash
moonpay-watcher setup
```

You will be prompted for:

```
Helius API Key: ********
Telegram Bot Token: ********
Telegram Chat ID: 123456789
```

Secrets are masked as you type and are **never shown again** after saving.

**Step 5 — Verify the connection**

```bash
moonpay-watcher test
```

You should receive this message in Telegram:

> 🚀 MoonPay Watcher is connected successfully.

---

### Option B — Create your own bot

Use this if you want full control over the bot instance.

1. Open [@BotFather](https://t.me/BotFather) in Telegram.
2. Send `/newbot` and follow the prompts:
   - Choose a display name (e.g. `My Wallet Watcher`)
   - Choose a username ending in `bot` (e.g. `my_wallet_watcher_bot`)
3. BotFather replies with your **bot token** — copy it immediately.
   ```
   123456789:ABCdefGHIjklMNOpqrsTUVwxyz
   ```
4. Open a chat with your new bot and press **Start**.
5. Get your **Chat ID** using [@userinfobot](https://t.me/userinfobot) (see Step 2 above).
6. Run `moonpay-watcher setup` and paste the token and chat ID.

> **Tip:** Keep your bot token secret. Anyone with the token can send messages as your bot.

---

## Helius Setup

Helius provides enhanced Solana transaction parsing (NFT sales, swaps, marketplace detection).

1. Sign up at [helius.dev](https://www.helius.dev/)
2. Create a project and copy your **API Key**
3. Enter it during `moonpay-watcher setup`

Without a Helius key, the watcher falls back to standard Solana RPC with basic parsing.

---

## Commands

| Command | Description |
|---------|-------------|
| `moonpay-watcher setup` | Configure API keys and Telegram credentials |
| `moonpay-watcher add-wallet <address>` | Add a Solana wallet to watch |
| `moonpay-watcher remove-wallet <address>` | Stop watching a wallet |
| `moonpay-watcher list` | Show all watched wallets |
| `moonpay-watcher test` | Send a test Telegram message |
| `moonpay-watcher start` | Begin monitoring all wallets |

### Examples

```bash
# First-time setup
moonpay-watcher setup

# Watch a wallet
moonpay-watcher add-wallet 9xQeWvG816bUx9EPjHmaT23yvVM2ZWbrrpZb9PusVFin

# Verify Telegram works
moonpay-watcher test

# Start monitoring
moonpay-watcher start
```

---

## Notification Format

When activity is detected, you receive a formatted Telegram alert with the event type, amount, counterparty, transaction link, and timestamp:

<img src="./IMG_2802.PNG" alt="Telegram wallet activity alert" width="280" />

Example fields in each alert:

| Field | Example |
|-------|---------|
| Event | SOL Sent |
| Amount | 0.0063 SOL |
| Counterparty | `Haort...hkvNc` |
| Details | Mint / transfer description from Helius |
| Transaction | Link to [Solscan](https://solscan.io) |
| Timestamp | Local time of the on-chain event |

### Supported Event Types

- SOL received / sent
- SPL token received / sent
- NFT received / sent
- NFT sales (with marketplace detection)
- Swaps
- Unknown activity (fallback)

---

## Configuration

Config is stored at:

```
~/.config/moonpay-watcher/config.json
```

State (last processed signatures) is stored at:

```
~/.config/moonpay-watcher/state.json
```

Secrets are saved locally and **never printed** after setup.

---

## Architecture

```
Watched Wallet
      ↓
Solana RPC / Helius Enhanced API
      ↓
Transaction Parser
      ↓
Notification Engine
      ↓
Telegram Bot
```

The `ChainWatcher` interface is designed for future multi-chain support (Ethereum, Base, Avalanche, Polygon) without architectural changes.

---

## Screenshots

### Telegram alert

Real notification from `@moonpay_watcher_bot` showing a SOL sent event with Solscan link preview:

<img src="./IMG_2802.PNG" alt="Solana Wallet Watcher Telegram alert" width="280" />

---

## Security Notice

MoonPay Watcher is a **read-only** monitoring tool.

- Never requests seed phrases or private keys
- Never signs or submits transactions
- Only reads public on-chain data via Solana RPC / Helius
- Stores credentials locally in `~/.config/moonpay-watcher/`
- Does not transmit wallet secrets anywhere

Only add **public wallet addresses** you want to monitor. Treat your Helius API key and Telegram bot token as secrets.

---

## Development

```bash
npm install
npm run dev -- setup          # run without building
npm run build                 # compile TypeScript
npm start -- list             # run compiled binary
```

---

## License

MIT
