Objective:
To build a robust Asset-Liability Management (ALM) framework that immunizes a bond portfolio against interest rate risk by matching the duration and convexity of assets to liabilities. The goal is to ensure the portfolio remains fully funded across a range of interest rate environments and to quantify the funding gap that arises when duration mismatches exist.

Process:
Portfolio & Liability Metrics — Computed the weighted duration and convexity for both the asset portfolio and the liability structure to establish a baseline for comparison.
Duration Gap Analysis — Calculated the Duration Gap (Portfolio Duration − Liability Duration) to identify the degree of interest rate mismatch between assets and liabilities.
Portfolio Rebalancing — Flagged portfolios with a non-zero duration gap and rebalanced the asset mix to bring the portfolio duration closer to the liability duration target.
Convexity Matching — Evaluated convexity on both sides of the balance sheet to ensure second-order price sensitivity is aligned, reducing residual risk after duration matching.
Interest Rate Shock Analysis — Simulated rate shocks of -2% to +2% in 1% increments and measured the divergence between asset price changes and liability price changes under each scenario.
Funding Ratio Evaluation — Computed the Funding Ratio (Assets / Liabilities) to determine whether the portfolio is fully funded, overfunded, or underfunded at the current rate level.

Results:
Portfolio & Liability Risk Metrics
| Metric | Value |
|---|---|
| Portfolio Duration | 4.35 years |
| Liability Duration | 4.80 years |
| Portfolio Convexity | 28.50 |
| Liability Convexity | 30.00 |
| Duration Gap | -0.45 |
| Funding Ratio | 1.00 |

Interpretation:
The Portfolio Duration of 4.35 is shorter than the Liability Duration of 4.80, producing a Duration Gap of -0.45. A negative gap means assets are less sensitive to rate changes than liabilities — when rates fall, liabilities will increase in value faster than assets, creating a funding shortfall.

The convexity gap of -1.50 (28.50 vs. 30.00) further confirms that liabilities have slightly more curvature than assets, meaning liabilities benefit more from large rate moves in either direction.

A Funding Ratio of 1.00 indicates the portfolio is exactly fully funded at the current rate level — assets equal liabilities in present value terms. Any rate movement, however, risks pushing this ratio below 1.00 due to the duration and convexity mismatches.

Portfolio Rebalancing
| Metric | Before Rebalancing | After Rebalancing |
|---|---|---|
| Portfolio Duration | 4.35 | 3.98 |
| Target Liability Duration | 4.80 | 4.80 |
| Duration Gap | -0.45 | -0.82 |
| Rebalancing Status | Required | In Progress |

Interpretation:
The initial Duration Gap of -0.45 triggered a rebalancing flag. Post-rebalancing, the portfolio duration moved to 3.98, still short of the 4.80 liability target.

This suggests that the rebalancing step adjusted the asset mix but has not yet fully closed the gap — further allocation to longer-duration bonds is required to achieve complete immunization.

Reducing the duration gap to zero is the immunization objective; until that is achieved, the portfolio retains residual interest rate risk on the liability side.

Interest Rate Shock Analysis
| Rate Shock (%) | Asset Change (%) | Liability Change (%) |
|---|---|---|
| -2% | +9.27 | +10.20 |
| -1% | +4.49 | +4.95 |
| 0% | 0.00 | 0.00 |
| +1% | -4.21 | -4.65 |
| +2% | -8.13 | -9.00 |

Interpretation:
At every shock level, liabilities move more than assets — both in gains and losses — directly reflecting the negative duration gap of -0.45.

Under a -2% rate shock, assets gain 9.27% while liabilities gain 10.20%, a divergence of +0.93%. This means the portfolio's net asset value (Assets − Liabilities) deteriorates when rates fall sharply.

Under a +2% rate shock, assets lose 8.13% while liabilities lose 9.00%, a divergence of 0.87% in the portfolio's favor. A rising rate environment slightly benefits this portfolio given assets are shorter in duration than liabilities.

The shock analysis confirms the core ALM principle: a negative duration gap exposes the portfolio to falling rates, not rising rates. The risk is asymmetric and greatest on the downside.


Tech Stack:Numpy,Pandas,Matplotlib.

Future Enhancements:
Dynamic Rebalancing Engine — Automate portfolio rebalancing whenever the duration gap exceeds a defined threshold (e.g., ±0.10).

Key Rate Duration (KRD) — Extend analysis beyond parallel shifts to model non-parallel yield curve movements using KRDs at specific tenor points.

Stochastic Rate Scenarios — Replace deterministic shocks with Monte Carlo simulations across thousands of rate paths to produce probabilistic funding ratio distributions.

Multi-Liability Matching — Handle pension-style ALM with multiple liability tranches across different payment horizons.

Real Bond Universe Integration — Source live bond data (e.g., US Treasuries, investment-grade corporates) to run immunization on actual market instruments.

Surplus Optimization — Extend the framework to maximize portfolio surplus (Assets − Liabilities) subject to a duration gap constraint using convex optimization.


Key Insights:
Duration gap is the primary risk driver — A gap of just -0.45 years is enough to generate a 0.93% funding divergence under a -200 bps shock, illustrating how even small mismatches compound under stress.

Negative duration gap favors rising rates — Assets losing 8.13% vs. liabilities losing 9.00% under a +2% shock means this portfolio actually gains net asset value when rates rise, making it directionally exposed to rate declines.

Convexity mismatch adds second-order risk — The portfolio convexity (28.50) is lower than liability convexity (30.00), meaning the immunization is imperfect even after duration is matched; large rate moves in either direction will still cause funding leakage.

Funding ratio of 1.00 is a knife's edge — Being exactly fully funded is only safe when duration and convexity are perfectly matched. With a -0.45 gap, the portfolio is one rate rally away from a funding deficit.

Rebalancing alone is insufficient — Post-rebalancing duration of 3.98 still falls short of the 4.80 target, highlighting that immunization is an iterative process requiring continuous monitoring and adjustment as rates and bond prices evolve.
