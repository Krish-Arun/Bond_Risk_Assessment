______________________________________________________________________

# 1. Data for G-Sec prediction

## A. Core target data

| Data | Fields needed | Frequency | Why you need it |
| :-- | :-- | --: | :-- |
| Indian G-Sec yields | Date, ISIN, security name, coupon, maturity date, yield to maturity, clean price, dirty price | Daily | This is the primary target for yield prediction |
| Benchmark yields | 2-year, 5-year, 10-year, 15-year, 20-year, 30-year yields | Daily | Needed to model the yield curve and predict different maturities |
| 10-year G-Sec yield | Date, yield, clean price, volume | Daily | Best starting target: high liquidity and clear market benchmark |
| Treasury Bill yields | 91-day, 182-day, 364-day yields | Daily/weekly | Captures short-term rate expectations and monetary-policy transmission |
| G-Sec trading data | Trade date, ISIN, price, yield, volume, number of trades, bid yield, ask yield | Daily | Measures liquidity, market activity, and price discovery |
| G-Sec auction data | Auction date, security, notified amount, accepted amount, cut-off yield, bid-to-cover ratio | Auction date | Captures bond supply and investor demand |
| Yield-curve data | Date, tenor, zero-coupon yield, par yield, forward rate | Daily | Needed for curve slope, curvature, and multi-maturity prediction |

For training, collect at least **5–10 years of daily data**. For a weekly model, 10–15 years is better because it covers different interest-rate cycles.

## B. RBI and policy data

| Data | Fields needed | Frequency | Why you need it |
| :-- | :-- | --: | :-- |
| Repo rate | Effective date, rate, change in bps | Event-based | Major driver of Indian interest-rate expectations |
| Reverse repo, SDF, MSF | Effective date, rate | Event-based | Defines RBI’s policy-rate corridor |
| CRR and SLR | Effective date, percentage | Event-based | Affects banking liquidity and bond demand |
| MPC meeting calendar | Meeting date, decision, policy stance, release date | Event-based | Helps create policy-event features |
| RBI liquidity operations | OMO purchase/sale, VRR/VRRR, amount, maturity, rate | Event-based/daily | Captures liquidity injections and absorptions |
| Government borrowing | Auction calendar, notified amount, issued amount, maturity | Weekly/event-based | More bond supply can pressure yields upward |
| Fiscal deficit | Month/quarter, deficit, borrowing requirement | Monthly/quarterly | Indicates future government financing needs |
| Liquidity indicator | Banking-system surplus/deficit, net liquidity injection | Daily/weekly | Affects short-term rates and bond demand |

## C. Indian macroeconomic data

| Data | Fields needed | Frequency | Why you need it |
| :-- | :-- | --: | :-- |
| CPI inflation | Date, headline CPI, food CPI, core CPI, YoY change | Monthly | Higher inflation usually raises yield expectations |
| WPI inflation | Date, index, YoY change | Monthly | Captures producer-price and input-cost pressure |
| GDP growth | Quarter, real GDP growth, nominal GDP growth | Quarterly | Strong growth can increase inflation and rate expectations |
| IIP growth | Month, index, YoY growth, sectoral growth | Monthly | High-frequency proxy for industrial activity |
| PMI | Month, manufacturing PMI, services PMI | Monthly | Measures business activity and sentiment |
| Bank credit growth | Month, credit growth, sectoral credit | Monthly | Indicates credit demand and economic momentum |
| Foreign trade | Exports, imports, trade deficit, current-account balance | Monthly/quarterly | Affects currency, inflation, and external financing |

## D. Global and currency data

| Data | Fields needed | Frequency | Why you need it |
| :-- | :-- | --: | :-- |
| USD/INR | Date, open, high, low, close, percentage change | Daily | Rupee depreciation can raise imported inflation and affect foreign flows |
| Brent crude | Date, price, daily change | Daily | Oil affects India’s inflation and current account |
| US 10-year Treasury yield | Date, yield, daily change | Daily | Global benchmark that influences Indian bond yields |
| US 2-year Treasury yield | Date, yield | Daily | Useful for global rate expectations and curve analysis |
| US Federal Funds rate | Effective date, rate, FOMC decision | Event-based | Captures global monetary-policy direction |
| VIX | Date, close, daily change | Daily | Measures global risk appetite |
| Dollar Index | Date, close, daily change | Daily | Captures dollar strength and emerging-market flows |
| Gold price | Date, price, daily change | Daily | Optional safe-haven and inflation-hedge indicator |

