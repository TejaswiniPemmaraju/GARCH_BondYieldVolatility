## Predicting Bond Yield Volatility for Risk Mitigation

### Overview

Bond yield is the return on the capital invested by an investor. A bond can be purchased for more than its face value, at a premium, or less than its face value, at a discount. The current yield is the bond's coupon rate divided by its market price.Price and yield are inversely related and as the price of a bond goes up, its yield goes down.

Financial Risk: Possible loss on an investment
Data and Project - Datacamp

The data ranges from 1961 to 2019. On plotting the bond yields, we get the following:
<img src="https://github.com/TejaswiniPemmaraju/BondYieldVolatility/assets/129342521/78271872-59b2-4579-b5cd-30f26561b0da" width="500" height="500">

In the above image, the long yields (e.g. SVENY30) tend to be more stable in the long term, while the short yields (e.g. SVENY01) vary a lot. These movements are related to the monetary policy of the FED and economic cycles.

### Process
Step 1: Calculate the change in yields. (Differentiation)

We use differetiation to make the time series independent of time. Differencing can help stabilise the mean of a time series by removing changes in the level of a time series, and therefore eliminating (or reducing) trend and seasonality. Seasonality is a characteristic of a time series in which the data experiences regular and predictable changes that recur every calendar year. Any predictable fluctuation or pattern that recurs or repeats over a one-year period is said to be seasonal.

Step 2: Examining the time series of yield changes

<img src="https://github.com/TejaswiniPemmaraju/BondYieldVolatility/assets/129342521/4637c8c7-ad30-4aea-bd82-b3a383203223" width="500" height="500">

Step 3: Testing for autocorrelation

Autocorrelation measures how a datapoint's past determines the future of a time series.

If the autocorrelation is close to 1, the next day's value will be very close to today's value.
If the autocorrelation is close to 0, the next day's value will be unaffected by today's value.

<img src="https://github.com/TejaswiniPemmaraju/BondYieldVolatility/assets/129342521/8a8ffefe-fdf5-4cc4-b7ca-7e14f93eb738" width="500" height="500">

Looking at the graph it could mean:
1. Normal ACF Plot: It suggests that there might not be a simple linear autocorrelation pattern in your data. In other words, the current value at a given time point is not significantly related to its past values at various lags.
2. Absolute Values ACF Plot: When the ACF for the absolute values of data is calculated, we examine the correlation between the magnitudes of the time series values at different lags. Strong correlation in this plot might imply conditional heteroskedasticity present in the data. Conditional heteroskedasticity means that the variability (volatility) of the data changes over time, and it might be influenced by previous observations. This is a common characteristic in financial time series data, and it suggests that the magnitude of price changes is autocorrelated.

In practical terms, strong correlation in the absolute values ACF plot could indicate that there are periods of high volatility followed by periods of low volatility in your data. It suggests that the magnitude of future price changes might be influenced by past price changes. Models like GARCH (Generalized AutoRegressive Conditional Heteroskedasticity) are often used to capture such conditional heteroskedasticity patterns in financial time series data.

Step 4: Building GARCH
