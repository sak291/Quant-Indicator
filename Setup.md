# 📈 Quant AI Indicator — Official TradingView Setup Guide

![TradingView AI Banner](https://img.shields.io/badge/TradingView-Pine_Script_v5-2962FF?style=for-the-badge&logo=tradingview&logoColor=white)
![Version](https://img.shields.io/badge/Version-1.0.4_Open_Source-089981?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-orange?style=for-the-badge)

Welcome to the official installation and configuration guide for the **Quant AI Indicator** for TradingView. Follow the instructions below to deploy the open-source script directly onto your chart.
//@version=5
indicator("Quant AI Indicator", overlay=true, shorttitle="Quant AI")

// --- Inputs & Settings ---
length      = input.int(20, title="Analysis Window", minval=1)
mult        = input.float(2.0, title="Volatility Multiplier", step=0.1)
src         = input.source(close, title="Price Source")

// --- Core Calculations ---
basis       = ta.sma(src, length)
dev         = mult * ta.stdev(src, length)
upper_path  = basis + dev
lower_path  = basis - dev

// --- Plotting Scenarios ---
plot(basis, title="Scenario B (Baseline)", color=color.rgb(41, 98, 255), linewidth=2)
plot(upper_path, title="Scenario A (Bullish Boundary)", color=color.rgb(8, 153, 129), linewidth=2, style=plot.style_dashed)
plot(lower_path, title="Scenario C (Bearish Boundary)", color=color.rgb(242, 54, 69), linewidth=2, style=plot.style_dashed)

// --- Visual Overlay ---
fill(plot(upper_path), plot(lower_path), color=color.new(color.blue, 95), title="Quant Context Zone")
