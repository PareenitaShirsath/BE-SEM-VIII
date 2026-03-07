# EXPERIMENT 5

## AIM
Developing and Backtesting a Simple Trading Algorithm

---

## THEORY

### Simple Moving Averages (SMAs)

A Simple Moving Average (SMA) is the average price of an asset over a specific period.  
It is calculated by adding the closing prices of the asset over a certain time period and dividing by the number of periods.

SMAs help smooth out price fluctuations and identify market trends.

- A **shorter-term SMA** reacts more quickly to price changes.
- A **longer-term SMA** provides a smoother indication of the trend.

In this experiment, two SMAs are calculated:

- **SMA_Short** : Window of **2 days**
- **SMA_Long** : Window of **3 days**

---

### Trading Strategy: SMA Crossover

The strategy used in this experiment is based on **SMA crossover signals**.

- When the **short-term SMA crosses above the long-term SMA** → **Buy Signal (Uptrend)**
- When the **short-term SMA crosses below the long-term SMA** → **Sell Signal (Downtrend)**

The main idea of this strategy is:

- **Buy when prices start rising**
- **Sell when prices start falling**

---

### Backtesting

Backtesting is the process of applying a trading strategy to **historical market data** to evaluate its performance.

In this experiment:

- The algorithm simulates trading based on generated **buy/sell signals**.
- The system calculates **portfolio value** and **profit or loss**.

**Limitations of Backtesting:**

- Results are based on past data.
- Past performance does **not guarantee future results**.

---

### Assumptions and Considerations

- **Simplified Model**  
  The model does not consider transaction costs, slippage, or sudden market volatility.

- **Parameter Optimization**  
  The choice of SMA window size affects the performance of the trading strategy.

- **Risk Management**  
  Real-world trading requires proper risk management techniques, which are not included in this model.

---

## Applications

### 1. Algorithmic Trading

#### Automated Trading Systems
- Automates buy and sell decisions using real-time market data.
- Reduces emotional bias in trading.
- Improves execution speed.

#### High-Frequency Trading (HFT)
- Detects short-term price fluctuations.
- Executes trades extremely quickly.
- Requires advanced infrastructure.

---

### 2. Portfolio Management

- **Trend Following**  
  Helps identify trends in stocks, bonds, commodities, and currencies.

- **Risk Management**  
  SMAs can be used to set **trailing stop-loss orders** to limit losses.

---

### 3. Financial Analysis and Research

- **Technical Analysis**  
  Used to identify trends, support and resistance levels, and trading opportunities.

- **Backtesting & Strategy Development**  
  Helps analysts evaluate trading strategies using historical data.

---

### 4. Other Applications

- **Inventory Management**  
  Used for forecasting demand and optimizing stock levels.

- **Economic Forecasting**  
  Helps identify trends in GDP, inflation, and economic indicators.

- **Signal Processing**  
  Used to extract meaningful patterns from noisy data.

---

## CONCLUSION

Thus, we have successfully developed and backtested a **simple trading algorithm using the SMA crossover strategy**.  
The experiment demonstrates how historical data can be used to test trading strategies and analyze their potential performance.
