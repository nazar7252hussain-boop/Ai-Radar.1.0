AI Radar — Android project (upgraded dashboard)

Included dashboard:
- Top 10 crypto market-cap rankings (CoinGecko)
- BTC, ETH, BNB, XRP, SOL, USDC, TRX, DOGE, ADA and BCH market selector
- Gold (XAU) and Silver (XAG) indicative spot quotes (Gold-API)
- DeFi protocol top 10 and TVL (DeFiLlama)
- Short-term signal using 5-minute Binance candles
- Long-term signal using 4-hour Binance candles
- RSI(14), MACD and EMA(20) rule-based indicators
- CoinDesk and Cointelegraph RSS headline sentiment
- Binance USD-M perpetual funding rate and current open interest (where supported)
- CoinGecko BTC market-cap dominance
- 1-hour historical rule-strategy backtest using up to 500 candles; signals are tested against the following candle
- On-device signal history with rough next-refresh outcome tracking (local storage)

Build APK:
1. Upload the contents of this project folder to a GitHub repository.
2. Open Actions and run "Build Android APK" (or push to main).
3. Download the AI-Radar-debug-apk artifact from the completed workflow.
4. Extract app-debug.apk on Android and install it. Android may ask permission to install unknown apps.

This ZIP is an Android Studio project with a cloud GitHub Actions build workflow, not a compiled APK.
Gold/Silver technical BUY/SELL signals are deliberately shown as WAIT because this build does not have historical metal candles. Metal spot quotes and DeFi TVL depend on public providers and may be unavailable or rate-limited.

Important: Signals are educational rule-based indicators, not validated predictions or financial advice. No exchange connection, wallet access, or automatic trading is included. No API keys are embedded.


Fake-order / spoofing heuristic (added):
- For supported Binance crypto pairs, the app opens public depth20 and aggregate-trade WebSocket streams.
- It flags unusually large visible bid/ask walls that shrink by 70% or more within successive snapshots when nearby executed trade notional is comparatively small.
- The panel shows a rolling suspicious-event count and LOW/MEDIUM/HIGH heuristic risk.
- This is not proof of spoofing: public order-book data cannot establish trader intent, detect all hidden orders, or reliably classify wash trading. Network disconnects and exchange feed limitations can affect results.
- Gold and Silver do not use this Binance crypto order-book detector.

Risk planner upgrade:
- Adds a paper-trade reference entry from the latest 5-minute candle.
- Calculates ATR(14) from OHLC candles, uses a 1.5 x ATR stop distance and a 2R target.
- Shows WAIT instead of generating a directional plan when the 5-minute signal is mixed.
- This is a volatility-based illustration only; it does not size positions or place orders, and excludes fees, slippage and gaps.

Upgrade build note:
- JavaScript syntax checked with Node.js.
- Backtest is a simple next-candle test, not a robust walk-forward study; it excludes fees, slippage, spread, funding payments and latency. Past results do not predict future results.
- Signal history is stored only on the device and uses a later refresh price as an approximate outcome, not an executed trade.
- Open interest is a current snapshot only; a time-series OI change chart is not included.
- A compiled APK is not included; use the included GitHub Actions workflow or Android Studio to build it.


AI RADAR v3.0 updates:
- App branding and Android application ID updated to AI Radar (com.airadar.app).
- Exchange selector: Binance or MEXC for selected-asset spot price, 5-minute and 4-hour candles, and 1-hour historical backtest (where the pair is listed).
- Exchange preference is saved on this device.
- Fake-order/spoofing detector intentionally remains Binance-only; the UI clearly reports it unavailable when MEXC is selected.
- Binance USD-M funding/open-interest metrics remain Binance-only.

MEXC market data uses its public spot REST API. Some symbols may not be listed on both exchanges. Gold and Silver remain spot-quote only and do not receive fabricated technical signals. The app still does not place orders or connect wallets.