## E. Indian market-sentiment data

| Data | Fields needed | Frequency | Why you need it |
| :-- | :-- | --: | :-- |
| Nifty 50 or Sensex | Date, open, high, low, close, volume, return | Daily | Broad risk-on/risk-off indicator |
| India VIX | Date, close, daily change | Daily | Measures Indian-market volatility |
| FPI debt flows | Date, net inflow/outflow, amount invested | Daily/weekly/monthly | Foreign demand can affect G-Sec yields |
| Mutual-fund debt flows | Date, category, inflow/outflow | Monthly | Indicates domestic institutional demand |
| Money-market rates | Call-money rate, overnight rate, weighted average call rate | Daily | Captures short-term liquidity conditions |


______________________________________________________________________

# 2. Data for corporate-bond prediction

For corporate bonds, you need **two prediction components**:

$$
\widehat{Y}_{\text{corporate},t+1}
=
\widehat{Y}_{\text{G-Sec},t+1}
+
\widehat{\text{Credit Spread}}_{t+1}
$$

The G-Sec model predicts the broad Indian interest-rate environment. The credit-spread model predicts the extra yield investors demand for that issuer, sector, rating, maturity, and liquidity profile.

## A. Corporate-bond market data

| Data | Fields needed | Frequency | Why you need it |
| :-- | :-- | --: | :-- |
| Corporate bond prices | Date, ISIN, clean price, dirty price, accrued interest | Daily | Needed to calculate yield and price changes |
| Corporate bond yields | Date, ISIN, yield to maturity, yield change | Daily | Primary target for corporate-bond prediction |
| Trading data | Trade date, ISIN, trade price, yield, volume, number of trades | Daily | Measures liquidity and market interest |
| Bid/ask data | Bid price, ask price, bid yield, ask yield, spread | Daily | Measures liquidity and transaction cost |
| Bond issue details | ISIN, issuer, issue date, maturity date, coupon, face value, coupon frequency | Static | Needed to calculate yield, duration, and maturity effects |
| Bond structure | Secured/unsecured, senior/subordinated, callable, puttable, convertible, collateral | Static | Affects credit risk and valuation |
| Credit spreads | Corporate yield minus comparable G-Sec yield | Daily | Main target for issuer-risk prediction |
| Sector spreads | Sector average yield, sector average spread | Daily/weekly | Captures industry-wide risk |

SEBI publishes daily corporate-bond trading data by exchange and reporting platform, including trade counts and traded amounts. cite cite[^15_2][^15_3]

## B. Issuer financial data

| Data | Fields needed | Frequency | Why you need it |
| :-- | :-- | --: | :-- |
| Income statement | Revenue, operating profit, EBITDA, interest expense, net profit | Quarterly/annual | Measures profitability and ability to service debt |
| Balance sheet | Total debt, short-term debt, long-term debt, cash, equity, assets | Quarterly/annual | Measures leverage and liquidity |
| Cash-flow statement | Operating cash flow, investing cash flow, financing cash flow, free cash flow | Quarterly/annual | Measures cash generation and repayment capacity |
| Financial ratios | Debt-to-equity, interest coverage, current ratio, quick ratio, ROE, ROA | Quarterly/annual | Standard credit-risk indicators |
| Debt profile | Total debt, maturity schedule, refinancing needs, covenant details | Quarterly/annual | Important for default and refinancing risk |
| Credit rating | Issuer, agency, rating, outlook, rating date, rating change | Event-based | Directly reflects credit risk |
| Rating history | Past upgrades, downgrades, outlook changes | Event-based | Helps model rating migration and spread changes |

## C. Issuer and sector data

