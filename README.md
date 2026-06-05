# Sentiment vs. Stock Market Performance
### Does Consumer Confidence Actually Drive Equity Returns?

> *At a time of geopolitical chaos and historically low consumer sentiment, the stock market has been surging. This project investigates whether that disconnect is a new phenomenon — or whether sentiment and returns were never meaningfully correlated to begin with.*

---

## The Question

Popular financial wisdom holds that when consumers feel good about the economy, markets go up — and when they feel bad, markets fall. This project tests that assumption rigorously using 45 years of data (1979–present), spanning the Volcker era, dot-com boom and bust, 2008 financial crisis, COVID crash, and the current tariff-driven sentiment collapse.

---

## Key Findings

1. **Sentiment and returns are not significantly correlated** (r = 0.073, p > 0.05) across the full 1979–present window. The popular assumption is not supported by the data.

2. **Era-by-era analysis confirms the pattern** — across 9 distinct historical periods, only 1 showed a statistically significant correlation (COVID crash, r = -0.59, p = 0.04), and even that was *inverse* — sentiment fell while the market recovered.

3. **Every sector posted strong returns during the current low-sentiment period (2022–present)** — Technology led at 2.0x cumulative return, but Industrials (1.68x), Energy (1.60x), and Financials (1.46x) all performed strongly. Market strength is broad-based, not explained by a single sector.

4. **The market reflects corporate earnings and institutional capital — not consumer feelings.** The S&P 500 is market-cap weighted, meaning a handful of AI-driven mega-cap companies (Magnificent 7 = ~34% of the index by 2025) can drive index gains regardless of how average Americans feel about the economy.

---

## Methodology

### Hypothesis Test
- **H₀:** No significant correlation between consumer sentiment and S&P 500 monthly returns
- **H₁:** Significant correlation exists
- **Test:** Pearson correlation (`scipy.stats.pearsonr`)
- **Result:** Fail to reject H₀ — r = 0.073, p > 0.05

### Era Breakdown
Correlation was computed separately for 9 historical periods to test whether the relationship differs across economic regimes. Lagged sentiment (t-1) was used to test whether prior month sentiment predicts current month returns.

### Sector Analysis
Cumulative returns calculated for 7 S&P 500 sector ETFs (XLK, XLF, XLE, XLY, XLP, XLV, XLI) from 2022–present to assess whether market strength during low sentiment is concentrated in tech/AI or broad-based.

---

## Data Sources

| Dataset | Source | Series/Ticker |
|---|---|---|
| Consumer Sentiment Index | FRED | `UMCSENT` |
| S&P 500 Price History | Yahoo Finance (yfinance) | `^GSPC` |
| Historical P/E Ratio | Macrotrends | Manual CSV download |
| Sector ETFs | Yahoo Finance (yfinance) | XLK, XLF, XLE, XLY, XLP, XLV, XLI |

---

## Tools & Libraries

- **Python** — Pandas, NumPy, SciPy, Matplotlib
- **yfinance** — S&P 500 and sector ETF data
- **fredapi** — FRED economic data API
- **Jupyter Notebook** — analysis and visualization

---

## How to Run

```bash
# Install dependencies
pip install pandas numpy scipy matplotlib yfinance fredapi

# Launch notebook
jupyter notebook sentvsval.ipynb
```

**Note:** FRED data (`UMCSENT.csv`) and Macrotrends P/E data (`pe-ratio.csv`) are included in the `/data` folder. No API key required for the CSV-based workflow.

---

## Visualizations

**S&P 500 Annual Returns vs Consumer Sentiment (1979–Present)**
- Dual-axis line chart showing both variables over time with key events annotated

**Sector Cumulative Returns (2022–Present)**
- Horizontal bar chart showing all 7 sectors ranked by total return during the current low-sentiment period

---

## Limitations

- Monthly data may be too coarse to capture short-term sentiment-return dynamics
- P/E ratio is backward-looking and can be distorted by earnings collapses
- Small sample sizes in short eras (COVID, Post-COVID) reduce statistical power
- Analysis does not control for confounding variables (interest rates, inflation, earnings growth)

---

## What I'd Investigate Next

- Compare equal-weighted vs market-cap weighted S&P 500 returns to quantify the Magnificent 7 concentration effect
- Add Federal Funds Rate as a control variable to separate monetary policy effects from sentiment effects
- Segment sentiment by income bracket to test the wealth concentration hypothesis — top 10% own 87% of equities
