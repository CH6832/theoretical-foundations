### 2.1 Probability Theory

#### 2.1.1 Random Variables and Distributions

1. **Discrete Random Variable**: Given a discrete random variable \( Y \) with possible values \{2, 4, 6\} and probabilities \{0.1, 0.4, 0.5\}, calculate the expected value and variance of \( Y \).

2. **Continuous Random Variable**: For a continuous random variable \( Y \) with PDF \( f_Y(y) = 3y^2 \) for \( 0 \leq y \leq 1 \), find \( P(0.2 \leq Y \leq 0.8) \) and the mean of \( Y \).

3. **Normal Distribution**: A financial asset's returns are normally distributed with a mean of 7% and a standard deviation of 1.5%. Calculate the probability that the return will be less than 5%.

4. **Log-Normal Distribution**: A stock price follows a log-normal distribution with parameters \( \mu = 0.04 \) and \( \sigma = 0.3 \). What is the probability that the stock price will be at least 1.5 times its current value?

5. **Expectation Calculation**: For a discrete random variable \( Y \) with the probability distribution \( P(Y = 1) = 0.3 \), \( P(Y = 4) = 0.5 \), and \( P(Y = 5) = 0.2 \), compute \( E[Y^2] \) and \( E[Y^3] \).

6. **Variance Calculation**: Given a continuous random variable \( Y \) with PDF \( f_Y(y) = 4y(1-y) \) for \( 0 \leq y \leq 1 \), calculate the variance of \( Y \).

7. **Skewness**: For a random variable \( Y \) with PDF \( f_Y(y) = \frac{3}{8}(y^2) \) for \( 0 \leq y \leq 2 \), compute the skewness of \( Y \).

8. **Kurtosis**: Calculate the kurtosis for a random variable \( Y \) uniformly distributed between \{0, 2\}.

9. **Simulating Data**: Using Python, simulate 5,000 samples from a normal distribution with a mean of 2 and a variance of 4. Compute the sample mean, variance, skewness, and kurtosis.

10. **Log-Normal Simulation**: Simulate 2,000 samples from a log-normal distribution with \( \mu = 0 \) and \( \sigma = 0.75 \) and plot the histogram of the simulated data.

#### 2.1.2 Expectation and Moments

11. **Expectation Calculation**: Calculate the expectation of a random variable \( Y \) where \( Y \) is uniformly distributed between 4 and 10.

12. **Variance Calculation**: If \( Y \) is exponentially distributed with parameter \( \lambda = 0.5 \), find the variance of \( Y \).

13. **Skewness and Kurtosis**: Compute the skewness and kurtosis of a normal distribution with mean 15 and variance 9.

14. **Empirical Moments**: Given a sample dataset with values {1, 2, 2, 3, 4}, compute the empirical mean, variance, skewness, and kurtosis.

15. **Comparing Distributions**: Compare the skewness and kurtosis of a normal distribution with that of a uniform distribution on \{1, 2, 3, 4\}.

16. **Moment Generating Functions**: Derive the moment-generating function (MGF) for a Poisson random variable with parameter \( \lambda \) and find the first two moments.

17. **Variance of a Sum**: If \( Y_1 \) and \( Y_2 \) are independent random variables with \( Var(Y_1) = 2 \) and \( Var(Y_2) = 3 \), compute the variance of \( Y_1 + Y_2 \).

18. **Covariance Calculation**: Given two random variables \( Y_1 \) and \( Y_2 \) with \( E[Y_1] = 5, E[Y_2] = 3 \), and \( E[Y_1Y_2] = 20 \), calculate the covariance \( Cov(Y_1, Y_2) \).

19. **Law of Total Expectation**: If \( Y \) is a random variable with \( E[Y | X = x] = 2x + 3 \) and \( E[X] = 4 \), find \( E[Y] \).

20. **Cauchy-Schwarz Inequality**: Demonstrate the Cauchy-Schwarz inequality for two random variables and give an example.

### 2.2 Statistical Inference

#### 2.2.1 Hypothesis Testing

21. **t-Test Application**: Perform a one-sample t-test on the dataset {4, 5, 6, 8, 7} to determine if the sample mean significantly differs from the population mean of 6.

22. **Chi-Square Test**: Use a chi-square test to determine if the observed frequencies in the table below differ from the expected frequencies.

    | Category | Observed | Expected |
    |----------|----------|----------|
    | A        | 15       | 10       |
    | B        | 30       | 30       |
    | C        | 20       | 30       |

23. **Confidence Intervals**: Calculate a 90% confidence interval for the mean of a normally distributed sample with a sample mean of 50 and a known standard deviation of 10 based on a sample size of 25.

24. **p-Value Calculation**: Compute the p-value for a t-test where the test statistic is 1.8 and the degrees of freedom are 15.

25. **Power of a Test**: Given a sample size of 30, an effect size of 0.5, and a significance level of 0.05, determine the power of a one-sample t-test.

