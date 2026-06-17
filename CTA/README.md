# Rates CTA Project Knowledge Map and Potential Directions

This document breaks a “rates CTA project from a bank S&T perspective” into three layers: first understand rates, then understand CTA, then turn the two into a project that can support research, backtesting, monitoring, and client-facing discussion. The companion notebook, `rates_cta_classic_cases.ipynb`, uses offline synthetic rates data to walk through several classic practical cases.

> Disclaimer: This material is for learning, research, and project design only. It is not investment or trading advice. Real trading requires official data, transaction costs, compliance constraints, model validation, and risk approval.

## 1. Rates CTA in One Sentence

Rates CTA means applying systematic CTA, trend-following, and risk-control methods to interest-rate assets. Tradable instruments usually include government bond futures, short-rate futures, IRS/OIS swaps, government bonds, cross-market rates curves, and combinations of these instruments.

The core idea is not to predict one specific central-bank meeting. It is to use disciplined signals to capture rates trends, curve trends, carry/roll-down, and cross-market relative strength, while managing risk through volatility targeting, DV01, stop-loss rules, and portfolio correlation controls.

## 2. Why a Bank S&T Desk Might Build This Project

In bank S&T, a rates CTA project may be much more than “just a strategy backtest.” It can serve several business use cases:

1. **Client content and market explanation**
   - Explain to institutional clients whether a rates trend-following model is currently long or short duration.
   - Analyze possible CTA positioning, stop-loss pressure, and rebalancing demand during recent rates moves.
   - Produce a weekly systematic rates monitor.

2. **Trading desk risk support**
   - Monitor trend, carry, and volatility signals across major rates markets.
   - Identify CTA crowdedness. For example, when U.S. Treasury futures trend signals are heavily aligned, NFP/CPI/FOMC events may create position-adjustment risk.
   - Give traders a systematic “market state dashboard.” It does not replace trader judgment; it complements it.

3. **Strategy research and index products**
   - Design a rates trend-following index, rates carry index, or curve CTA basket.
   - Provide explainable rules for structured products, overlays, or risk-premia products.
   - Package the strategy into a client-facing backtest factsheet.

4. **Portfolio overlay and hedging**
   - Build a systematic duration overlay for bond portfolios.
   - Dynamically adjust duration, curve exposure, and market weights across rates regimes.
   - Study whether rates CTA provides “crisis alpha” during bond selloffs or rallies.

5. **Internal research platform**
   - Build a reusable backtesting engine covering data cleaning, continuous contracts, signals, transaction costs, and risk reports.
   - Extend the same platform later to FX CTA, commodity CTA, or cross-asset macro CTA.

## 3. Rates Foundations You Need to Know

### 3.1 The Price-Yield Relationship

The most important approximation is:

```text
Bond/futures long-duration PnL ≈ -Duration × ΔYield
```

If you are long duration:

- Yields fall, prices rise, and the strategy makes money.
- Yields rise, prices fall, and the strategy loses money.

In real trading, you also need to consider:

- **DV01/PV01**: The change in position value for a 1bp move in rates.
- **Duration**: First-order price sensitivity to yield changes.
- **Convexity**: Second-order price sensitivity to yield changes.
- **Carry**: The natural return earned or paid while holding the position.
- **Roll-down**: The gain or loss from a bond or swap “rolling” to a shorter maturity point on the curve, assuming the curve shape is unchanged.

### 3.2 Common Instruments

1. **Government bond futures**
   - U.S. Treasury futures: TU, FV, TY, US, WN.
   - Europe: Bund, Bobl, Schatz, Buxl.
   - U.K.: Gilt futures.
   - Japan: JGB futures.
   - Australia, Canada, and other markets also have futures.
   - Key details: CTD, conversion factor, delivery option, roll calendar, and continuous contract construction.

2. **Short-rate futures**
   - SOFR futures and Fed Funds futures.
   - Euribor, SONIA, SARON, and others.
   - These are closer to central-bank path expectations and front-end repricing.

3. **IRS/OIS swaps**
   - Receiver swap: similar to long duration; it makes money when rates fall.
   - Payer swap: similar to short duration; it makes money when rates rise.
   - Curve trades are possible, such as 2s10s, 5s30s, and butterflies.

4. **Cash government bonds**
   - Better reflect carry, roll-down, repo/funding, and specialness.
   - Data and execution are more complex.

### 3.3 Curves and Factors

Rates markets are often understood through three intuitive factors:

- **Level**: The whole curve shifts up or down.
- **Slope**: Short-end rates move relative to long-end rates, such as 2s10s steepeners or flatteners.
- **Curvature**: The belly moves relative to the wings, such as a 2s5s10s butterfly.

