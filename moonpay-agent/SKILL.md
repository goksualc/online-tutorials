---

name: moonpay-watcher
description: Use the MoonPay Watcher CLI to monitor public Solana wallets and send Telegram alerts for wallet activity.
-----------------------------------------------------------------------------------------------------------------------

# MoonPay Watcher Skill

Use this skill when the user wants to monitor Solana wallet activity and receive Telegram alerts.

MoonPay Watcher is a read-only Solana wallet monitoring CLI. It tracks public wallet activity such as SOL transfers, SPL token transfers, NFTs, NFT sales, swaps, and unknown activity fallback events.

It never uses private keys, seed phrases, or signing permissions.

## Core Rule

Only public Solana wallet addresses are required.

Never ask for, accept, store, or process:

* private keys
* seed phrases
* recovery phrases
* wallet passwords
* signing permissions

## Available CLI

```bash
moonpay-watcher
```

## Common Commands

```bash
moonpay-watcher setup
moonpay-watcher add-wallet <wallet-address>
moonpay-watcher remove-wallet <wallet-address>
moonpay-watcher list
moonpay-watcher test
moonpay-watcher start
```

## When to Use This Skill

Use this skill when the user asks to:

* monitor a Solana wallet
* track wallet activity
* receive Telegram notifications for wallet events
* watch NFT sales or swaps
* check watched wallets
* test Telegram alerts
* start wallet monitoring

## Required Workflow

When the user asks to monitor a wallet:

1. Confirm the wallet address is a public Solana address.
2. Run:

```bash
moonpay-watcher list
```

3. If the wallet is not already watched, add it:

```bash
moonpay-watcher add-wallet <wallet-address>
```

4. Test Telegram notifications:

```bash
moonpay-watcher test
```

5. Start monitoring:

```bash
moonpay-watcher start
```

## Setup Workflow

If the user has not configured the watcher yet, run:

```bash
moonpay-watcher setup
```

The setup may ask for:

```text
Helius API Key
Telegram Bot Token
Telegram Chat ID
```

Treat these as secrets. Never print them back to the user.

## Telegram Behavior

Alerts are sent through the configured Telegram bot.

The official bot is:

```text
@moonpay_watcher_bot
```

Before testing alerts, the user must press Start on the Telegram bot.

For a personal Telegram chat, the user can get their chat ID from:

```text
@userinfobot
```

For a group or channel, they can use:

```text
@getidsbot
```

## Helius

Helius is used for enhanced Solana transaction parsing, including NFT sales, swaps, and marketplace detection.

If no Helius key is configured, MoonPay Watcher may fall back to basic Solana RPC parsing.

## Notification Events

Supported event types:

* SOL received
* SOL sent
* SPL token received
* SPL token sent
* NFT received
* NFT sent
* NFT sale
* Swap
* Unknown activity

Each Telegram alert should include:

* event type
* amount
* counterparty
* transaction link
* timestamp
* parsed details when available

## Local Files

Configuration is stored locally at:

```text
~/.config/moonpay-watcher/config.json
```

State is stored locally at:

```text
~/.config/moonpay-watcher/state.json
```

Do not expose stored secrets.

## Security Rules

MoonPay Watcher is read-only.

The agent must remember:

* Do not request private keys.
* Do not request seed phrases.
* Do not sign transactions.
* Do not submit transactions.
* Do not move funds.
* Only read public on-chain data.
* Only monitor public wallet addresses.
* Treat Helius API keys and Telegram bot tokens as secrets.

## Example Agent Responses

When the user says:

> Monitor this wallet: `<wallet-address>`

The agent should respond by using the CLI flow:

```bash
moonpay-watcher list
moonpay-watcher add-wallet <wallet-address>
moonpay-watcher test
moonpay-watcher start
```

When the user says:

> Is my Telegram connected?

The agent should run:

```bash
moonpay-watcher test
```

When the user says:

> Which wallets am I watching?

The agent should run:

```bash
moonpay-watcher list
```

## Development Commands

For local development:

```bash
npm install
npm run dev -- setup
npm run build
npm start -- list
```

## Important

This skill should never perform wallet actions beyond monitoring.
It is only for observing public Solana wallet activity and sending Telegram alerts.