| Data | Fields needed | Frequency | Why you need it |
| :-- | :-- | --: | :-- |
| Issuer profile | Company name, sector, industry, ownership type, listing status | Static | Needed for grouping and sector features |
| Sector performance | Sector index return, sector volatility, sector credit spread | Daily/weekly | Captures industry-wide conditions |
| Commodity exposure | Input commodity prices relevant to issuer | Daily | Important for manufacturing, power, metals, and oil-related issuers |
| Regulatory events | Policy changes, tariffs, sector regulations, approvals | Event-based | Can affect issuer cash flows and credit risk |
| Corporate events | Earnings release, debt issuance, refinancing, default, restructuring, merger | Event-based | Can cause sudden yield and spread changes |
| News sentiment | Headline, publication date, sentiment score, source | Event-based | Optional but useful for event-driven risk signals |

## D. Corporate-bond liquidity data

This is especially important because many Indian corporate bonds trade infrequently.


| Data | Fields needed | Frequency | Why you need it |
| :-- | :-- | --: | :-- |
| Trading frequency | Number of trades per day/week/month | Daily/weekly | Low liquidity makes price data stale |
| Trading volume | Traded value, traded quantity | Daily | Measures market interest |
| Bid-ask spread | Bid price, ask price, spread in bps | Daily | Measures transaction cost |
| Days since last trade | Date of last trade, days elapsed | Daily | Identifies stale prices |
| Dealer quotes | Indicative bid/ask yield, quote timestamp | Intraday/daily | Useful when actual trades are absent |
| Outstanding amount | Amount issued, amount outstanding, free float | Static/monthly | Larger issues are often more liquid |


______________________________________________________________________

# 3. Features you derive from collected data

You do not need to collect all derived features separately. Calculate them from the raw data.

## G-Sec features

| Feature group | Examples |
| :-- | :-- |
| Lagged yields | $Y_{t-1}$, $Y_{t-5}$, $Y_{t-10}$, $Y_{t-20}$ |
| Yield changes | 1-day, 5-day, 10-day, 20-day change |
| Returns | Daily log return or percentage change |
| Moving averages | 5-day, 10-day, 20-day, 50-day average yield |
| Momentum | Current yield minus moving average |
| Volatility | 5-day, 20-day, 60-day rolling standard deviation |
| Range | Rolling maximum, minimum, high-low range |
| Volume features | Volume change, relative volume, rolling average volume |
| Yield-curve slope | $10Y - 2Y$, $10Y - 5Y$, $10Y - 91D$ |
| Curve curvature | $2Y_{5Y} - Y_{2Y} - Y_{10Y}$ |
| Curve regime | Steepening, flattening, inversion indicator |
| Policy events | MPC-week dummy, repo-rate-change dummy, auction-day dummy |

## Corporate-bond features

| Feature group | Examples |
| :-- | :-- |
| Lagged yield | Bond yield at $t-1$, $t-5$, $t-20$ |
| Yield change | 1-day, 5-day, 20-day yield change |
| Credit spread | Corporate yield minus comparable G-Sec yield |
| Spread change | 1-day, 5-day, 20-day spread change |
| Rating features | Current rating, rating score, rating outlook, days since rating change |
| Financial features | Debt-to-equity, interest coverage, EBITDA margin, cash flow |
| Liquidity features | Volume, number of trades, bid-ask spread, days since last trade |
| Maturity features | Time to maturity, duration, modified duration |
| Sector features | Sector spread, sector index return, sector volatility |
| Event features | Earnings-release dummy, rating-change dummy, refinancing dummy |


______________________________________________________________________

# 4. Live-data requirements

Your live engine does not need to predict from “all data.” It needs to fetch the **latest available values of the exact features used in training**.

## A. Live G-Sec feed

Fetch these before each prediction:


| Live input | Update frequency | Example use |
| :-- | --: | :-- |
| Latest 10-year G-Sec yield | Intraday or end-of-day | Base input for prediction |
| Latest 2-year, 5-year, 91-day yields | Intraday or end-of-day | Yield-curve features |
| Latest G-Sec volume and trade count | End-of-day | Liquidity features |
| Latest repo rate | Event-based | Policy feature |
| Latest RBI liquidity condition | Daily/weekly | Liquidity feature |
| Latest CPI/WPI | Monthly, with publication date | Inflation feature |
| Latest IIP/GDP | Monthly/quarterly, with publication date | Growth feature |
| Latest government borrowing | Weekly/event-based | Supply feature |
| Latest USD/INR | Intraday or daily | Currency feature |
| Latest Brent crude | Intraday or daily | Inflation/external-shock feature |
| Latest US 10-year yield | Intraday or daily | Global-rate feature |
| Latest VIX and Nifty | Intraday or daily | Risk-sentiment feature |

