## Predicting Bond Yield Volatility for Risk Mitigation

### Overview

Bond yield is the return on the capital invested by an investor. A bond can be purchased for more than its face value, at a premium, or less than its face value, at a discount. The current yield is the bond's coupon rate divided by its market price.Price and yield are inversely related and as the price of a bond goes up, its yield goes down.

Financial Risk: Possible loss on an investment
Data and Project - Datacamp

The data ranges from 1961 to 2019. On plotting the bond yields, we get the following:

<img src="https://github.com/TejaswiniPemmaraju/BondYieldVolatility/assets/129342521/78271872-59b2-4579-b5cd-30f26561b0da" width="350" height="350">

In the above image, the long yields (e.g. SVENY30) tend to be more stable in the long term, while the short yields (e.g. SVENY01) vary a lot. These movements are related to the monetary policy of the FED and economic cycles.

### Process

##### Step 1: Calculate the change in yields. (Differentiation)

We use differetiation to make the time series independent of time. Differencing can help stabilise the mean of a time series by removing changes in the level of a time series, and therefore eliminating (or reducing) trend and seasonality. Seasonality is a characteristic of a time series in which the data experiences regular and predictable changes that recur every calendar year. Any predictable fluctuation or pattern that recurs or repeats over a one-year period is said to be seasonal.

##### Step 2: Examining the time series of yield changes

<img src="https://github.com/TejaswiniPemmaraju/BondYieldVolatility/assets/129342521/4637c8c7-ad30-4aea-bd82-b3a383203223" width="350" height="350">

##### Step 3: Testing for autocorrelation

Autocorrelation measures how a datapoint's past determines the future of a time series.

If the autocorrelation is close to 1, the next day's value will be very close to today's value.
If the autocorrelation is close to 0, the next day's value will be unaffected by today's value.

<img src="https://github.com/TejaswiniPemmaraju/BondYieldVolatility/assets/129342521/8a8ffefe-fdf5-4cc4-b7ca-7e14f93eb738" width="450" height="450">

Looking at the graph it could mean:
1. Normal ACF Plot: It suggests that there might not be a simple linear autocorrelation pattern in your data. In other words, the current value at a given time point is not significantly related to its past values at various lags.
2. Absolute Values ACF Plot: When the ACF for the absolute values of data is calculated, we examine the correlation between the magnitudes of the time series values at different lags. Strong correlation in this plot might imply conditional heteroskedasticity present in the data. Conditional heteroskedasticity means that the variability (volatility) of the data changes over time, and it might be influenced by previous observations. This is a common characteristic in financial time series data, and it suggests that the magnitude of price changes is autocorrelated.

Strong correlation in the absolute values ACF plot could indicate that there are periods of high volatility followed by periods of low volatility in your data. It suggests that the magnitude of future price changes might be influenced by past price changes. Models like GARCH (Generalized AutoRegressive Conditional Heteroskedasticity) are often used to capture such conditional heteroskedasticity patterns in financial time series data.

##### Step 4: Building GARCH

A Generalized AutoRegressive Conditional Heteroskedasticity (GARCH) model is the most well known econometric tool to handle changing volatility in financial time series data. It assumes a hidden volatility variable that has a long-run average it tries to return to while the short-run behavior is affected by the past returns.

The most popular form of the GARCH model assumes that the volatility follows this process:
σ2t = ω + α ⋅ ε2t-1 + β ⋅ σ2t-1
where σ is the current volatility, σt-1 the last day's volatility and εt-1 is the last day's return. The estimated parameters are ω, α, and β.

On plotting the yield changes with the estimated volatilities and residuals for 1 year maturity

<img src="https://github.com/TejaswiniPemmaraju/GARCH_BondYieldVolatility/assets/129342521/a2a82a74-ae77-4064-8d2b-027cd739cff6" width="250" height="250">

On plotting the yield changes with the estimated volatilities and residuals for 20 year maturity

<img src="https://github.com/TejaswiniPemmaraju/GARCH_BondYieldVolatility/assets/129342521/e8d5763c-4a77-4dcf-9817-88fc6d070f32" width="250" height="250">

On comparing the model:
1. 1-year GARCH model shows a similar but more erratic behavior compared to the 20-year GARCH model.
2. 1-year model have greater volatility, but the volatility of its volatility is larger than the 20-year model.
3. GARCH model helps make things more understandable and predictable, but it doesn't make them completely normal. Better than uncoditional distribution but worse than normal distribution

Lets now create a graphical comparison between the original data (x_1), the data after applying GARCH modeling (res_1), and a normal distribution to visualize the changes in the data distribution due to the GARCH modeling to asses how well Garch model fits.

<img src="https://github.com/TejaswiniPemmaraju/GARCH_BondYieldVolatility/assets/129342521/4f0b7383-1cd2-4c17-b224-500d2aa325c4" width="350" height="350">

To focus on the tails where the differences are most profound lets draw Q-Q plots:

<img src="https://github.com/TejaswiniPemmaraju/GARCH_BondYieldVolatility/assets/129342521/a95bf388-84be-4269-96bd-6f88ce8774e0" width="350" height="350">

### Key Findings:

1. GARCH modeling illuminated the temporal evolution of bond yield volatility, providing a comprehensive understanding of changing dynamics.
2. By significantly improving the normality of residuals, GARCH modeling paved the way for more accurate predictions.
3. Notably, it pinpointed distinctions between the 1-year and 20-year yield changes, underlining varying levels of volatility.
4. The 1-year GARCH model exhibited higher volatility and greater volatility of volatility compared to the 20-year model, signifying nuanced risk profiles.
5. GARCH modeling added a layer of predictability to yield behavior while maintaining a slight deviation from a perfectly normal distribution, emphasizing the potential for model enhancement.





