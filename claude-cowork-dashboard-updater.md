# Claude Cowork — Daily Dashboard Data Generator

## What This Does

Every day at **9:00 PM GMT+7**, you generate a fresh `ai-data.json` file in `/STOCK and Finances/`. This file powers the Portfolio News Dashboard — it provides the market overview bar, market sentiment banner, and AI TLDR analysis for every holding.

---

## Step-by-Step Instructions

### Step 1: Read the Portfolio

Read `/STOCK and Finances/portfolio.md` to get the current holdings. The default tickers are:

| Symbol | Company | Sector |
|--------|---------|--------|
| BTCUSD | Bitcoin / USD | Crypto |
| RKLB | Rocket Lab | Space/Aerospace |
| SATS | EchoStar Corp | Satellite/Telecom |
| TE | T1 Energy | Energy |
| STX | Seagate Tech | Tech/Storage |
| TSAT | Telesat Corp | Satellite/Telecom |
| BBAI | BigBear.ai | AI/Defense |
| NBIS | Nebius Group | AI/Cloud |
| OKLO | Oklo Inc | Nuclear Energy |
| NVTS | Navitas Semi | Semiconductors |

### Step 2: Research the Market

Use web search to find TODAY's data for:
- **S&P 500, NASDAQ, DOW** — closing price + daily % change
- **Bitcoin (BTC)** — current price + 24h % change
- **VIX** — current level + daily % change
- **Oil (WTI)** — current price + daily % change
- **Overall market sentiment** — bullish, bearish, or neutral based on the day's action
- **Key market drivers** — summarize in 1-2 sentences why the market moved

### Step 3: Research Each Holding

For EACH ticker in the portfolio, use web search to find:
- Latest news (earnings, analyst upgrades/downgrades, contracts, SEC filings, sector moves)
- Why the price changed today
- Key risks and catalysts coming up
- Your assessment: **bullish**, **bearish**, or **neutral**
- A signal tag: `BULLISH`, `BEARISH`, `HOLD`, `CAUTION`, `HIGH RISK`, `SPECULATIVE`, `PIVOT`, `FEAR MODE`, or a custom one-word tag

### Step 4: Write the ai-data.json File

Write the file to `/STOCK and Finances/ai-data.json` with this **exact** JSON structure:

```json
{
    "generated_at": "2026-03-07T21:00:00+07:00",
    "market_overview": {
        "sp500": { "value": "5,738", "change": "-1.0%", "direction": "down" },
        "nasdaq": { "value": "18,069", "change": "-1.3%", "direction": "down" },
        "dow": { "value": "42,579", "change": "-1.5%", "direction": "down" },
        "btc": { "value": "$70,658", "change": "-2.8%", "direction": "down" },
        "vix": { "value": "24.8", "change": "+8.2%", "direction": "up" },
        "oil": { "value": "$82.40", "change": "+3.1%", "direction": "up" }
    },
    "sentiment": {
        "mood": "bearish",
        "icon": "🔴",
        "summary": "One sentence explaining why the market is bullish/bearish/neutral today."
    },
    "insights": [
        {
            "ticker": "MARKET",
            "type": "bearish",
            "signal": "BEARISH",
            "text": "<strong>Bold headline.</strong> 2-4 sentences explaining the market today. Be direct, conversational, and specific."
        },
        {
            "ticker": "RKLB",
            "type": "bullish",
            "signal": "BULLISH",
            "text": "<strong>Bold headline.</strong> 2-4 sentences with specific numbers, news, and your take. Reference the user's cost basis when relevant (e.g., 'down 55% from your cost')."
        }
    ]
}
```

---

## CRITICAL RULES for the JSON

1. **`generated_at`** — Use the current date/time in ISO 8601 format with `+07:00` timezone
2. **`market_overview`** — Values are strings. `direction` must be `"up"` or `"down"`
3. **`sentiment.mood`** — Must be exactly `"bullish"`, `"bearish"`, or `"neutral"` (lowercase)
4. **`sentiment.icon`** — Use `"🟢"` for bullish, `"🔴"` for bearish, `"🟡"` for neutral
5. **`insights`** array must contain:
   - First entry must be `"ticker": "MARKET"` (overall market analysis)
   - Then one entry per portfolio holding (check portfolio.md for the latest list)
6. **`type`** field — Must be exactly `"bullish"`, `"bearish"`, or `"neutral"` (lowercase)
7. **`text`** field — Start with `<strong>Bold hook headline.</strong>` then 2-4 sentences. Use `<strong>` tags for emphasis (NOT markdown bold). Keep it under 300 characters.
8. **Escape quotes properly** — This is JSON, so double quotes inside strings must be escaped as `\"`
9. **Be direct and opinionated** — The user has aggressive risk tolerance and prefers blunt analysis over hedging
10. **Reference the user's cost basis** — When a stock is significantly up or down from their average cost, mention it

---

## Sentiment Icons Quick Ref

| Mood | Icon | Sentiment Banner Color |
|------|------|----------------------|
| bullish | 🟢 | Green |
| bearish | 🔴 | Red |
| neutral | 🟡 | Orange/Yellow |

## Signal Tags Quick Ref

| Tag | When to Use |
|-----|-------------|
| BULLISH | Strong positive momentum, good fundamentals |
| BEARISH | Declining, bad news, deteriorating fundamentals |
| HOLD | Okay position, no action needed |
| CAUTION | Watch closely, mixed signals |
| HIGH RISK | Significant downside risk, volatility |
| SPECULATIVE | Thesis-driven, high uncertainty |
| PIVOT | Company undergoing major strategic change |
| FEAR MODE | Extreme fear/selling pressure |

---

## Example Trigger

When the user says: **"run the daily"**, **"update dashboard"**, or **"generate ai-data"**, execute this full routine.

When done, confirm: *"✅ ai-data.json updated. Refresh your dashboard to see the latest analysis."*
