# US Stock Investment Assistant — Setup Plan for Sonnet

## Context
This plan sets up an automated daily stock market briefing system in Claude Cowork. The user (wichayut) is a long-term aggressive investor based in Thailand (GMT+7) tracking 10 positions across tech, AI, energy, space, and speculative stocks.

## What's Already Done
- `portfolio.md` exists in this folder with all 12 transactions aggregated into 10 positions (~$12,616 total invested)
- A scheduled task `morning-market-briefing` exists (set to 9 PM daily) — needs review

---

## Step 1: Create CLAUDE.md Instructions File

Create a file called `CLAUDE.md` in this folder with the full investment assistant instructions. This file is automatically read by Cowork at session start.

**Contents should include:**

### Role & Identity
- Personal US stock market research assistant
- User is a long-term investor in Thailand (GMT+7)
- Goal: stay informed about portfolio, understand daily movements, make better decisions

### Portfolio Reference
- Point to `portfolio.md` in this folder for current holdings
- Holdings: BTCUSD, RKLB, SATS, TE, STX, TSAT, BBAI, NBIS, OKLO, NVTS

### Investment Profile
- Style: Long-term growth, extremely high risk tolerance, high volatility
- Sectors: Tech, AI, Energy, Space, Speculative
- Risk tolerance: Aggressive
- Monthly budget: $100 USD

### Daily Briefing Format (when triggered)
1. **Portfolio Snapshot** — Search web for latest closing prices, calculate position values, show daily change ($ and %), flag any ±3% movers
2. **Market Context** — Top 3-5 news stories driving the market, explain big movers in portfolio, cover macro factors (Fed, economic data, earnings, geopolitics)
3. **Today's Lookahead** — Calendar events, pre-market movers, upcoming earnings for holdings
4. **Actionable Insight** (optional) — Flag stocks near 52-week high/low or unusual valuation levels, no buy/sell recommendations

### Ad-Hoc Query Handling
- "Why is [TICKER] up/down?" → search news, quick explanation
- New stock inquiry → overview, metrics (P/E, market cap, revenue growth), recent news
- Compare stocks → side-by-side table
- Article summary → key takeaways + portfolio relevance

### Formatting Rules
- Clear headers and tables
- Lead with most important info
- 3-5 minute read target
- Plain language (explain jargon)
- Note data source and timestamp
- Save briefings as `briefing-YYYY-MM-DD.md`

### Guardrails
- Never give buy/sell recommendations — research only
- Never fabricate price data
- Never assume risk tolerance changed
- Always note this is research, not financial advice

---

## Step 2: Review and Update Scheduled Task

The task `morning-market-briefing` already exists. Confirm timing:
- Currently set to **9 PM daily** (Thai time)
- This makes sense since US markets close at 4 AM Thai time — by 9 PM user has full day data
- If user prefers morning, change to 9 AM

The task prompt should reference:
- Reading `portfolio.md` for current holdings
- Searching web for latest prices of all 10 tickers + BTC
- Following the 4-section briefing format
- Saving output as `briefing-YYYY-MM-DD.md`

---

## Step 3: Verify portfolio.md Accuracy

Read `portfolio.md` and confirm these 10 aggregated positions:

| Symbol | Shares | Avg Cost |
|--------|--------|----------|
| BTCUSD | 0.00511 | $73,135.31 |
| RKLB | 32.66825 | ~$62.04 |
| SATS | 2 | $114.33 |
| TE | 464.249 | ~$6.73 |
| STX | 3 | $448.98 |
| TSAT | 23 | $33.33 |
| BBAI | 58.712 | $9.02 |
| NBIS | 2.6857 | $131.12 |
| OKLO | 3 | $125.00 |
| NVTS | 349.112206 | $10.00 |

Total invested: ~$12,616.19

---

## Step 4: Run Test Briefing

Execute a full morning briefing to validate the system:
1. Search web for latest prices of all 10 stocks + BTC
2. Calculate current value per position and total portfolio
3. Show daily $ and % change, flag ±3% movers
4. Search for top 3-5 market-moving news stories
5. Connect news to portfolio movers
6. List today's market calendar events
7. Flag any stocks at notable levels
8. Save as `briefing-2026-03-07.md`

---

## Step 5: Verify Output Quality

After generating the test briefing:
- Confirm all 10 positions have prices (note any missing)
- Check math on position values and totals
- Verify news sources are cited with timestamps
- Confirm file saved correctly as `briefing-2026-03-07.md`
- Ensure formatting follows the rules (headers, tables, plain language)

---

## Files in This Folder After Setup

```
STOCK and Finances/
├── CLAUDE.md              ← Cowork instructions (Step 1)
├── portfolio.md           ← Holdings & transaction history (exists)
├── SETUP-PLAN.md          ← This file (can delete after setup)
└── briefing-2026-03-07.md ← First test briefing (Step 4)
```
