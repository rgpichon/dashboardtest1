import yfinance as yf
import pandas as pd
import matplotlib.pyplot as plt
import streamlit as st

# --- Portfolio Setup ---
assets = {
    'AAPL': 0.10,
    'NVDA': 0.10,
    'BRK-B': 0.10,
    'WMT': 0.10,
    'RACE': 0.10,
    'IEF': 0.05,
    'AM.PA': 0.07,      # Dassault Aviation SA
    'RHM.DE': 0.07,     # Rheinmetall AG
    'GLD': 0.07,
    'GDX': 0.07,
    'GS': 0.10,
    'VWESX': 0.07
}

# --- Streamlit UI ---
st.set_page_config(layout="wide")
st.title("📈 Portfolio Performance Dashboard (2025 YTD)")

start_date = st.date_input("Select Start Date", pd.to_datetime("2025-01-01"))

if st.button("Run Analysis"):
    symbols = list(assets.keys())
    st.info("Downloading price data...")

    prices = yf.download(symbols, start=start_date).Close.dropna()

    # Normalize and calculate portfolio
    normalized = prices / prices.iloc[0] * 100
    weights = pd.Series(assets)
    weighted = normalized.multiply(weights, axis=1)
    portfolio = weighted.sum(axis=1)

    # Plot
    fig, ax = plt.subplots(figsize=(14, 6))
    ax.plot(portfolio, label='Portfolio', color='black', linewidth=2)

    for symbol in normalized.columns:
        ax.plot(normalized[symbol], label=symbol, linestyle='--', alpha=0.7)

    ax.set_title("Portfolio & Asset Performance")
    ax.set_ylabel("Normalized Value (Start = 100)")
    ax.legend()
    ax.grid(True)

    st.pyplot(fig)
