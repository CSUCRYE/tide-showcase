<div align="center">

<img src="assets/tide_demo.gif" alt="潮汐 Tide demo" width="100%">

# 潮汐 Tide

**An A-share-focused, chat-driven stock research assistant, with a bridge to overseas markets**

English · [中文](README_ZH.md)

*This is a showcase repository — the source code is private, this page describes the project and how to request a demo invite.*

</div>

---

## Why I built this

I got into stock trading four years ago. Since then I've made money and lost money, and
paid plenty of tuition along the way. This March, it occurred to me: instead of squinting
at charts and news feeds alone, why not let an LLM handle the repetitive parts — pulling
data, walking through technicals — and keep the actual judgment calls for myself.

That idea turned into months of nights-and-weekends work, going from a script that barely
ran to a full multi-page app with its own factor-scoring engine, backtesting lab, and
machine-learning comparison tools. Along the way I discovered that the scoring weights I'd
carefully hand-tuned turned out to have very weak predictive power once I actually
backtested them properly — instead of hiding that finding, I built it into the project's
guiding principle (see "Honesty" below).

**This is not a financial product and not a stock-tipping service — it's a personal tool I
use and keep improving myself.**

## Want to try it?

The app is live and running, gated behind an invite code (a handful of people are already
using it). It's not open to the public, and this repository intentionally doesn't include
the source code.

**Open a new Issue in this repository (the "Issues" tab above) and let me know you'd
like to try it, along with a way
to privately reach you (email works well).** I'll reply with the demo link and an invite
code through that private channel — not as a public comment on the issue, since anyone
could read that.

## What it is

A Streamlit app with four entry points — four different ways of looking at the market:

| Entry | Angle | What it does |
|---|---|---|
| **潮汐表 (Screen)** | Discover | Multi-factor ranking across all A-shares, by momentum and valuation percentile, with a reason for each pick |
| **验潮 (Diagnose)** | Deep dive | Deep technical diagnosis of a single stock — K-line chart plus historical signal backtest stats |
| **问潮 (Ask)** | Follow up | Multi-turn natural-language Q&A about a stock's quotes, indicators, and historical signals |
| **潮讯 (Signals)** | Event-driven | Today's newly triggered, historically high-confidence signal combos across the CSI 300 (experimental) |

## Highlights

### Screen · Strategy Lab

Ranks all A-shares by a momentum + valuation composite score. The **Strategy Lab** lets
you drag a slider and watch the historical IC and backtest curve recompute live for any
weight combination — including training an actual machine learning model (logistic
regression / gradient boosting) on the same historical panel and comparing it, honestly,
against a naive baseline.

<img src="assets/screenshots/strategy_lab.png" alt="Strategy Lab" width="100%">
<img src="assets/screenshots/ml_model.png" alt="Machine learning model comparison" width="100%">

### Diagnose · Deep single-stock analysis

K-line chart with moving averages, MACD/RSI/KDJ, historical signal win rates reported with
a Wilson lower confidence bound (not a raw win rate), an LLM-generated report with an
optional fact-check pass, a KNN-based "similar stocks" panel, and an LLM-summarized digest
of recent public disclosures.

<img src="assets/screenshots/diagnose.png" alt="Diagnose page" width="100%">

### Signals · Event-driven scanning

Scans the CSI 300 constituents for stocks that just triggered a two-signal combination with
a historically strong, pooled-and-confidence-adjusted track record. If nothing qualifies
today, the page says so honestly instead of manufacturing a signal just to have something
to show.

<img src="assets/screenshots/signals.png" alt="Signals page" width="100%">

### Ask · Multi-turn follow-up + tool calling

Natural-language, multi-turn questions about a stock's quotes, indicators, and historical
signals. On Claude specifically, it can decide mid-conversation to pull in the stock's
recent disclosures or its similar-stocks panel via tool calls, instead of being limited to
whatever was pre-computed.

## Honesty is the project's operating principle

Most "AI stock picking" tools market themselves on "look how accurate we are." My own
years of trading taught me that any simple factor model is unlikely to show meaningful
predictive power over a short window — that's common knowledge in quant circles, not a
secret.

So Tide does the opposite: factor effectiveness is shown plainly, including unflattering
conclusions like "this period's momentum factor IC is near zero, sometimes even negative."
That extends to the machine learning models too — I trained real ones on the same
historical data and reported their real out-of-sample accuracy next to a naive baseline.
The honest result: gradient boosting edges past that baseline by a hair, logistic
regression mostly doesn't, and neither reliably beats the plain fixed-weight score they
were supposed to improve on. That's shown in the app, not buried.

## Tech stack

- **UI**: Python + [Streamlit](https://streamlit.io/)
- **Market data**: [AkShare](https://akshare.akfamily.xyz/) (public sources like Eastmoney/Tencent Finance, with automatic multi-source fallback)
- **Charts**: Plotly
- **ML**: scikit-learn (logistic regression, gradient boosting), walk-forward backtesting
- **LLM**: Claude / Gemini / GLM — pluggable, BYOK
- **Deployment**: Docker + Caddy on a small VPS

## Disclaimer

Everything this tool generates — rankings, reports, answers, signal statistics — is
aggregated data and historical-statistics assistance, not investment advice of any kind.
Accuracy, completeness, and timeliness of the data are not guaranteed. All backtest
statistics (win rates, returns, holding periods, etc.) reflect historical data and do not
represent future returns. The stock market carries risk; make your own judgment and bear
the consequences of your own decisions.

---

<div align="center">

by CSUCRYE

</div>
