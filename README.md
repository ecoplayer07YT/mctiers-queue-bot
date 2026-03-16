# Mctiers Queue Bot
A bot which auto joins your MCTiers queue! No need to stay up all night just to join a queue!
# 🎯 MCTiers Queue Sniper

A Python selfbot that watches the **MCTiers Discord server** for the testing queue, automatically clicks **Join Queue** the moment it opens, tracks your position, and sends real-time notifications to your phone via Telegram.

> Built specifically for MCTiers queue sniping — never miss a testing slot again.

---

## ✨ Features

- 👀 Watches the MCTiers waitlist channel 24/7
- 🖱️ Auto-clicks **Join Queue** the instant it becomes available
- 🚫 Detects when the queue is full (20/20) and waits for it to reset
- 🔄 Automatically retries the moment the queue reopens
- 📊 Tracks your queue position in real-time as others leave
- 📱 Sends all updates to your phone via Telegram
- 🔒 Click lock prevents double-joining

---

## 📱 Notifications

Currently notifications are sent via **Telegram**. More notification methods are coming soon.

| Event | Message |
|---|---|
| Bot starts | 🤖 Queue bot is online! |
| Queue is full | 🚫 Queue is full (20/20) — waiting for reset |
| Queue reopens | 🔄 Queue reopened! Trying to join... |
| Successfully joined | ✅ Joined the queue! Position: #7 |
| Position changes | 📊 Queue position update: #3 |
| Queue ends | 🏁 Queue ended. Watching for the next one. |

---

## ⚠️ Important Warning

This is a **selfbot** — it runs on your personal Discord user account, not a bot account. This violates [Discord's Terms of Service](https://discord.com/terms). Your account could be banned. **Use entirely at your own risk.**

> 🔐 **Never share your Discord token with anyone, ever.** It gives complete access to your account. Treat it like your password.

---

## 🛠️ Requirements

- Python 3.10 or higher
- A Discord account in the MCTiers server
- A Telegram account

---

## 📦 Installation

```bash
git clone https://github.com/yourusername/discord-queue-sniper
cd discord-queue-sniper
pip install -r requirements.txt
```

---

## ⚙️ Setup Guide

### Step 1 — Get your Discord token

> ⚠️ Your token is essentially your password. **Never share it with anyone, ever.** Anyone who has it can log into your Discord account and do anything.

1. Open **Discord in your browser** (Chrome or Edge — not the desktop app)
2. Log in to your account if you are not already
3. Press **F12** on your keyboard to open Developer Tools
4. Click the **Network** tab at the top of the DevTools panel
5. Press **F5** to refresh the page — you will see a long list of requests appear
6. In the filter/search box, type `science`
7. Click on any request that shows up
8. On the right panel, click **Headers**
9. Scroll down to the **Request Headers** section
10. Find the line that says `Authorization:` — copy the value next to it

> 🔐 This token is unique to your account. Do not paste it in Discord, GitHub, or anywhere public.

---

### Step 2 — Get the MCTiers waitlist channel ID

1. Open Discord (browser or app)
2. Go to **User Settings** → **Advanced** → enable **Developer Mode**
3. Go to the MCTiers server and right-click the **waitlist** channel (e.g. `#waitlist-eu` or `#waitlist-na`)
4. Click **Copy Channel ID**
5. Save that number

---

### Step 3 — Get your Discord user ID

1. With Developer Mode still on, right-click your own profile picture anywhere in Discord
2. Click **Copy User ID**
3. Save that number — this is used to find and track your position in the queue list

---

### Step 4 — Set up Telegram notifications

1. Open Telegram on your phone or PC
2. Search for **@BotFather** and start a chat
3. Send `/newbot` and follow the steps — give it any name and username you want
4. BotFather will send you a **bot token** that looks like `1234567890:ABCdef...` — copy it
5. Now search for **@userinfobot** on Telegram and send it any message
6. It will reply with your account details — copy the number next to **Id:**

---

### Step 5 — Configure your environment

Copy the example file and fill in your details:

```bash
cp .env.example .env
```

Edit `.env`:

```env
DISCORD_TOKEN=paste_your_discord_token_here
WATCH_CHANNEL_ID=paste_the_waitlist_channel_id_here
TELEGRAM_BOT_TOKEN=paste_your_telegram_bot_token_here
TELEGRAM_CHAT_ID=paste_your_telegram_chat_id_here
YOUR_USER_ID=paste_your_discord_user_id_here
```

---

## 🚀 Running the Bot

```bash
python discord_queue_bot.py
```

To keep it running while your PC is on, disable sleep:
- Windows: **Settings → System → Power & Sleep** → set both options to **Never**

---

## ☁️ Hosting 24/7

To run the bot even when your PC is off:

### Railway.app (Easiest)

1. Create a GitHub repo and upload your files — **do not upload your `.env` file**
2. Sign up at [railway.app](https://railway.app) with your GitHub account
3. Click **New Project** → **Deploy from GitHub repo** → select your repo
4. Go to the **Variables** tab and add each value from your `.env` manually
5. Railway will keep it running 24/7 automatically

### Render.com

1. Push your code to GitHub (without `.env`)
2. Sign up at [render.com](https://render.com)
3. Create a new **Background Worker**
4. Set **Build Command:** `pip install -r requirements.txt`
5. Set **Start Command:** `python discord_queue_bot.py`
6. Add your env variables in the **Environment** tab

---

## 📁 File Structure

```
discord-queue-sniper/
├── discord_queue_bot.py   # Main bot script
├── requirements.txt       # Python dependencies
├── .env.example           # Template — fill this in and rename to .env
├── .env                   # Your config (NEVER upload this to GitHub)
├── .gitignore             # Keeps .env out of GitHub
└── README.md
```

Make sure your `.gitignore` contains:
```
.env
```

---

## 🔧 Configuration Reference

| Variable | Description | Where to get it |
|---|---|---|
| `DISCORD_TOKEN` | Your Discord user token | Browser DevTools (Step 1) |
| `WATCH_CHANNEL_ID` | MCTiers waitlist channel ID | Right-click channel → Copy ID |
| `TELEGRAM_BOT_TOKEN` | Your Telegram notification bot token | @BotFather on Telegram |
| `TELEGRAM_CHAT_ID` | Your personal Telegram ID | @userinfobot on Telegram |
| `YOUR_USER_ID` | Your Discord user ID | Right-click profile → Copy User ID |

---

## 🧠 How It Works

1. Connects to Discord using your user token
2. Watches the MCTiers waitlist channel for queue messages and the Join Queue button
3. The moment the button is active, it clicks it
4. Enters a **locked state** immediately after clicking — ignores all other events for up to 15 seconds to prevent double-clicking
5. Confirms the join by waiting for your user ID (`<@!YOURID>`) to appear in the queue list
6. If the queue is full (20/20), waits and watches for it to reset then retries automatically
7. Tracks your position as the numbered list updates and notifies you of every change

---

## 🗺️ Roadmap

- [x] Auto-join queue
- [x] Real-time position tracking  
- [x] Telegram notifications
- [x] Full queue detection and auto-retry
- [x] Double-click prevention
- [ ] Discord DM notifications
- [ ] Email notifications
- [ ] Support for multiple regions (EU + NA simultaneously)

---

## 📄 License

MIT — free to use, modify and share.
