# Modernising the All-Weather Portfolio
## Introduction
### Modernising the All-Weather Portfolio takes the portfolio from Bridgewater Associates and changes it to address modern problems and phenomena's. The new portfolio aims to recreate the portfolio whilst diversifying from these new risks that the contemporary market faces.
## Motivation
### The original five-asset all-weather portfolio looks brittle given inflationary pressure from the Middle East, AI-driven equity concentration, the sovereign bond selloff and elevated gold prices.
### Three of the five assets face headwinds: equities (index concentration in AI), long-dated treasuries (sticky inflation, low G7 growth) and gold (a dollar rebound or a pause in central bank buying could unwind the rally).
### The approach is to reduce sensitivity to these headwinds by diversifying within each asset class and adding new securities.

## Results and Key findings
### Raising the equity weighting improved risk-adjusted returns and drawdown against the original portfolio, and the bond portfolio became less volatile.
### The GMV sleeve helped most, because its low volatility let it become a larger component.
## Results
![Cumulative growth](images/allcumulative_returns.png)
![Weightings for Portfolios](images/weights.png)
![Drawdown](images/drawdowns.png)
### Maintaining the drawdown performance of the original portfolios whilst gaining better returns.
|                                                       |   Annualized Return |   Annualized Vol |   Sharpe Ratio |   Sortino Ratio |   Calmar Ratio |   Skewness |   Kurtosis |   Cornish-Fisher VaR (5%) |   Historic CVaR (5%) |   Max Drawdown |   Max DD Duration (mo) |   Hit Rate |   Best Month |   Worst Month |
|:------------------------------------------------------|--------------------:|-----------------:|---------------:|----------------:|---------------:|-----------:|-----------:|--------------------------:|---------------------:|---------------:|-----------------------:|-----------:|-------------:|--------------:|
| Equal Weight Portfolio                                |               0.096 |            0.085 |          0.755 |           1.22  |          0.651 |     -0.412 |      2.842 |                     0.035 |                0.045 |         -0.148 |                     26 |      0.634 |        0.054 |        -0.064 |
| Risk Parity Portfolio                                 |               0.077 |            0.078 |          0.593 |           0.941 |          0.541 |     -0.463 |      2.984 |                     0.033 |                0.043 |         -0.143 |                     31 |      0.645 |        0.049 |        -0.063 |
| ERP with GMV                                          |               0.079 |            0.078 |          0.613 |           0.994 |          0.541 |     -0.433 |      2.933 |                     0.033 |                0.043 |         -0.147 |                     30 |      0.656 |        0.05  |        -0.062 |
| ERP with Sleeves                                      |               0.061 |            0.056 |          0.54  |           0.952 |          0.732 |     -0.368 |      2.619 |                     0.023 |                0.029 |         -0.084 |                     28 |      0.667 |        0.038 |        -0.038 |
| Bounded Equal Risk with Multi Asset Sleeves Portfolio |               0.086 |            0.075 |          0.722 |           1.226 |          0.94  |     -0.406 |      2.713 |                     0.031 |                0.04  |         -0.091 |                     27 |      0.677 |        0.052 |        -0.05  |

Key decisions
The uncapped sleeves portfolio put 59% in bonds, leaving it exposed to inflation and US policy shocks and lowering risk-adjusted return.
[Readdress] Confirm the 59% from your weights output.
A 40% cap was chosen because Sortino and Sharpe gains fade as the cap tightens, and volatility and drawdown rise faster beyond a 30% cap.
[Readdress] “Past 30%” is ambiguous. Do you mean below 30%? Fix the wording and put the cap table directly under this bullet.
A 38% cap had the best Sortino and hit rate, but picking it would overfit the weights to this data.
[Readdress] Check this against the cap table, since the README claim has to match the numbers.
ERC weights were chosen over GMV to avoid concentration in long-dated treasuries and gold.
[Readdress] This is in your earlier notes but missing from this conclusion. Add it back.

|                |   Annualized Return |   Annualized Vol |   Sortino Ratio |   Max Drawdown |   Hit Rate |
|:---------------|--------------------:|-----------------:|----------------:|---------------:|-----------:|
| NO Constraints |               0.061 |            0.056 |           0.952 |         -0.084 |      0.667 |
| 40%            |               0.086 |            0.075 |           1.226 |         -0.091 |      0.677 |
| 38%            |               0.088 |            0.077 |           1.234 |         -0.092 |      0.677 |
| 30%            |               0.098 |            0.085 |           1.229 |         -0.096 |      0.656 |

Limitations
Weights aren’t rebalanced using previous data, and without rebalancing the weighting scheme becomes less relevant the longer the backtest runs.
[Readdress] Two problems. Your claim that gold and equities “grow unrestricted” depends on how erk.backtest_ws applies the weights. If it multiplies fixed weights by each month’s returns, that is monthly rebalancing to constant weights, and assets can’t drift. Check the function before you state this. The cleaner limitation is the one you already have in the code: the weights come from covariance estimated on the full sample from 2016 and are then held fixed, so results are in-sample.
The new instruments only have history from 2016 and 2019.
Add that the backtest window starts in 2019.
The original portfolio covers the financial crash, so it performs in a bear market, but you would have liked to test the new portfolio there.
[Readdress] This reads as contradictory. Your results table starts in 2019, so it can’t show bear-market performance. Either show the 2007+ results for the original five-asset portfolio and say plainly that the new one is untested through the GFC, or cut the bear-market claim.
The returns could be affected by the recent equity and gold rally.
[Readdress] Replace “high returns” with “returns”. Your bounded portfolio’s 8.6% is below equal weight’s 9.6%, so “high” invites the wrong question.
Drawdown duration barely changed across caps (27 to 28 months), so max drawdown is the better measure.
[Readdress] “Inputting a cap from 27 months to 28” is garbled. Say the duration moved from 27 to 28 months across caps.
Next steps
Extend the backtest further back.
Estimate ERC and GMV portfolios on the past three years of data, then rebalance with the max-weight logic, possibly letting some positions grow before profit-taking.
Include rebalancing costs.
Adapt the portfolio for different rate regimes (falling and rising rates).
Test a leveraged risk parity version.