A rates CTA does not have to trade only level trends. It can also trade:

- Duration trend: for example, trend-following in TY, Bund, or JGB.
- Curve trend: for example, persistent steepening or flattening in 2s10s.
- Cross-market trend: for example, long JGB duration and short UST duration.
- Carry/roll-down: favoring the curve points with better roll-down.
- Signal blends: trend + carry + volatility regime.

## 4. CTA Foundations

### 4.1 Time-Series Momentum

A classic CTA signal is:

```text
Past N-day return is positive -> go long
Past N-day return is negative -> go short
```

Common lookbacks:

- 1 month: about 21 trading days.
- 3 months: about 63 trading days.
- 6 months: about 126 trading days.
- 12 months: about 252 trading days.

Rates CTA usually does not rely on one single lookback. It often blends multiple speeds to reduce parameter overfitting.

### 4.2 Volatility Targeting

The key to CTA is often not “how smart the signal is,” but whether the risk unit is consistent:

```text
Position size ∝ target volatility / realized volatility
```

If a market has become more volatile, the position automatically decreases. If volatility has fallen, the position increases. Real trading also requires leverage caps, margin caps, DV01 caps, and liquidity caps.

### 4.3 Portfolio Construction

Common methods include:

- Equal weighting after volatility targeting.
- Inverse volatility weighting.
- Risk parity.
- Covariance-aware allocation.
- Drawdown-based deleveraging.
- Signal confidence weighting.

In rates, there is also a hidden risk: several markets may appear to be separate assets, but correlations can rise sharply during risk-on/risk-off moves or synchronized central-bank cycles.

### 4.4 Transaction Costs

At minimum, a backtest should consider:

- Bid/ask spread.
- Futures roll cost.
- Slippage.
- Funding and margin.
- Swap execution cost.
- Market impact, especially in less liquid curve points.

A rough but useful first version can model cost as:

```text
cost = turnover × cost_per_unit
```

## 5. Possible Rates CTA Project Directions

### Direction A: Rates Trend-Following Backtest

Goal: Build a clean and explainable rates CTA prototype.

Minimum version:

- Input: continuous prices for major government bond futures, or yield proxies.
- Signal: 1M/3M/6M/12M trend.
- Risk control: volatility targeting + leverage cap.
- Cost: turnover-based transaction cost.
- Output: Sharpe, drawdown, rolling volatility, position history, and market contribution.

This is a good way to demonstrate coding ability, rates intuition, and backtesting hygiene.

### Direction B: CTA Positioning / Flow Monitor

Goal: Infer the likely direction of systematic funds from price trends, volatility, and public positioning data.

Possible data:

- Futures prices.
- Realized volatility.
- CFTC COT positions.
- Estimated trend signals.
- CTA benchmark replication.

Outputs:

- Current model position: long, short, or flat duration.
- Position crowdedness.
- Signal flip level: the price or yield level that would trigger a trend reversal.
- Event risk: positioning fragility around CPI, FOMC, or NFP.

This type of project is especially useful for bank S&T because it can directly support client conversations.

### Direction C: Carry + Roll-Down Rates Strategy

Goal: Use curve shape to identify the tenors and markets with more attractive holding returns.

Typical questions:

- Which market has the best roll-down for long-duration exposure?
- Which tenor, 2Y/5Y/10Y/30Y, has the most attractive carry/roll?
- What should the model do when carry and trend signals conflict?

Key points:

- Real carry/roll requires curve data, coupons, funding, repo, futures CTD, or swap curve analytics.
- A first version can use zero-coupon or swap curve approximations.

### Direction D: Curve CTA

Goal: Trade not only level, but also curve slope and butterflies.

Examples:

- 2s10s trend-following: if the curve steepened over the past 3 months, enter a steepener; if it flattened, enter a flattener.
- 5s30s mean reversion or momentum.
- 2s5s10s butterfly: the belly is rich or cheap relative to the wings.

Key points:

- The trade must be DV01-neutral. Otherwise, you may think you are trading curve, while in reality you are mainly trading duration.
- Curve trade costs and liquidity differ from outright duration trades.

### Direction E: Regime-Aware Rates CTA

Goal: Adjust signals or risk according to the macro regime.

Possible regimes:

- High inflation vs low inflation.
- Central-bank hiking cycle vs cutting cycle.
- High volatility vs low volatility.
- Risk-off recession scare vs soft landing.

Methods:

- Label regimes using realized volatility, yield trends, or curve inversion.
- Complex machine learning is not required. Simple rules are often easier to explain.