## B. Live corporate-bond feed

For each selected corporate bond, fetch:


| Live input | Update frequency | Example use |
| :-- | --: | :-- |
| Latest bond clean price | Intraday/end-of-day | Calculate current yield |
| Latest bond yield | Intraday/end-of-day | Direct model input |
| Latest trading volume | Daily | Liquidity feature |
| Latest bid/ask yield | Intraday, if available | Liquidity and spread feature |
| Latest comparable G-Sec yield | Daily | Credit-spread calculation |
| Latest credit rating and outlook | Event-based | Credit-risk feature |
| Latest financial ratios | Quarterly/annual | Issuer-risk feature |
| Latest sector spread | Daily/weekly | Sector-risk feature |
| Latest issuer news | Event-based | Event-risk feature |
| Latest bond maturity and coupon | Static | Duration and cash-flow features |

## C. Live-data ingestion design

```text
Scheduled data fetcher
        ↓
Source APIs / CSV downloads
        ↓
Raw data store
        ↓
Validation and cleaning
        ↓
Feature-engineering service
        ↓
Trained model
        ↓
Prediction API
        ↓
Dashboard / alerts
        ↓
Prediction log and outcome tracking
```

---

## Rough Live data fetching Road Map

| Data | Recommended source | Fetch method | Update level |
| :-- | :-- | :-- | :-- |
| Indian G-Sec yields | RBI DBIE, CCIL | API / scheduled download | Daily; hourly only if source provides it |
| T-Bill yields | RBI DBIE, CCIL | API / scheduled download | Daily |
| G-Sec yield curve | CCIL | API / download | Daily |
| G-Sec trades and volume | CCIL | API / download | Daily |
| G-Sec auctions | RBI / CCIL | API / scheduled scrape | Event-based |
| Corporate-bond trades | SEBI, NSE, BSE | API / scheduled download | Daily |
| Corporate-bond prices and yields | NSE/BSE, authorised market-data provider | API / download | Daily; intraday only with a licensed feed |
| Repo rate and MPC decisions | RBI | API / RSS / scheduled scrape | Event-based |
| CPI, WPI, GDP, IIP | RBI DBIE, MoSPI | API / scheduled download | On release |
| USD/INR | RBI, financial-data provider | API | Hourly or daily |
| Brent crude | Financial-data provider | API | Hourly or daily |
| US 10-year Treasury yield | Financial-data provider | API | Hourly or daily |
| VIX / Nifty | Financial-data provider | API | Hourly or daily |
| Credit ratings | CRISIL, ICRA, CARE, agency websites | Scheduled scrape / manual update | Event-based |
| Corporate financials | Company filings, NSE/BSE, financial-data provider | API / download | Quarterly/annual |

## Important distinction

Do not assume every source has a public real-time API. For your capstone, use this hierarchy:

1. **Official public APIs/downloads** — RBI DBIE, SEBI, CCIL where available.
2. **Scheduled scraping** — only for public pages that permit it and do not have an API.
3. **Commercial market-data API** — needed if you require reliable intraday bond pricing, dealer quotes, or corporate-bond tick data.
4. **Manual upload** — acceptable for a capstone demo if a particular dataset is not available through an API.

______________________________________________________________________

# 2. Three update levels

## Level 1: Hourly updates

Use hourly updates only for **fast-moving market indicators** that can influence bond yields during the day.


| Data | Update frequency | Why |
| :-- | --: | :-- |
| USD/INR exchange rate | Hourly | Currency movement can affect inflation and foreign-flow expectations |
| Brent crude price | Hourly | Oil-price movement affects inflation expectations |
| US 10-year Treasury yield | Hourly | Global rate expectations influence Indian bonds |
| VIX | Hourly | Measures global risk sentiment |
| Nifty 50 or Sensex | Hourly | Broad Indian risk-on/risk-off indicator |
| India VIX | Hourly | Indian-market volatility |
| Dollar Index | Hourly | Global dollar strength |
| Gold price | Hourly | Optional macro-hedge indicator |

