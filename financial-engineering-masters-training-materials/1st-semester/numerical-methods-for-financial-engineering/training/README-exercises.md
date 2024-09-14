### Probability Theory

1. **Discrete Random Variables:**
   - Compute the expected value and variance for a discrete random variable representing the number of heads in 10 coin flips.

2. **Continuous Random Variables:**
   - For a continuous random variable \(X\) with \(f_X(x) = \frac{1}{\sqrt{2\pi \sigma^2}} \exp \left( -\frac{(x - \mu)^2}{2\sigma^2} \right)\), calculate the probability \(P(\mu - \sigma \leq X \leq \mu + \sigma)\).

3. **Normal Distribution:**
   - Simulate a dataset of 1,000 daily returns following a normal distribution with mean 0 and standard deviation 0.02. Compute the sample mean and standard deviation.

4. **Log-Normal Distribution:**
   - Generate a log-normal distribution sample with \(\mu = 0\) and \(\sigma = 0.1\). Compare its histogram with a normal distribution histogram of the log-transformed data.

5. **Expectation and Variance:**
   - Given a discrete random variable with values \(\{1, 2, 3\}\) and probabilities \(\{0.2, 0.5, 0.3\}\), calculate the expectation and variance.

6. **Skewness and Kurtosis:**
   - For a dataset of financial returns, compute the skewness and kurtosis. Interpret the results in terms of risk and outliers.

7. **Monte Carlo Simulation of Normal Returns:**
   - Simulate 10,000 returns from a normal distribution and estimate the 95th percentile of the returns.

8. **Expectation with Discrete Random Variables:**
   - Compute the expected value of a random variable representing the outcome of rolling two six-sided dice.

9. **Variance Calculation:**
   - Given a continuous random variable with a known PDF, compute its variance using numerical integration.

10. **Moment Generating Functions:**
    - Derive the moment generating function for a normal distribution and use it to find the mean and variance.

### Statistical Inference

11. **t-Test for Two Independent Samples:**
    - Perform a t-test to compare the means of daily returns from two different stocks.

12. **Chi-Square Test for Independence:**
    - Conduct a chi-square test to determine if there is a significant relationship between two categorical financial variables.

13. **Confidence Interval for Mean:**
    - Calculate a 95% confidence interval for the mean of a sample of stock returns using the t-distribution.

14. **Maximum Likelihood Estimation (MLE):**
    - Use MLE to estimate the parameters of a log-normal distribution based on a given sample of financial data.

15. **Hypothesis Testing for Proportions:**
    - Test whether the proportion of days with positive returns for a stock differs significantly from 50%.

16. **Comparing Means with Paired t-Test:**
    - Perform a paired t-test to compare the returns of a stock before and after a major corporate event.

17. **Wilcoxon Signed-Rank Test:**
    - Apply the Wilcoxon signed-rank test to assess whether the median of a sample of daily returns differs from zero.

18. **Bayesian Hypothesis Testing:**
    - Use Bayesian methods to test whether a given financial model provides a better fit to the data compared to a competing model.

19. **Confidence Interval for Proportion:**
    - Compute a confidence interval for the proportion of days a stock's return exceeds a certain threshold.

20. **Goodness-of-Fit Test:**
    - Perform a goodness-of-fit test to check if the returns of a stock follow a normal distribution.

### Linear Regression

21. **Ordinary Least Squares (OLS):**
    - Fit an OLS model to predict stock returns based on macroeconomic indicators. Evaluate the model’s performance using \(R^2\) and residual plots.

22. **Multicollinearity Detection:**
    - Assess multicollinearity in a regression model by calculating the Variance Inflation Factor (VIF) for each independent variable.

23. **Residual Analysis:**
    - Analyze the residuals from an OLS regression of stock returns on market returns. Check for patterns or non-constant variance.

24. **Regularization Techniques:**
    - Implement Lasso and Ridge regression to improve the performance of a financial model with many predictors.

25. **Polynomial Regression:**
    - Apply polynomial regression to model non-linear relationships between financial variables, such as stock price and trading volume.

26. **Model Diagnostics:**
    - Conduct diagnostic tests on a regression model to check for heteroskedasticity, autocorrelation, and normality of residuals.

27. **Interaction Effects:**
    - Include interaction terms in a regression model to examine how the relationship between stock returns and economic indicators changes with different levels of another variable.

28. **Cross-Validation:**
    - Use k-fold cross-validation to evaluate the predictive performance of a linear regression model on financial data.

29. **Robust Regression:**
    - Fit a robust regression model to handle outliers in stock return data.

30. **Time Series Regression:**
    - Apply regression techniques to model the relationship between stock returns and macroeconomic factors over time.

### Time Series Analysis

31. **ARIMA Model Fitting:**
    - Fit an ARIMA model to historical stock prices and use it to forecast future prices. Evaluate the model using in-sample and out-of-sample tests.

32. **Seasonality and Trends:**
    - Decompose a time series of monthly stock returns into trend, seasonal, and residual components using STL (Seasonal-Trend decomposition).

33. **GARCH Model Application:**
    - Apply a GARCH model to estimate the volatility of stock returns and use it to forecast future volatility.

34. **Exponential Smoothing:**
    - Implement exponential smoothing methods to forecast stock prices and compare with ARIMA forecasts.

35. **Cointegration Testing:**
    - Test for cointegration between stock prices of two companies to determine if they move together over time.

36. **Volatility Clustering:**
    - Analyze volatility clustering in financial time series and model it using a GARCH(1,1) process.

37. **Granger Causality Test:**
    - Perform a Granger causality test to investigate whether one financial time series can predict another.

38. **Rolling Window Analysis:**
    - Conduct rolling window regression to analyze how the relationship between stock returns and economic indicators changes over time.

39. **Kalman Filtering:**
    - Use Kalman filtering to estimate the hidden state of a financial time series, such as underlying volatility.

40. **Long Memory Processes:**
    - Model a time series with long memory properties using Fractional ARIMA (FARIMA) models.

### Portfolio Optimization

41. **Mean-Variance Optimization:**
    - Construct an efficient frontier by optimizing the weights of a multi-asset portfolio to maximize return for a given level of risk.

42. **Capital Asset Pricing Model (CAPM):**
    - Apply CAPM to estimate the expected return of a stock based on its beta and the market risk premium.

43. **Sharpe Ratio Calculation:**
    - Compute the Sharpe ratio for different portfolios to evaluate their risk-adjusted performance.

44. **Portfolio Rebalancing:**
    - Simulate periodic portfolio rebalancing to maintain target asset allocation and assess its impact on performance.

45. **Black-Litterman Model:**
    - Incorporate investor views into the portfolio optimization process using the Black-Litterman model.

46. **Value at Risk (VaR) Calculation:**
    - Estimate the Value at Risk for a portfolio using historical simulation and parametric methods.

47. **Stress Testing:**
    - Perform stress testing on a portfolio to assess its performance under adverse market conditions.

48. **Tracking Error Analysis:**
    - Calculate and analyze the tracking error of a portfolio relative to a benchmark index.

49. **Monte Carlo Simulation for Portfolio Risk:**
    - Use Monte Carlo simulation to estimate the distribution of portfolio returns and assess the probability of extreme losses.

50. **Factor Models:**
    - Implement factor models, such as the Fama-French three-factor model, to analyze the sources of portfolio returns.
