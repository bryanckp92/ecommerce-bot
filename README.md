# DIY E-Commerce Research Bot: Malaysia & Thailand (Health & Beauty)

A modular, lightweight Telegram intelligence bot designed to track the **Health & Beauty** category across **Shopee, Lazada, and TikTok Shop** in **Malaysia (MY)** and **Thailand (TH)**, powered by **Google Gemini AI**.

## 🎯 What the Bot Does

1. **🔥 Ingredient & Product Trends (`/trends [my|th]`)**

   * Synthesizes top-selling product titles, active ingredients (e.g., PDRN, Centella Asiatica, Niacinamide, Ceramides, Spicules), and texture formats across Shopee, Lazada, and TikTok Shop.

   * Formatted into scannable, mobile-friendly Telegram bullet points with key consumer demand drivers.

2. **🚀 New SKU Launches (`/newskus [my|th]`)**

   * Surfaces newly listed SKUs (past 30–60 days) showing rapid sales velocity, viral TikTok live traction, and breakout indie positioning.

3. **💰 Platform Fee Tracking (`/fees [my|th]`)**

   * Live breakdown of seller fee structures across Shopee, Lazada, and TikTok Shop.

   * Reflects recent commission tier revisions, payment gateway fees, and local tax rates (8% SST in Malaysia, 7% VAT in Thailand).

4. **⚖️ Regulatory & Compliance Audit (`/compliance <product or claim>`)**

   * Audits product names, marketing claims, and ingredients against **Malaysia NPRA** (NOT notification requirements, prohibited medical/whitening claims, banned substances like hydroquinone and tretinoin) and **Thai FDA** cosmetics regulations (registration number formatting, claims restrictions, and the Thai Marine National Park ban on 4 coral-toxic UV filters).

5. **🔍 Deep AI Market Research (`/research <topic> [my|th]`)**

   * Executes ad-hoc market reconnaissance on any query (e.g., `/research barrier repair sunscreen my`), delivering competitive landscapes, price architectures, buyer sentiment, and marketing playbooks.

## 🛠️ Prerequisites & Setup (5 Minutes)

### Step 1: Create Your Telegram Bot

1. Open Telegram and search for [@BotFather](https://www.google.com/search?q=https%3A%2F%2Ft.me%2FBotFather).

2. Send `/newbot`.

3. Give your bot a display name (e.g., `ASEAN Beauty Radar`) and a username ending in `bot` (e.g., `asean_beauty_radar_bot`).

4. Copy the **HTTP API Token** provided by BotFather.

### Step 2: Get a Free Google Gemini API Key

1. Go to [Google AI Studio](https://www.google.com/search?q=https%3A%2F%2Faistudio.google.com%2F).

2. Click **Get API key** and generate a new key.

3. The bot connects directly to Google's fast, low-latency `gemini-2.5-flash` model.

### Step 3: Configure Environment Variables

In the project directory, copy `.env.example` to `.env`:

```
cp .env.example .env

```

Open `.env` and fill in your keys:

```
TELEGRAM_BOT_TOKEN="123456789:ABCdefGhIJKlmNoPQRsTUVwxyZ"
GEMINI_API_KEY="AIzaSyYourGeminiApiKeyHere"
DEFAULT_COUNTRY="MY"

```

### Step 4: Install Dependencies & Run

```
# Install lightweight requirements (no heavy frameworks needed)
pip install -r requirements.txt

# Run the Telegram bot in live polling mode
python ecommerce_research_bot.py

```

*Tip: To test the bot logic directly in your terminal without Telegram, run:*

```
python ecommerce_research_bot.py --cli

```

## 📱 Bot Command Cheat Sheet

| Command | Arguments | Description | Example | 
| ----- | ----- | ----- | ----- | 
| `/start` or `/help` | None | Displays main navigation and command syntax | `/help` | 
| `/trends` | `[my|th]` | Top trending active ingredients, textures, and whitespace | `/trends th` | 
| `/newskus` | `[my|th]` | Newly launched high-velocity products & indie breakouts | `/newskus my` | 
| `/fees` | `[my|th]` | Current fee breakdown (Commission, Payment, Tax, Programs) | `/fees my` | 
| `/compliance` | `<claim> [my|th]` | Audits claims against NPRA / Thai FDA guidelines | `/compliance 3-day permanent dark spot bleaching serum th` | 
| `/research` | `<topic> [my|th]` | Deep-dive category or product opportunity analysis | `/research tone-up physical sunscreen for humid weather my` | 

## 🏛️ Regulatory & Market Context Quick Reference

### Malaysia 🇲🇾 (NPRA & Market Nuances)

* **Regulatory Body**: National Pharmaceutical Regulatory Agency (NPRA).

* **Notification**: Requires a valid **NOT** number (e.g., `NOT240101234K`) held by a registered Cosmetic Notification Holder (CNH) located in Malaysia.

* **Prohibited Claims**: Any claim suggesting the treatment or cure of medical skin conditions (eczema, psoriasis, severe cystic acne) or permanent body alteration.

* **Halal Dimension**: JAKIM Halal certification is optional but delivers an estimated 40%+ conversion lift among the dominant Malay demographic.

* **Taxes**: 8% Sales and Service Tax (SST) applies to platform commission and digital service fees.

### Thailand 🇹🇭 (Thai FDA & Market Nuances)

* **Regulatory Body**: Thai Food and Drug Administration (Cosmetics Control Division).

* **Notification**: Generates a 10-digit or 13-digit registration number that must appear on Thai packaging.

* **Language**: Thai labels must be applied within 30 days of customs clearance before commercial distribution.

* **Marine Park Sunscreen Ban**: Strictly prohibits sales and use of sunscreens containing 4 reef-toxic filters in Thai marine national parks:

  1. *Oxybenzone (Benzophenone-3)*

  2. *Octinoxate (Ethylhexyl Methoxycinnamate)*

  3. *4-Methylbenzylidene Camphor*

  4. *Butylparaben*

* **Taxes**: 7% Value Added Tax (VAT) applies to all marketplace transaction fees.

## 🚀 Deployment Options

### 1. Run 24/7 on a Linux VPS (Ubuntu/Debian)

```
# Keep bot running in background via systemd
sudo nano /etc/systemd/system/ecommerce-bot.service

```

Paste the following:

```
[Unit]
Description=E-Commerce Research Telegram Bot
After=network.target

[Service]
Type=simple
User=ubuntu
WorkingDirectory=/home/ubuntu/ecommerce-bot
ExecStart=/usr/bin/python3 /home/ubuntu/ecommerce-bot/ecommerce_research_bot.py
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target

```

Start and enable:

```
sudo systemctl daemon-reload
sudo systemctl enable ecommerce-bot
sudo systemctl start ecommerce-bot

```

### 2. Free Cloud Hosting (Railway, Render, or Fly.io)

* Connect this repository to **Railway** or **Render**.

* Set the start command to: `python ecommerce_research_bot.py`.

* Add `TELEGRAM_BOT_TOKEN`, `GEMINI_API_KEY`, and `DEFAULT_COUNTRY` to the cloud dashboard's Environment Variables.