### Does hourly make sense for bonds?

**Yes, but only partly.**

Hourly updates make sense for:

- The latest available G-Sec yield, if your data provider offers intraday quotes.
- USD/INR, crude oil, US yields, VIX, and Nifty.
- Recalculating technical indicators.
- Refreshing a dashboard.

Hourly updates usually do **not** make sense for:

- CPI, WPI, GDP, IIP, fiscal deficit.
- Credit ratings.
- Quarterly financial statements.
- Government borrowing calendars.
- Corporate-bond settlement data.
- Historical training data.

For Indian G-Secs, hourly yield updates are useful only if you can obtain a reliable intraday quote feed. Otherwise, update bond yields **once daily after market close**.

## Level 2: Daily updates

This should be your main update level for the prediction engine.


| Data | Update time | Why |
| :-- | --: | :-- |
| G-Sec yields | After market close, around 5–6 PM IST | Captures the day’s final market level |
| T-Bill yields | After market close | Updates short-term rate conditions |
| Yield curve | After market close | Updates curve slope and curvature |
| G-Sec trading volume | After market close | Updates liquidity features |
| Corporate-bond prices and yields | After market close | Updates bond-specific valuation |
| Corporate-bond trading volume | After market close | Updates liquidity features |
| Corporate-bond credit spreads | After market close | Updates issuer-risk features |
| USD/INR, crude, US yields, VIX, Nifty | After market close | Creates a stable daily feature snapshot |
| Corporate-bond trade data | After market close or next morning | SEBI reports use settlement-date data |

### Recommended daily schedule

```text
5:30 PM IST — Fetch G-Sec yields, T-Bill yields, yield curve
5:35 PM IST — Fetch G-Sec volume and trades
5:40 PM IST — Fetch corporate-bond prices, yields, and volumes
5:45 PM IST — Fetch USD/INR, crude, US yields, VIX, Nifty
5:50 PM IST — Validate and clean all data
5:55 PM IST — Build features
6:00 PM IST — Run prediction model
6:05 PM IST — Update dashboard and store prediction
```

This is the most realistic approach for a capstone product.

## Level 3: Weekly updates

Use weekly updates for data that changes slowly or is released weekly.


| Data | Update frequency | Why |
| :-- | --: | :-- |
| Government borrowing calendar | Weekly | Planned auctions and issuance affect supply expectations |
| RBI weekly liquidity data | Weekly | Captures banking-system liquidity conditions |
| Money-market aggregates | Weekly | Useful for liquidity and short-rate analysis |
| Market summary | Weekly | Useful for reporting and dashboard trends |
| Model-performance review | Weekly | Tracks live prediction accuracy |
| Feature-drift check | Weekly | Detects whether input distributions have changed |


______________________________________________________________________

# 3. Event-based updates

Some data should not be fetched on a fixed hourly/daily/weekly schedule. Fetch it immediately when it is published.


| Event | Trigger | Data to update |
| :-- | :-- | :-- |
| RBI MPC decision | Policy announcement | Repo rate, stance, policy-change feature |
| CPI/WPI release | Publication date | Inflation features |
| GDP release | Publication date | Growth feature |
| IIP release | Publication date | Industrial-activity feature |
| G-Sec auction | Auction date | Cut-off yield, notified amount, bid-to-cover ratio |
| Corporate earnings | Filing date | Financial ratios and issuer features |
| Credit-rating change | Rating announcement | Rating, outlook, rating-change feature |
| Bond issuance | Issue date | Bond details and outstanding amount |
| Default or restructuring | Event date | Credit-risk feature and alert |


______________________________________________________________________

# 4. Where to store updates

Use a simple three-layer storage design:

```text
Raw data store
      ↓
Clean data store
      ↓
Feature store
```


## A. Raw data store

Store the data exactly as received from the source.

Examples:

- `raw/gsec_yields/2026-11-14.csv`
- `raw/corporate_bonds/2026-11-14.csv`
- `raw/macro/cpi/2026-10.csv`
- `raw/rbi_policy/repo_rate.json`

