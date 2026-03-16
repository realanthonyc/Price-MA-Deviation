# Price-MA Deviation (PMAD)

Price-MA Deviation (PMAD) is a TradingView Pine Script indicator designed to quantify how "stretched" the price is relative to its Moving Average. It normalizes this deviation onto a 0-100 scale, making it a powerful tool for identifying overextended market conditions across different timeframes.

## Why Use PMAD?

In trending markets, the distance between price and its Mean (Moving Average) constantly fluctuates. A simple "percentage from MA" doesn't tell you much because volatility changes. 

PMAD solves this by **normalizing the deviation based on its own historical range**:

- It doesn't just tell you that the price is 5% away from the MA.
- It tells you that a 5% deviation is the highest it has been in the last 200 bars (Level 100) or just a typical fluctuation (Level 50).

## Core Logic

1.  **Selection:** Choose your price source (defaults to `hlc3`), MA type (SMA/EMA), and period for both Fast and Slow tracks.
2.  **Calculation:** It measures the raw percentage difference: `(Price - MA) / MA * 100`.
3.  **Normalization:** It looks back over a user-defined window (`Normalization Lookback`) to find the historical High/Low of these deviations and maps the current value to a 0-100 scale.
 
In simplified form:

```text
raw deviation = (price - moving average) / moving average * 100
normalized deviation = position of current raw deviation inside its recent min-max range
```

## Interpreting the Dual-Line System

The strength of PMAD lies in the interaction between the **Fast Deviation** (thick line) and the **Slow Deviation** (thin line).

### The Power of Convergence & Divergence
- **Macro-Micro Alignment:** When both the Slow and Fast lines hit the extreme zones (above 85 or below 15) simultaneously, the market is "historically stretched" on multiple horizons. These are high-probability areas for mean reversion or significant trend exhaustion.
- **Short-term Pullbacks in Long-term Trends:** If the Slow line is holding steady around 50-60 (healthy uptrend) while the Fast line dips below 15, this often signals a "buy the dip" opportunity within a strong trend, rather than a reversal.
- **Normalization Divergence:** If the price makes a new high but the Fast PMAD reaches a lower peak than the previous one, it suggests the price is struggling to maintain its momentum away from the MA—often a precursor to a trend shift.

### Understanding the Scale

Here is a quick reference for the key PMAD levels and the default configuration (Fast: 20 EMA / 150 Lookback | Slow: 200 SMA / 200 Lookback):

| Level        | Zone              | Market Sentiment                                                     |
| :----------- | :---------------- | :------------------------------------------------------------------- |
| **85 - 100** | **Upper Stretch** | Extreme bullish extension. The "rubber band" is pulled to its limit. |
| **50**       | **Midpoint**      | Price is oscillating normally around its MA. Equilibrium.            |
| **0 - 15**   | **Lower Stretch** | Extreme bearish extension. Panic selling or climax near-term.        |

PMAD is best read as a momentum and volatility tool (or a relative stretch tool), not as a standalone buy or sell signal. An extreme reading (0 or 100) indicates extension, not an immediate reversal. Markets can remain stretched longer than most traders can remain solvent. Use this in conjunction with price action and volume.