26. **Paired t-Test**: Conduct a paired t-test on the datasets {3, 5, 2, 4} and {4, 6, 3, 5} and interpret the results.

27. **One-Way ANOVA**: Perform a one-way ANOVA test to determine if there are significant differences among the means of three different groups given the following data: Group 1: {5, 7, 8}, Group 2: {9, 10, 11}, Group 3: {12, 13, 14}.

28. **Multiple Comparisons**: Apply the Tukey's HSD test to adjust for multiple comparisons in the previous ANOVA exercise.

29. **Z-Test**: Given a sample mean of 100, a population mean of 95, and a standard deviation of 10, conduct a z-test to determine if the sample mean significantly differs from the population mean.

30. **Hypothesis Test for Proportions**: Given that 70 out of 200 surveyed individuals preferred product A over product B, perform a hypothesis test to determine if the proportion of preferences for product A is significantly greater than 0.25.

### 2.3 Time Series Analysis

#### 2.3.1 ARIMA Models

31. **ARIMA Identification**: Given the time series data for monthly sales, create and interpret ACF and PACF plots to identify the appropriate ARIMA model.

32. **ARIMA Fitting**: Fit an ARIMA(1,1,1) model to a given time series dataset and interpret the coefficients of the model.

33. **Model Diagnostics**: Assess the residuals of a fitted ARIMA model for normality and independence using a Q-Q plot and the Ljung-Box test.

34. **Forecasting**: Use a fitted ARIMA model to forecast the next 6 months of sales data and evaluate the forecast accuracy using MSE.

35. **Differencing**: Apply differencing to the time series dataset to achieve stationarity and provide a summary of changes to the data.

36. **Model Selection**: Use the AIC and BIC criteria to compare the performance of different ARIMA models on a given time series dataset.

37. **Seasonal ARIMA**: Fit a seasonal ARIMA model to monthly sales data and interpret the seasonal coefficients.

38. **Outlier Detection**: Identify and handle outliers in a time series dataset before fitting an ARIMA model using statistical tests or visualization.

39. **Model Validation**: Validate the fitted ARIMA model using an out-of-sample dataset and calculate the forecast accuracy metrics, including MAE and RMSE.

40. **ARIMA vs. Exponential Smoothing**: Fit an ARIMA model and an exponential smoothing model to the same time series data and compare their performance using a validation dataset.

#### 2.3.2 GARCH Models

41. **GARCH Identification**: Given daily return data for a stock, identify the appropriate GARCH model by examining the ACF of squared returns.

42. **GARCH Fitting**: Fit a GARCH(1,1) model to the daily returns of a stock and interpret the estimated parameters, including the significance of the coefficients.

43. **Volatility Forecasting**: Use a fitted GARCH

 model to forecast the next month's volatility of a stock and assess the forecast accuracy against realized volatility.

44. **Model Comparison**: Compare the performance of different GARCH models (e.g., GARCH, EGARCH) based on their ability to predict volatility on a test dataset.

45. **Model Diagnostics**: Perform diagnostic checks on the residuals of a GARCH model to verify that they exhibit no autocorrelation and are homoscedastic.

46. **Backtesting**: Backtest the volatility forecasts from a GARCH model using historical data and evaluate its predictive performance using various metrics.

47. **Risk Management**: Estimate Value at Risk (VaR) for a portfolio of assets using a fitted GARCH model.

48. **Volatility Spillover**: Investigate volatility spillover effects between different stocks using a multivariate GARCH model.

49. **Robustness Check**: Assess the robustness of a GARCH model by applying it to different subsets of data (e.g., pre- and post-crisis periods).

50. **Parameter Sensitivity**: Analyze the sensitivity of the GARCH model’s forecasts to changes in the parameters using simulations.

### 2.4 Practical Exercises

51. **Data Analysis**: Collect a real-world dataset (e.g., stock prices) and perform exploratory data analysis using summary statistics and visualizations.

52. **Financial Modeling**: Build a financial model to predict future stock prices based on historical data, applying regression or time series techniques.

53. **Risk Management**: Develop a quantitative risk management strategy for a portfolio using Monte Carlo simulations to estimate potential losses.

54. **Algorithmic Trading**: Implement a simple algorithmic trading strategy based on moving averages and backtest its performance on historical data.

55. **Report Writing**: Prepare a comprehensive report detailing a quantitative finance project, including data analysis, model fitting, results, and conclusions.

56. **Data Cleaning**: Given a dataset with missing values, perform data cleaning and imputation techniques to prepare the data for analysis.

57. **Feature Engineering**: Create additional features for a financial dataset (e.g., moving averages, volatility measures) to enhance a predictive model.

58. **Data Visualization**: Create meaningful visualizations (e.g., time series plots, histograms, boxplots) to communicate insights from a financial dataset.

59. **Predictive Analytics**: Apply machine learning techniques (e.g., decision trees, random forests) to build predictive models for stock prices.

