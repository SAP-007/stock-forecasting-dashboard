# Financial Insights Web App: Stock Analysis & Forecasting Dashboard

A Streamlit web app for stock analysis and price forecasting, built on the Polygon.io market-data API. It compares five forecasting models side by side and includes a GPT-powered chatbot that explains financial terms.

Built as the MS Business Analytics capstone (BAN 693) at California State University, East Bay, 2025.

![Forecast tab: GRU forecast and five models ranked by MAPE and RMSE](forecast-model-comparison.png)

![Insights tab: price snapshot, volume trend and 50/200-day crossover signals](insights-tab.png)

![Company overview: profile, key stats, 30-day price and dividends](company-overview.png)

![Sector summary: market-cap rank and comparison](sector-summary.png)

## What it does

**Market insights**
- Daily OHLC snapshot with day-over-day change
- Volume trend with 7-day and 30-day moving averages
- 50-day vs 200-day moving-average crossovers, marked as buy and sell signals

**Company overview**
- Profile, exchange, market cap, 52-week range, year-to-date return and dividend yield
- Five related companies from the same sector, with their daily change
- Recent dividends and stock splits

**Sector summary**
- Market-cap rank and percentile within each sector, with a comparison chart

**Forecasting**
- Five models: ARIMA, SARIMA, XGBoost, LSTM and GRU
- Chronological 80/20 train/test split, so no future data leaks into training
- XGBoost on lagged features; LSTM and GRU in TensorFlow/Keras with early stopping
- Recursive multi-day forecasts for a 1–30 day horizon
- A validation leaderboard ranking each model by MAPE and RMSE

**Finance chatbot**
- Answers questions such as "What is EBITDA?" using GPT-3.5 through the OpenAI API

**Market news**
- Top headlines from Polygon, with links to the full articles

## Engineering notes

- API calls retry with backoff on rate limits (HTTP 429) and handle missing tickers gracefully
- Market data is cached for 24 hours and models are cached per session, which keeps the app fast and within API limits
- API keys are read from environment variables and never committed

## Tech stack

Python · Streamlit · Pandas · NumPy · statsmodels (ARIMA, SARIMA) · XGBoost · TensorFlow/Keras (LSTM, GRU) · scikit-learn · Plotly · OpenAI API · Polygon.io API

## Run it locally

```bash
pip install -r requirements.txt
```

Create a file named `keys.env` in the project folder:

```
POLYGON_API_KEY=your_polygon_key
OPENAI_API_KEY=your_openai_key
```

Then start the app:

```bash
streamlit run stocks_dashboard.py
```
