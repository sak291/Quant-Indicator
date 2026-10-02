# 📈 Quant AI Indicator Setup Guide (TradingView)

Welcome to the official installation guide for the **Quant AI Indicator** on TradingView. Follow these simple steps to add the Pine Script to your chart.
//@version=5
indicator("Quant AI Indicator", overlay=true)

// --- Parameters & Inputs ---
length = input.int(14, title="Analysis Period")
mult = input.float(2.0, title="Volatility Multiplier")

// --- Core Calculations ---
basis = ta.sma(close, length)
dev = mult * ta.stdev(close, length)
upper_scen = basis + dev
lower_scen = basis - dev

// --- Plot Scenarios ---
plot(basis, "Baseline (Range)", color=color.blue, linewidth=2, style=plot.style_line)
plot(upper_scen, "Scenario A (Bullish)", color=color.green, linewidth=2, style=plot.style_dashed)
plot(lower_scen, "Scenario C (Bearish)", color=color.red, linewidth=2, style=plot.style_dashed)

// --- Visual Alerts & Background Context ---
fill(plot(upper_scen), plot(lower_scen), color=color.new(color.blue, 95), title="Context Range")