60. **Scenario Analysis**: Conduct scenario analysis to evaluate the impact of different market conditions on a portfolio's performance.

61. **Stress Testing**: Develop a stress testing framework for a financial institution to evaluate its resilience against economic shocks.

62. **Portfolio Optimization**: Use the mean-variance optimization framework to construct an optimal investment portfolio based on expected returns and risk.

63. **Time Series Decomposition**: Decompose a time series into its trend, seasonal, and residual components and interpret the results.

64. **Cross-Validation**: Implement cross-validation techniques to assess the performance of a predictive model on a financial dataset.

65. **Hypothesis Testing in Practice**: Apply hypothesis testing techniques to real-world data, interpreting the results in the context of a financial decision.

66. **Exploratory Data Analysis**: Conduct an exploratory data analysis on a financial dataset, summarizing key findings and visualizing the data.

67. **Simulation Studies**: Perform a Monte Carlo simulation study to assess the risk and return of an investment strategy.

68. **Market Research**: Analyze consumer preference data using statistical techniques to inform product development strategies.

69. **A/B Testing**: Design and analyze an A/B test for a marketing campaign, determining the effectiveness of different strategies.

70. **Time Series Clustering**: Implement clustering techniques to group similar time series data and interpret the results in a financial context.

71. **Quantitative Risk Assessment**: Conduct a quantitative assessment of credit risk using models like logistic regression or decision trees.

72. **Data-Driven Decision Making**: Create a case study on how data-driven approaches can enhance decision-making in financial institutions.

73. **Financial Derivatives Pricing**: Model the pricing of financial derivatives using Black-Scholes or binomial models and analyze the sensitivity of the price to different parameters.

74. **Event Study Analysis**: Perform an event study analysis to assess the impact of a specific event (e.g., earnings announcement) on stock prices.

75. **Ethical Considerations**: Discuss the ethical implications of using data analytics in finance, focusing on transparency and fairness.

76. **Sensitivity Analysis**: Conduct a sensitivity analysis on a financial model to evaluate how changes in assumptions affect outcomes.

77. **Implementation of a Trading Algorithm**: Design and implement a simple trading algorithm based on a given strategy and evaluate its performance in a backtest.

78. **Regime-Switching Models**: Fit a regime-switching model to a financial time series and interpret the switching behavior.

79. **Quantitative Finance Research**: Conduct a literature review on a current topic in quantitative finance, summarizing key findings and methodologies.

80. **Risk Metrics Calculation**: Calculate and interpret various risk metrics (e.g., Sharpe ratio, Sortino ratio) for an investment portfolio.

### 2.5 Applications of Probability in Finance

81. **Risk-Return Tradeoff**: Analyze the risk-return tradeoff for a set of financial assets and construct a corresponding risk-return plot.

82. **Dynamic Asset Allocation**: Develop a dynamic asset allocation strategy that adjusts based on market conditions and historical performance.

83. **Portfolio Rebalancing**: Implement a portfolio rebalancing strategy and analyze its effectiveness in maintaining risk levels.

84. **Black-Litterman Model**: Use the Black-Litterman model to adjust the expected returns of a portfolio based on investor views.

85. **Market Microstructure Analysis**: Examine the impact of market microstructure on asset pricing and trading strategies.

86. **Hedging Strategies**: Design hedging strategies for a financial portfolio using options or futures and analyze their effectiveness.

87. **Credit Risk Modeling**: Develop a credit risk model using logistic regression to predict the likelihood of default on loans.

88. **Financial Market Predictions**: Utilize historical data to build predictive models for future market movements and assess their accuracy.

89. **Risk Factors Analysis**: Identify and analyze key risk factors affecting asset prices in a specific market.

90. **Behavioral Finance Implications**: Explore the implications of behavioral finance on market efficiency and investment strategies.

91. **Statistical Arbitrage**: Implement a statistical arbitrage strategy based on pairs trading and evaluate its profitability.

92. **Financial Reporting Analysis**: Analyze financial statements using ratio analysis to assess the financial health of a company.

93. **Mergers and Acquisitions Valuation**: Use quantitative methods to assess the value of a merger or acquisition.

94. **Environmental, Social, and Governance (ESG) Investing**: Investigate the performance of ESG investments and their implications for risk management.

95. **Blockchain and Finance**: Examine the impact of blockchain technology on financial markets and its potential for innovation.

96. **Robo-Advisory Services**: Evaluate the effectiveness of robo-advisory services in personal finance management and investment.

97. **Financial Regulation Impact**: Analyze the impact of financial regulation on market behavior and investment strategies.

98. **Alternative Investment Strategies**: Investigate alternative investment strategies, such as hedge funds and private equity, and their risk profiles.

99. **Crowdfunding Analysis**: Analyze the success factors of crowdfunding campaigns using statistical methods.

100. **Algorithmic Risk Management**: Develop algorithms for risk management that utilize real-time data analytics and predictive modeling.
