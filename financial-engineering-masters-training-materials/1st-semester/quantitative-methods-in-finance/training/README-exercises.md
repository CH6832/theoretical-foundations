### 2.1 Probability Theory

#### 2.1.1 Random Variables and Distributions

1. **Discrete Random Variable**: Consider a discrete random variable \( X \) with possible values \{1, 2, 3\} and probabilities \{0.2, 0.5, 0.3\}. Calculate the expected value and variance of \( X \).

2. **Continuous Random Variable**: For a continuous random variable \( X \) with PDF \( f_X(x) = 2x \) for \( 0 \leq x \leq 1 \), find \( P(0.3 \leq X \leq 0.7) \) and the mean of \( X \).

3. **Normal Distribution**: A stock's returns are normally distributed with a mean of 5% and a standard deviation of 2%. What is the probability that the return will be between 3% and 7%?

4. **Log-Normal Distribution**: If a stock price follows a log-normal distribution with parameters \( \mu = 0.05 \) and \( \sigma = 0.2 \), what is the probability that the stock price will exceed 1.2 times its current value?

5. **Expectation Calculation**: For a discrete random variable \( X \) with the probability distribution \( P(X = 1) = 0.4 \), \( P(X = 2) = 0.4 \), and \( P(X = 3) = 0.2 \), compute \( E[X^2] \) and \( E[X^3] \).

6. **Variance Calculation**: Given a continuous random variable \( X \) with PDF \( f_X(x) = e^{-x} \) for \( x \geq 0 \), calculate the variance of \( X \).

7. **Skewness**: For a random variable \( X \) with the following PDF \( f_X(x) = \frac{1}{2} \) for \( 0 \leq x \leq 2 \), compute the skewness of \( X \).

8. **Kurtosis**: Calculate the kurtosis for a random variable \( X \) uniformly distributed between \{-1, 1\}.

9. **Simulating Data**: Using Python, simulate 1,000 samples from a normal distribution with a mean of 0 and a variance of 1, and compute the sample mean, variance, skewness, and kurtosis.

10. **Log-Normal Simulation**: Simulate 1,000 samples from a log-normal distribution with \( \mu = 0 \) and \( \sigma = 0.5 \) and plot the histogram of the simulated data.

#### 2.1.2 Expectation and Moments

11. **Expectation Calculation**: Calculate the expectation of a random variable \( X \) where \( X \) is uniformly distributed between 3 and 7.

12. **Variance Calculation**: If \( X \) is exponentially distributed with parameter \( \lambda = 1 \), find the variance of \( X \).

13. **Skewness and Kurtosis**: Compute the skewness and kurtosis of a normal distribution with mean 10 and variance 4.

14. **Empirical Moments**: Given a sample dataset, compute the empirical mean, variance, skewness, and kurtosis.

15. **Comparing Distributions**: Compare the skewness and kurtosis of a normal distribution with that of a t-distribution with 5 degrees of freedom.

### 2.2 Statistical Inference

#### 2.2.1 Hypothesis Testing

16. **t-Test Application**: Perform a t-test on two sample datasets to determine if their means are significantly different. Interpret the p-value.

17. **Chi-Square Test**: Use a chi-square test to determine if two categorical variables are independent based on a given contingency table.

18. **Confidence Intervals**: Calculate a 95% confidence interval for the mean of a normally distributed sample with a known standard deviation.

19. **p-Value Calculation**: Compute the p-value for a hypothesis test where the test statistic is 2.5 and the degrees of freedom are 10.

20. **Power of a Test**: Determine the power of a t-test given the sample size, effect size, and significance level.

21. **Paired t-Test**: Conduct a paired t-test to compare the means of two related samples and interpret the results.

22. **One-Way ANOVA**: Perform a one-way ANOVA test to determine if there are significant differences among the means of three different groups.

23. **Multiple Comparisons**: Apply a Bonferroni correction to adjust for multiple comparisons in hypothesis testing.

24. **Z-Test**: Given a sample mean, population mean, and standard deviation, conduct a z-test to determine if the sample mean significantly differs from the population mean.

25. **Hypothesis Test for Proportions**: Perform a hypothesis test for proportions to determine if the observed proportion of successes differs from a hypothesized proportion.

### 2.3 Time Series Analysis

#### 2.3.1 ARIMA Models

26. **ARIMA Identification**: Given a time series dataset, identify the appropriate ARIMA(p, d, q) model using autocorrelation and partial autocorrelation plots.

27. **ARIMA Fitting**: Fit an ARIMA model to a time series dataset and interpret the coefficients of the model.

28. **Model Diagnostics**: Assess the residuals of an ARIMA model for autocorrelation and heteroskedasticity.

29. **Forecasting**: Use an ARIMA model to forecast future values of a time series and evaluate the forecast accuracy.

30. **Differencing**: Apply differencing to a time series dataset to make it stationary and assess the impact on the data.

31. **Model Selection**: Compare the performance of different ARIMA models using AIC and BIC criteria.

32. **Seasonal ARIMA**: Fit a seasonal ARIMA model to a time series with seasonal patterns and interpret the seasonal components.

33. **Outlier Detection**: Identify and handle outliers in a time series dataset before fitting an ARIMA model.

34. **Model Validation**: Validate the fitted ARIMA model using out-of-sample data and compute forecast accuracy metrics such as MSE or MAE.

35. **ARIMA vs. Exponential Smoothing**: Compare the performance of ARIMA and exponential smoothing models on a given time series dataset.

#### 2.3.2 GARCH Models

36. **GARCH Identification**: Identify the appropriate GARCH model for a time series with changing volatility using autocorrelation of squared returns.

37. **GARCH Fitting**: Fit a GARCH(1,1) model to a financial time series and interpret the estimated parameters.

38. **Volatility Forecasting**: Use a fitted GARCH model to forecast future volatility and assess the forecast accuracy.

39. **Model Comparison**: Compare the performance of different GARCH models (e.g., GARCH, EGARCH, TGARCH) based on in-sample and out-of-sample volatility predictions.

40. **Model Diagnostics**: Perform diagnostic checks on the residuals of a GARCH model to ensure it adequately captures volatility clustering.

41. **Backtesting**: Backtest a GARCH model’s volatility forecasts using historical data and evaluate its predictive performance.

42. **Risk Management**: Apply a GARCH model to estimate Value at Risk (VaR) for a financial portfolio.

43. **Volatility Spillover**: Investigate volatility spillover effects between different financial assets using multivariate GARCH models.

44. **Robustness Check**: Assess the robustness of a GARCH model by fitting it to different subsets of data or using different estimation methods.

45. **Parameter Sensitivity**: Analyze how sensitive the GARCH model’s volatility forecasts are to changes in model parameters.

### 2.4 Practical Exercises

46. **Data Analysis**: Collect a real-world financial dataset (e.g., stock prices) and perform exploratory data analysis using summary statistics and visualizations.

47. **Financial Modeling**: Build a financial model using historical data to estimate future stock prices or returns and evaluate the model's performance.

48. **Risk Management**: Develop a risk management strategy for a financial portfolio using quantitative methods such as Value at Risk (VaR) and Conditional Value at Risk (CVaR).

49. **Algorithmic Trading**: Implement a basic trading algorithm based on quantitative strategies and backtest its performance using historical data.

50. **Report Writing**: Prepare a comprehensive report on a quantitative finance project, including data analysis, modeling, results, and interpretations.
