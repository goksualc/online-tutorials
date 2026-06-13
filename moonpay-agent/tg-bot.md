# Telegram Bot Setup

This guide covers everything you need to connect MoonPay Watcher to Telegram.

---

## Prerequisites

- A Telegram account (mobile or desktop)
- Access to [@BotFather](https://t.me/BotFather) — Telegram's official bot management service

---

## Step 1 — Create a Bot

1. Open Telegram and start a chat with [@BotFather](https://t.me/BotFather).
2. Send the command:
   ```
   /newbot
   ```
3. Choose a **display name** for your bot (e.g. `My Wallet Watcher`).
4. Choose a **username** — must end in `bot` (e.g. `my_wallet_watcher_bot`).
5. BotFather replies with your **bot token**:
   ```
   123456789:ABCdefGHIjklMNOpqrsTUVwxyz
   ```
6. Copy the token immediately and store it somewhere safe.

> **Security:** Treat your bot token like a password. Anyone who has it can send messages as your bot. Never commit it to source control or share it publicly.

---

## Step 2 — Get Your Chat ID

MoonPay Watcher needs your Chat ID to know where to deliver notifications.

### Personal chat (recommended for most users)

1. Open [@userinfobot](https://t.me/userinfobot) in Telegram.
2. Press **Start**.
3. The bot replies with your numeric user ID, for example:
   ```
   123456789
   ```
4. This number is your **Telegram Chat ID**.

### Group or channel

1. Add [@getidsbot](https://t.me/getidsbot) to the group or channel.
2. It posts the chat ID — groups use a negative number, for example:
   ```
   -1001234567890
   ```
3. Copy the ID, then remove the bot if you no longer need it.

---

## Step 3 — Activate Your Bot

Before MoonPay Watcher can message you, you must start a conversation with the bot:

1. Search for your bot by username in Telegram.
2. Open the chat and press **Start**.

This step is required. Telegram does not allow bots to initiate conversations with users who have not started them first.

---

## Step 4 — Configure MoonPay Watcher

Run the setup command and enter your credentials when prompted:

```bash
moonpay-watcher setup
```

```
Helius API Key:      ••••••••
Telegram Bot Token:  ••••••••
Telegram Chat ID:    123456789
```

Credentials are masked as you type and are never displayed again after saving.

---

## Step 5 — Verify the Connection

```bash
moonpay-watcher test
```

If everything is configured correctly, you will receive this message in Telegram:

> 🚀 MoonPay Watcher is connected successfully.

If the message does not arrive, check that you pressed **Start** on the bot (Step 3) and that the Chat ID matches the account you used.

---

## Troubleshooting

| Symptom | Likely cause | Fix |
|---------|-------------|-----|
| No test message received | Bot not started | Open the bot in Telegram and press **Start** |
| `Forbidden` error in logs | Wrong chat ID | Re-run `moonpay-watcher setup` with the correct ID |
| `Unauthorized` error in logs | Invalid bot token | Regenerate token via `/token` in @BotFather |
| Messages go to wrong chat | Chat ID mismatch | Confirm your ID with @userinfobot |

---

## Using the Official Bot

If you prefer not to create your own bot, MoonPay Watcher is pre-configured to work with the official instance:

| | |
|---|---|
| **Bot name** | Solana Wallet Watcher |
| **Username** | [@moonpay_watcher_bot](https://t.me/moonpay_watcher_bot) |

Start the bot, get your Chat ID from @userinfobot, then request the shared bot token from the project maintainer.

---

## Reference

| Resource | Link |
|----------|------|
| BotFather | [t.me/BotFather](https://t.me/BotFather) |
| Get personal chat ID | [t.me/userinfobot](https://t.me/userinfobot) |
| Get group/channel ID | [t.me/getidsbot](https://t.me/getidsbot) |
| Official bot | [t.me/moonpay_watcher_bot](https://t.me/moonpay_watcher_bot) |
| Telegram Bot API docs | [core.telegram.org/bots/api](https://core.telegram.org/bots/api) |
