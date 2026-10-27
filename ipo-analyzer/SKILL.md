---
name: ipo-analyzer
description: Analyze an Indian IPO (mainboard or SME) on 10 factors — financials, valuation, subscription, market sentiment, GMP, promoters/OFS/use of funds, listing-day supply-demand, sector trend, anchor investors, issue size and lock-ins — using web search and Claude in Chrome, then explain what happened and what the signals suggest. Use when the user names an IPO and asks to analyze it, check it, compare it, or explain its listing.
---

# IPO Analyzer

Analyze one IPO (or compare a few) and give the user a clear, evidence-backed picture:
**what is happening / what happened**, and **what the signals suggest** for listing gains
and for long-term holding. The user makes the final decision.

## Ground rules

- Never invent numbers. Every figure in the report must come from a page you actually read.
  If a number can't be found, write "Not found" and lower your confidence.
- Prefer official sources (RHP/DRHP on SEBI, NSE/BSE pages) over aggregators. Use
  aggregators (Chittorgarh, Investorgain, Moneycontrol) for subscription and GMP.
- Don't log in to any site, don't fill forms, don't solve CAPTCHAs. If a page is blocked,
  try another source from `references/sources.md`.
- This is information, not investment advice. Present signals and scenarios; never say
  "you must buy/sell". End every report with the disclaimer in the template.
- Always state the date/time the data was collected — GMP and subscription change hourly.

## Step 1 — Identify the IPO and its stage

Ask (or infer) the IPO name. Then find:
- Mainboard or SME (exchange: NSE / BSE / NSE Emerge / BSE SME)
- Price band, lot size, issue size, open/close/allotment/listing dates
- **Stage** — this decides what the report focuses on:

| Stage | Focus |
|---|---|
| Upcoming (not open) | Financials, valuation, promoters, sector, early GMP |
| Open (subscribing) | Above + live subscription by category, anchors |
| Closed, not listed | Final subscription, GMP trend, market mood → listing outlook |
| Listed | **What happened**: listing price vs issue price, and which factors explain it; what to do next as a holder (signals only) |

## Step 2 — Collect data

Use WebSearch / WebFetch first (faster). Switch to Claude in Chrome when a page needs
JavaScript (live subscription tables, NSE pages, GMP tables). With Chrome, load tools in
one ToolSearch call, open a new tab, and read pages with get_page_text / read_page.

Collect everything listed in `references/sources.md` → "Data checklist".
Save raw findings to `data/<ipo-name>.md` with the source URL next to each number.

## Step 3 — Score every factor

Score each factor using the rubric in `references/factors.md`:
**+2 strong positive, +1 positive, 0 neutral/unknown, −1 negative, −2 strong negative.**
Write one line of evidence for each score.

Factors are grouped into two lenses:
- **Listing-gain lens:** Subscription demand, Market sentiment, GMP, Listing-day supply/demand, Issue size
- **Long-term lens:** Financials, Valuation, Promoters/OFS/use of funds, Sector trend, Anchors & lock-ins

Total each lens separately (range −10 to +10) and map it:
- +6 to +10 → Strong
- +2 to +5 → Moderate
- −1 to +1 → Mixed
- −2 to −10 → Weak

Apply the red-flag overrides in `references/factors.md` — any hard red flag caps that lens
at "Mixed" no matter the score.

## Step 4 — Explain (for listed IPOs: what happened)

If the IPO has listed, compare listing open/close to issue price and to the last GMP.
Explain the gap using the factors: e.g. "QIB 120x + strong market → listed 45% up, above
GMP" or "Mostly OFS + Nifty fell 2% that day → listed 8% below GMP".

## Step 5 — Write the report

Use `templates/report.md` exactly. Keep it short and plain — the user may not be a finance
expert. Explain any jargon in a few words the first time it appears.

The "What the signals suggest" section gives scenarios, not orders, for example:
- For listing gains: "Signals are Strong — historically IPOs with this profile tend to list at a premium, but a market fall could change that."
- For long-term: "Valuation is stretched vs peers; a long-term holder would want to see X."
- For someone already holding after listing: what to watch (lock-in dates, results, peer moves).

If the user asks to compare several IPOs, produce one scorecard per IPO and then a
side-by-side table of the two lens ratings.
