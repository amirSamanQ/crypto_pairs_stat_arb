# crypto_pairs_stat_arb

A collection of experiments in **statistical arbitrage** on crypto pairs (focused on BTC/ETH).  
The project covers the entire workflow: fetching market data, testing stationarity, simulating pair trading strategies, and running parameter grid searches.

---

## 📂 Project Structure


---

## 🛠 Features

- **Data Fetching**: Download Binance Futures kline (candlestick) data with a sliding window approach.
- **Stationarity Testing**: Use ADF (Augmented Dickey-Fuller) and KPSS tests to verify mean-reversion properties of BTC/ETH ratio and spread.
- **Backtesting**: Simulate a pair trading strategy (sell BTC & buy ETH when spread > upper bound, and vice versa).
- **Grid Search**: Optimize hyperparameters (`k`, `fee_rate`, `window_size`) to evaluate strategy performance under different conditions.

---

## 📊 Methodology

1. **Spread Definition**  
   - Ratio: `BTC / ETH`  
   - Difference: `BTC - ETH`  

2. **Stationarity Tests**  
   - ADF → H0: unit root (non-stationary)  
   - KPSS → H0: stationary  

3. **Trading Logic**  
   - Compute rolling mean and std of the spread.  
   - Define:
     ```
     upper_bound = mean + k * std
     lower_bound = mean - k * std
     ```
   - If spread > upper → Sell BTC, Buy ETH  
   - If spread < lower → Buy BTC, Sell ETH  
   - Partial rebalancing (e.g., $200 per trade), including transaction fees.

4. **Evaluation**  
   - Compare strategy vs Buy & Hold BTC, ETH, and 50/50 portfolio.  
   - Track total trades, average interval between trades, and returns.  

---

## ⚙️ Installation

Clone the repository:
```bash
git clone https://github.com/amirSamanQ/crypto_pairs_stat_arb.git
cd crypto_pairs_stat_arb