### Direction F: Production Dashboard

Goal: Make something traders and sales can check every day.

Modules:

- Market state: yield changes, curve changes, and volatility.
- CTA signal: trend, carry, roll, and blended score.
- Position estimate: target DV01, position change, and turnover.
- Risk: stress shocks, VaR, and drawdown.
- Events: CPI, FOMC, NFP, and auction calendar.

## 6. Data and Engineering Considerations

### 6.1 Data Sources

Real projects may use:

- Bloomberg: futures, swaps, curves, CFTC data, calendars.
- Refinitiv/Eikon.
- CME/ICE/Eurex settlement data.
- FRED: Treasury yields and macro series.
- Internal bank curves and analytics.

Research prototypes can start with:

- Public yields.
- Futures settlement CSV files.
- Synthetic data to validate the framework.

### 6.2 Continuous Contracts

Government bond futures cannot be naively stitched using the front contract, because roll dates can create artificial jumps. Common methods include:

- Back-adjusted continuous prices.
- Ratio-adjusted prices.
- Return-spliced series.
- Rolling by open interest or fixed roll dates.

The roll rule must be recorded. Otherwise, the backtest is not reproducible.

### 6.3 Backtest Hygiene

Avoid:

- Look-ahead bias.
- Survivorship bias.
- Generating a signal from the close and trading the same close.
- Ignoring transaction costs.
- Ignoring holidays and time zones.
- Treating yield levels as futures total returns.
- Mixing price returns, excess returns, yield bp changes, and DV01 PnL.

Recommended practice:

- Use close data on day `t` to generate the signal, and apply the position from day `t+1`.
- Use only past data for volatility and normalization.
- Be explicit about units: price return, yield bp, and DV01 PnL should not be mixed casually.

## 7. How to Present the Project in an Interview or Project Discussion

You can describe the project as a staged plan:

1. **Phase 1: Research prototype**
   - Use major rates futures or yield proxies to build a trend-following backtest.
   - Output strategy returns, positions, risk, and attribution.

2. **Phase 2: Rates-specific enhancement**
   - Add carry/roll-down, curve CTA, and DV01-neutral risk.
   - Add realistic transaction costs and futures roll treatment.

3. **Phase 3: S&T productization**
   - Turn it into a daily monitor or client-facing dashboard.
   - Show CTA positioning, signal flip levels, and scenario stress.

4. **Phase 4: Validation**
   - Test parameter stability, market subsamples, event stress, and transaction-cost sensitivity.
   - Compare with existing CTA indices or trend benchmarks.

## 8. The 20 Questions You Should Clarify First

1. Are the tradable instruments futures, swaps, cash bonds, or analytics only?
2. Is the goal alpha research, risk monitoring, client content, or a product index?
3. What is the data source? Bloomberg, internal curves, or something else?
4. Is the frequency daily, intraday, or weekly?
5. Does it need to be executable, or is it research-only?
6. Is shorting allowed?
7. Is leverage allowed?
8. Is risk measured by volatility, DV01, VaR, or margin?
9. Are there market or tenor limits?
10. Does the strategy need cross-market allocation?
11. Should transaction costs and roll costs be included?
12. How will futures continuous contracts be built?
13. Is the swap curve OIS or IRS?
14. Which analytics library defines carry/roll-down?
15. Should convexity adjustment be included?
16. Is the signal pure trend, or trend + carry + value?
17. Does the project need to estimate CTA industry positioning?
18. Is the output for traders, sales, clients, or risk managers?
19. Is success measured by Sharpe, drawdown, explainability, or adoption?
20. Does the project eventually need a dashboard or automated report?

## 9. Recommended Minimum Deliverable

A strong, practical MVP could include:

- `README.md`: knowledge framework, assumptions, methodology, and risks.
- `rates_cta_classic_cases.ipynb`: offline runnable strategy cases.
- Data interface template: to be replaced later with Bloomberg, FRED, or internal curves.
- Strategy report: performance table, drawdown, positions, and stress.
- Daily monitor example: signal, target risk, recent PnL, and flip levels.

## 10. Companion Notebook Contents

`rates_cta_classic_cases.ipynb` includes:

1. Synthetic multi-market yield curve data.
2. Duration-based rates return proxy.
3. Classic 10Y rates trend-following.
4. Robustness comparison across multiple lookbacks.
5. 2s10s DV01-neutral curve CTA.
6. Carry/roll-down cross-sectional strategy.
7. Combined trend + curve + carry portfolio and stress report.

In a real project, you can replace the notebook’s synthetic data with official data while keeping the signal, backtest, risk-control, and reporting framework.
