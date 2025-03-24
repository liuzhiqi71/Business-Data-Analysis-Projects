# Bitcoin and S&P 500 Analysis

This analysis retrieves historical data for Bitcoin (BTC-USD) and the S&P 500 index (SPY) from Yahoo Finance, calculates their daily returns, and performs a linear regression to explore the relationship between their returns.

## Results

- **Correlation coefficient (r):** Measures the strength and direction of the linear relationship between Bitcoin and S&P 500 returns.
- **Coefficient of determination (R²):** Indicates the proportion of the variance in the S&P 500 returns that is predictable from the Bitcoin returns.
- **Linear Regression Model:** Provides a statistical method to model the relationship between Bitcoin returns (independent variable) and S&P 500 returns (dependent variable).

## R Script

```r
library(quantmod)

# Get historical data for Bitcoin and S&P 500 index
btc_data <- getSymbols("BTC-USD", src = "yahoo", from = "2017-01-01", to = "2025-01-01", auto.assign = FALSE)
spy_data <- getSymbols("SPY", src = "yahoo", from = "2017-01-01", to = "2025-01-01", auto.assign = FALSE)

# Extract closing prices
btc_close <- Cl(btc_data)
spy_close <- Cl(spy_data)

# Calculate returns
btc_returns <- dailyReturn(btc_close)
spy_returns <- dailyReturn(spy_close)

# Merge returns data
returns_data <- merge.xts(btc_returns, spy_returns, all = FALSE)
colnames(returns_data) <- c("BTC_Returns", "SPY_Returns")

# Calculate correlation coefficient
correlation <- cor(returns_data$BTC_Returns, returns_data$SPY_Returns)
print(paste("Correlation coefficient (r):", correlation))

# Calculate coefficient of determination
coefficient_of_determination <- correlation^2
print(paste("Coefficient of determination (R^2):", coefficient_of_determination))

# Linear regression using least squares method
lm_model <- lm(SPY_Returns ~ BTC_Returns, data = as.data.frame(returns_data))
print(summary(lm_model))

# Save high-resolution plot
png(filename = "btc_spy_regression.png", width = 1920, height = 1080, res = 300)
par(mar = c(5, 5, 4, 2) + 0.1, cex = 0.8)  # Adjust margins and font size
plot(as.numeric(returns_data$BTC_Returns), as.numeric(returns_data$SPY_Returns), 
     xlab = "Bitcoin (BTC-USD) Returns", 
     ylab = "S&P 500 (SPY) Returns",
     main = "Linear Relationship between Bitcoin Returns and S&P 500 Returns",
     col = "#31a354", pch = 16, xlim = range(returns_data$BTC_Returns), ylim = range(returns_data$SPY_Returns))  # Plot BTC points in green

points(as.numeric(returns_data$BTC_Returns), as.numeric(returns_data$SPY_Returns), 
       col = "red", pch = 1)  # Plot SP500 points in red

abline(lm_model, col = "black")  # Regression line in black

# Add legend
legend("topright", legend = c("BTC Returns", "SPY Returns", "Regression Line"), 
       col = c("#31a354", "red", "black"), pch = c(16, 1, NA), lty = c(NA, NA, 1))
dev.off()


