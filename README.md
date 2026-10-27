# IPO Analyzer — a Claude skill

A Claude skill that analyzes Indian IPOs (mainboard and SME) on 10 factors and tells you
**what is happening / what happened** and **what the signals suggest** — using web search
and Claude in Chrome to collect live data.

## Factors
1. Company financials
2. IPO valuation (vs peers)
3. Subscription demand (QIB / NII / retail)
4. Overall market sentiment
5. Grey Market Premium (unofficial)
6. Promoters, OFS and use of funds
7. Listing-day supply and demand
8. Sector trend
9. Anchor investors and lock-ins
10. Issue size

Each factor is scored −2 to +2 and grouped into two ratings: **Listing gains** and **Long-term**.

## Repo layout
```
ipo-analyzer/
├── SKILL.md              # instructions Claude follows
├── references/
│   ├── factors.md        # scoring rubric + red flags
│   └── sources.md        # where to find each data point
└── templates/
    └── report.md         # output format
```

## Install
**Claude app (claude.ai / desktop):** zip the `ipo-analyzer` folder and upload it under
Settings → Capabilities → Skills.

**Claude Code:** copy the folder to `~/.claude/skills/ipo-analyzer/`.

For live data from JavaScript-heavy pages (NSE, subscription tables), install the
**Claude in Chrome** extension and keep Chrome open.

## Use
> Analyze the <Company> IPO
> What happened on <Company>'s listing day?
> Compare <IPO A> and <IPO B>

## Disclaimer
For information and education only — not investment advice. GMP is unofficial.
