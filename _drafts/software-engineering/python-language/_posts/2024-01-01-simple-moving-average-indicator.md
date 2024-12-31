---
layout: post
title: "Simple Moving Average (SMA) Indicator"
author: andre
categories: [ software-engineering, python-language ]
tags: [numpy]
image: /assets/images/software-engineering/python-language/array-creation-in-numpy.png
description: "This post provides a comprehensive guide with examples on using NumPy for array creation, showcasing efficient methods to initialize arrays with specific values, shapes, and patterns."
comments: true
---

- Table of Contents
{:toc .large-only}

> Disclaimer: This blog post is for educational purposes only and does not constitute financial advice. Trading involves risk, and it’s essential to perform thorough research and consult with a financial advisor before making trading decisions.

Exploring the Simple Moving Average indicator using the TA-Lib python library. This blog forms part of an ongoing series, Technical Analysis in Python, where I look into key trading indicators and their practical applications.

The Simple Moving Average (SMA) is a widely used metric that calculates the average price of an asset, typically its closing price, over a specified number of days.

In this blog, I will demonstrate how to compute and utilise SMA with Python’s TA-Lib library, providing valuable insights for algorithmic trading strategies.

## Definition & Key Points

The **Simple Moving Average (SMA)** calculates the average of a selected range of prices, typically closing prices, by the number of periods in that range.

It is called “moving” because it continuously updates as new data becomes available and old data drops off.

Here are the key points for the Simple Moving Average (SMA) trade indicator:

- **Average Price**: SMA calculates the average price of an asset over a specified number of periods.
- **Trend Smoothing**: It smooths out price fluctuations to reveal underlying trends more clearly.
- **Lagging Indicator**: SMA is a lagging indicator, meaning it reflects past trends rather than predicting future ones.
- **Key Levels**: Helps identify support and resistance levels, trend direction, and potential reversal points.
- **Trend Signals**: Price above SMA may indicate an uptrend, while price below may suggest a downtrend.
- **Common Periods**: Commonly used periods include 10, 21, 50, and 200 days.

## SMA Calculation
Calculating the Simple Moving Average is straightforward. It involves summing up the closing prices of a specified number of periods and then dividing by the number of periods.



## Python Example Using TA-Lib
Now, let’s implement the Simple Moving Average using Python’s TA-Lib library. TA-Lib is a popular technical analysis library that provides a wide range of indicators, including SMA. If you haven't installed TA-Lib yet, you can do so using pip. Note that TA-Lib requires the underlying C library to be installed on your system.

### Basic Example: Time period
This example calculates the Simple Moving Averages (SMA) of a predefined array of prices for three different time periods: 5, 7, and 9 days.

```python
import talib
import numpy as np

# Example prices
prices = np.array([10, 11, 12, 13, 14, 15, 16, 17, 18, 19], dtype=np.float64)

# Calculate SMA with different timeperiods
sma_5 = talib.SMA(prices, timeperiod=5)
sma_7 = talib.SMA(prices, timeperiod=7)
sma_9 = talib.SMA(prices, timeperiod=9)

# Print the calculated SMA
print("5-period SMA:", sma_5)
print("7-period SMA:", sma_7)
print("9-period SMA:", sma_9)
```
After calculating the SMAs, it prints the resulting values, which display nan for the initial periods where there isn't enough data to perform the average calculation.