Store:

- Source name.
- Download timestamp.
- Source URL or API endpoint.
- Raw response.
- Data-version or file hash.

This lets you audit and reload data if a source changes.

## B. Clean data store

Store cleaned, standardized data.

Examples:

- `clean/gsec_yields.parquet`
- `clean/corporate_bonds.parquet`
- `clean/macro_indicators.parquet`
- `clean/rbi_policy_events.parquet`

Standardize:

- Date format.
- Timezone.
- ISIN.
- Yield units.
- Currency.
- Missing-value flags.
- Duplicate records.


## C. Feature store

Store the final model-ready features.

Examples:

- `features/gsec_features.parquet`
- `features/corporate_bond_features.parquet`
- `features/live_snapshot.parquet`

This is the table your prediction model reads.

For a capstone, you can use:

- **SQLite** for a simple local application.
- **PostgreSQL** for a more production-like system.
- **Parquet files** for batch ML training and feature storage.
- **Redis** only if you need very fast caching of live indicators.

# 6. Practical recommendation

For your project, use this setup:


| Data | Update frequency | Storage |
| :-- | --: | :-- |
| G-Sec yields | Daily after market close | `bond_yields` |
| T-Bill yields | Daily after market close | `bond_yields` |
| Yield curve | Daily after market close | `yield_curve` |
| G-Sec volume | Daily after market close | `bond_trades` |
| Corporate-bond prices/yields | Daily after market close | `corporate_bond_prices` |
| Corporate-bond volume | Daily after market close | `corporate_bond_trades` |
| USD/INR, crude, US yield, VIX, Nifty | Hourly during market hours | `live_market_snapshot` |
| CPI, WPI, GDP, IIP | Event-based on release | `macro_indicators` |
| Repo rate and MPC | Event-based | `rbi_policy_events` |
| Credit ratings | Event-based | `credit_ratings` |
| Corporate financials | Quarterly/annual | `issuer_financials` |
| Prediction results | After every prediction | `predictions` |

## Final recommendation

Use **hourly updates for external market indicators**, **daily updates for bond yields and corporate-bond data**, and **event-based updates for macro releases and policy decisions**.

This is realistic because:

- Bond yields do not always change every hour.
- Indian corporate bonds often trade infrequently.
- Macro data is published at fixed intervals.
- A daily bond-yield snapshot is usually enough for a next-day or next-week forecast.
- Hourly external indicators still let the dashboard feel live and responsive.

---

# Extras

## Recommended database tables

### `bond_yields`

| Column | Type |
| :-- | :-- |
| date | DATE |
| isin | TEXT |
| security_name | TEXT |
| issuer_type | TEXT |
| maturity_date | DATE |
| coupon | FLOAT |
| yield | FLOAT |
| clean_price | FLOAT |
| volume | FLOAT |
| source | TEXT |
| fetched_at | TIMESTAMP |

### `macro_indicators`

| Column | Type |
| :-- | :-- |
| indicator_name | TEXT |
| observation_date | DATE |
| publication_date | DATE |
| value | FLOAT |
| unit | TEXT |
| frequency | TEXT |
| source | TEXT |
| fetched_at | TIMESTAMP |

### `live_market_snapshot`

| Column | Type |
| :-- | :-- |
| snapshot_time | TIMESTAMP |
| gsec_10y_yield | FLOAT |
| tbill_91d_yield | FLOAT |
| yield_2y | FLOAT |
| yield_5y | FLOAT |
| usd_inr | FLOAT |
| brent_crude | FLOAT |
| us_10y_yield | FLOAT |
| vix | FLOAT |
| nifty_close | FLOAT |
| source | TEXT |

### `predictions`

| Column | Type |
| :-- | :-- |
| prediction_id | TEXT |
| bond_isin | TEXT |
| prediction_time | TIMESTAMP |
| horizon | TEXT |
| predicted_yield | FLOAT |
| predicted_direction | TEXT |
| confidence_lower | FLOAT |
| confidence_upper | FLOAT |
| model_version | TEXT |
| feature_snapshot | JSON |
| actual_yield | FLOAT |
| actual_outcome_time | TIMESTAMP |

