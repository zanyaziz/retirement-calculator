# Net Worth Percentile Calculator

A single-page web calculator that estimates where your household net worth sits in the
US distribution — and how long it would take to climb to the next rung if the rungs
themselves keep rising.

**Live:** https://zanyaziz.github.io/retirement-calculator/

Everything runs in your browser. Nothing is stored, sent, or tracked — refresh the
page and your numbers are gone.

## What you enter

- **Income** — base salary, annual bonus, and stock compensation (with an optional
  company/ticker label), plus any other income rows you add.
- **Tax rate and annual expenses** — savings = income × (1 − tax rate) − expenses.
  A waterfall shows the flow: Income → −Taxes → −Expenses → = Annual Savings. You can
  also override the savings figure directly.
- **Properties** — each with a current value and the liability (mortgage) against it;
  equity is the difference. One property can be marked as your **primary home**,
  which Tab 3 treats specially (below).
- **Cash and other assets.**
- **Brokerage / retirement accounts** — each account is either a single total or a
  detailed list of holdings (symbol + value) that sums automatically.
- **Other liabilities.**
- **Assumptions** — expected return on invested assets (default 6%), property
  appreciation (default 0%, conservative), and a bar-growth adjustment (default 0).

## How the percentile is estimated

Net worth thresholds come from the **Federal Reserve's 2025 Survey of Consumer
Finances (SCF)**, as tabulated by DQYDJ — e.g. the 90th percentile rung is
$2,550,306, the 95th is $4,907,372, the 98th is $10,034,008, and the 99th is
$16,463,320. The full rung table (1st–99.9th percentile) is hardcoded in the page.

Your percentile is estimated by **log-linear interpolation** between the two rungs
that bracket your net worth. That makes it an estimate, not an exact rank — the SCF
publishes thresholds, not a continuous curve.

## How the projection works

The percentile bars are moving targets. Historically, each rung of the SCF ladder has
risen at roughly the same nominal pace — about **5.5%/yr from 1989 to 2025** (the
90th-percentile bar compounded at 5.52%/yr; the 95th and 99th at 5.59%/yr). The
calculator grows each future bar at its rung's documented long-run rate (plus your
adjustment), while your net worth grows bucket by bucket:

- invested assets compound at your return assumption, with your annual savings added
  each year;
- property equity grows at your appreciation assumption;
- liabilities stay flat.

A year-by-year simulation (up to 80 years) finds when — if ever — your projected net
worth crosses the rising next bar, and the chart plots both lines so you can see the
crossing (or see the bar pull away, in which case the page says plainly: *not on the
current path*). It also solves for the extra annual savings that would reach the next
rung in exactly 10 years.

## Tab 3 — Retirement: how long will it last?

Pick how many years from now you'd like to retire. Tab 3 grows the same Tab 1
balance sheet to that day (same savings, same return), then draws it down against
your spending — inflated every year — less Social Security and any other income,
until the money runs out, and reports the age and year that happens.

The balance sheet is split into three buckets: **liquid money** (invested + cash −
other debts, always counted), **other property equity** (counted by default —
assumed sold at retirement), and **primary home equity** (excluded by default, so
the headline answer is how long your money lasts *while you keep your home*). In
Tab 3 you can switch the home on, either as a last resort (tapped only after the
other money runs out) or as a sale at retirement.

Social Security can be estimated in the page using the real SSA formula — 2026
bend points ($1,286 / $7,749), the $184,500 wage base, full retirement age 67,
and the standard early/delayed claiming factors — applied to your Tab 1 income,
or entered directly from your SSA statement, or left out entirely. The estimate
is a ballpark, labelled as one.

These projections are scenarios, not forecasts, and this is not financial advice.

## Tech

One self-contained HTML file — no build step, no dependencies, no backend. Open
`index.html` in any browser, or fork this repo and enable GitHub Pages.

## License

MIT — see [LICENSE](LICENSE). Copyright (c) 2026 Zain Aziz.

The SCF threshold data is from the US Federal Reserve's Survey of Consumer Finances.
