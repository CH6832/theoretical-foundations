# Financial Modeling: Theoretical Background and Practical Examples

## Probability Theory

### Random Variables and Distributions

**Random Variables:** A random variable \(X\) is a function that assigns a real number to each outcome of a random process. Random variables can be classified into:

- **Discrete Random Variables:** Can take on a countable number of values. For example, the number of heads in a series of coin flips.
- **Continuous Random Variables:** Can take on any value within a range. For example, stock prices.

**Probability Mass Function (PMF) for Discrete Random Variables:**  
For a discrete random variable \(X\), the PMF is given by:

$P(X = x) = p(x)$

where \(p(x)\) is the probability that \(X\) takes the value \(x\).

**Probability Density Function (PDF) for Continuous Random Variables:**  
For a continuous random variable \(X\), the PDF is denoted by \(f_X(x)\). The probability that \(X\) falls within an interval \([a, b]\) is computed as:

$P(a \leq X \leq b) = \int_a^b f_X(x) \, dx$

**Key Probability Distributions:**

- **Normal Distribution:** Defined by its mean \(\mu\) and standard deviation \(\sigma\). The PDF is:

$f_X(x) = \frac{1}{\sqrt{2\pi\sigma^2}} \exp \left( -\frac{(x - \mu)^2}{2\sigma^2} \right)$

This function describes a symmetric, bell-shaped curve centered around the mean \(\mu\). The parameter \(\sigma\) controls the spread of the distribution.

- **Log-Normal Distribution:** A random variable \(X\) is log-normally distributed if \(\log(X)\) is normally distributed. Its PDF is:

$f_X(x) = \frac{1}{x\sigma\sqrt{2\pi}} \exp \left( -\frac{(\log(x) - \mu)^2}{2\sigma^2} \right)$

This distribution is used when the variable of interest is strictly positive and the logarithm of the variable follows a normal distribution.

**Python Example:**

```python
import numpy as np
import matplotlib.pyplot as plt

# Simulating a random variable for daily returns
daily_return = np.random.normal(0, 0.01, 1000)

# Plotting the distribution
plt.hist(daily_return, bins=30, density=True, alpha=0.6, color='g')
plt.title("Histogram of Daily Returns")
plt.show()
```

### Expectation and Moments

**Expectation (Mean):** The expectation \(E[X]\) of a random variable \(X\) represents the average value over many trials.

**Discrete Random Variables:**  

$E[X] = \sum_{i} x_i \cdot p(x_i)$

Here, \(x_i\) are the possible values of \(X\), and \(p(x_i)\) are their probabilities.

**Continuous Random Variables:**  

$E[X] = \int_{-\infty}^{\infty} x \cdot f_X(x) \, dx$

This integral computes the average value of the continuous random variable by weighing each possible value by its probability density.

**Variance:** Measures the spread of values around the mean. It is given by:

$\text{Var}(X) = E[(X - E[X])^2]$

Variance can also be calculated as:

$\text{Var}(X) = E[X^2] - (E[X])^2$

It measures how much the values of \(X\) deviate from the mean on average.

**Skewness:** Measures the asymmetry of the distribution. It is given by:

$\text{Skewness} = \frac{E[(X - E[X])^3]}{(\text{Var}(X))^{3/2}}$

Positive skewness indicates a distribution with a long right tail, while negative skewness indicates a long left tail.

**Kurtosis:** Measures the "tailedness" of the distribution. It is given by:

$\text{Kurtosis} = \frac{E[(X - E[X])^4]}{(\text{Var}(X))^2} - 3$

A higher kurtosis indicates heavier tails and a sharper peak compared to a normal distribution.

**Python Example:**

```python
import numpy as np

# Calculating moments
mean = np.mean(daily_return)
variance = np.var(daily_return)
skewness = np.mean((daily_return - mean)**3) / np.std(daily_return)**3
kurtosis = np.mean((daily_return - mean)**4) / np.std(daily_return)**4

print(f"Mean: {mean}, Variance: {variance}, Skewness: {skewness}, Kurtosis: {kurtosis}")
```

## Statistical Inference

### Hypothesis Testing

**Principles:** Hypothesis testing involves making an assumption (the null hypothesis \(H_0\)) and determining if there is enough evidence to reject it in favor of an alternative hypothesis \(H_1\).

**Common Tests:**

- **t-Test:** Compares the means of two groups. The test statistic is:

$t = \frac{\bar{X}_1 - \bar{X}_2}{s \sqrt{\frac{1}{n_1} + \frac{1}{n_2}}}$

where \(\bar{X}_1\) and \(\bar{X}_2\) are the sample means, \(s\) is the pooled standard deviation, and \(n_1\) and \(n_2\) are the sample sizes. This test assesses if the difference between the means is statistically significant.

- **Chi-Square Test:** Tests the independence of categorical variables. The test statistic is:

$\chi^2 = \sum \frac{(O_i - E_i)^2}{E_i}$

where \(O_i\) is the observed frequency and \(E_i\) is the expected frequency. This statistic measures how well the observed frequencies match the expected frequencies under the null hypothesis.

**Python Example:**

```python
from scipy import stats

# t-test example
t_stat, p_value = stats.ttest_1samp(daily_return, 0)
print(f"T-statistic: {t_stat}, P-value: {p_value}")
```

### Confidence Intervals

**Construction:** A confidence interval provides a range in which we expect the true parameter to lie with a certain confidence level. For a mean with a known standard deviation:

$\text{CI} = \bar{X} \pm Z \cdot \frac{\sigma}{\sqrt{n}}$

where \(\bar{X}\) is the sample mean, \(Z\) is the Z-score corresponding to the desired confidence level, \(\sigma\) is the standard deviation, and \(n\) is the sample size. This interval captures the true mean with a given level of confidence.

**Python Example:**

```python
from scipy import stats

# Confidence interval calculation
conf_interval = stats.norm.interval(0.95, loc=np.mean(daily_return), scale=stats.sem(daily_return))
print(f"95% Confidence Interval: {conf_interval}")
```

### Maximum Likelihood Estimation (MLE)

**MLE Techniques:** MLE estimates parameters by maximizing the likelihood function. For a parameter \(\theta\), the likelihood function is:

$L(\theta) = \prod_{i=1}^n f(x_i; \theta)$

where \(f(x_i; \theta)\) is the probability density function for the parameter \(\theta\). MLE finds the parameter values that make the observed data most probable.

**Python Example:**

```python
from scipy import stats

# MLE for normal distribution
mean_mle, std_mle = stats.norm.fit(daily_return)
print(f"MLE Estimates - Mean: {mean_mle}, Std Dev: {std_mle}")
```

## Linear Regression

### Ordinary Least Squares (OLS)

**Fundamentals:** OLS estimates parameters by minimizing the sum of squared residuals. The OLS estimator for parameters \(\beta\) is:

$\hat{\beta} = (X^T X)^{-1} X^T y$

where \(X\) is the matrix of explanatory variables, \(y\) is the vector of observed values, and \(\hat{\beta}\) are the estimated coefficients.

**Application:** In finance, OLS can be used to model relationships between financial variables, such as the relationship between stock returns and market indices.

**Python Example:**

```python
import statsmodels.api as sm

# OLS regression
X = sm.add_constant(X)  # Adding a constant term
model = sm.OLS(y, X).fit()
print(model.summary())
```

### Diagnostics and Multicollinearity

**Diagnostics:** Includes residual analysis to check for model validity. Residuals should be randomly distributed with constant variance. The R-squared value measures the proportion of variance explained by the model:

$R^2 = 1 - \frac{\text{RSS}}{\text{TSS}}$

where RSS is the residual sum of squares and TSS is the total sum of squares.

**Multicollinearity:** Occurs when independent variables are highly correlated. The Variance Inflation Factor (V

IF) measures the degree of multicollinearity:

$\text{VIF} = \frac{1}{1 - R_i^2}$

where \(R_i^2\) is the R-squared from regressing the \(i\)-th variable on the others. A VIF value above 10 suggests high multicollinearity, which may inflate the variance of the coefficient estimates.

**Python Example:**

```python
from statsmodels.stats.outliers_influence import variance_inflation_factor

# Calculate VIF
vif = pd.DataFrame()
vif["VIF Factor"] = [variance_inflation_factor(X.values, i) for i in range(X.shape[1])]
vif["features"] = X.columns
print(vif)
```

## Time Series Analysis

### ARIMA Models

**Autoregressive Integrated Moving Average (ARIMA):** ARIMA models are used for forecasting time series data by combining autoregression (AR), differencing (I), and moving averages (MA).

**ARIMA Model:** The ARIMA model is denoted by ARIMA(p, d, q) where:
- \(p\) is the number of lag observations (autoregressive part),
- \(d\) is the degree of differencing (to make the series stationary),
- \(q\) is the size of the moving average window.

The model is given by:

$Y_t = c + \phi_1 Y_{t-1} + \phi_2 Y_{t-2} + \dots + \phi_p Y_{t-p} + \theta_1 \epsilon_{t-1} + \dots + \theta_q \epsilon_{t-q} + \epsilon_t$

where \(\epsilon_t\) is white noise.

**Python Example:**

```python
import pandas as pd
from statsmodels.tsa.arima.model import ARIMA

# ARIMA model fitting
model = ARIMA(time_series_data, order=(p,d,q))
model_fit = model.fit()
print(model_fit.summary())
```

### GARCH Models

**Generalized Autoregressive Conditional Heteroskedasticity (GARCH):** GARCH models estimate the volatility of time series data. A GARCH(p, q) model is defined as:

$\sigma_t^2 = \alpha_0 + \sum_{i=1}^p \alpha_i \epsilon_{t-i}^2 + \sum_{j=1}^q \beta_j \sigma_{t-j}^2$

where \(\sigma_t^2\) is the variance of the error term at time \(t\), \(\epsilon_t\) is the residual error, and \(\alpha_i\) and \(\beta_j\) are coefficients.

**Python Example:**

```python
from arch import arch_model

# GARCH model fitting
garch_model = arch_model(time_series_data, vol='Garch', p=1, q=1)
garch_fit = garch_model.fit()
print(garch_fit.summary())
```

## Portfolio Optimization

### Mean-Variance Optimization

**Markowitz Portfolio Theory:** Seeks to optimize the trade-off between portfolio risk and return. The optimal portfolio minimizes variance for a given expected return:

$\text{Minimize} \quad \sigma_p^2 = \mathbf{w}^T \mathbf{\Sigma} \mathbf{w}$
$\text{Subject to} \quad \mathbf{w}^T \mathbf{1} = 1, \quad \mathbf{w}^T \mathbf{\mu} = \mu_p$

where \(\mathbf{w}\) is the vector of asset weights, \(\mathbf{\Sigma}\) is the covariance matrix, \(\mathbf{1}\) is a vector of ones, and \(\mathbf{\mu}\) is the vector of expected returns.

**Python Example:**

```python
import numpy as np
import cvxpy as cp

# Covariance matrix and expected returns
cov_matrix = np.cov(returns)
expected_returns = np.mean(returns, axis=0)

# Portfolio optimization
w = cp.Variable(n)
risk = cp.quad_form(w, cov_matrix)
ret = expected_returns.T @ w
prob = cp.Problem(cp.Minimize(risk), [cp.sum(w) == 1, ret >= target_return])
prob.solve()

print("Optimal weights:", w.value)
```

### Efficient Frontier

**Concept:** The efficient frontier represents the set of optimal portfolios that offer the highest expected return for a given level of risk. These portfolios are graphically represented on a curve in risk-return space.

**Python Example:**

```python
import matplotlib.pyplot as plt

# Simulating portfolios
returns_simulated, risks_simulated = simulate_portfolios(returns)

# Plotting the efficient frontier
plt.plot(risks_simulated, returns_simulated, 'o', markersize=2)
plt.xlabel('Risk (Standard Deviation)')
plt.ylabel('Return')
plt.title('Efficient Frontier')
plt.show()
```

## Monte Carlo Simulation

### Principles and Applications

**Principle:** Monte Carlo simulation uses random sampling to estimate mathematical functions and model systems with significant uncertainty. In finance, it is used to assess the risk of portfolios, option pricing, and other probabilistic scenarios.

**Application:** Simulating the future price of a stock based on historical volatility.

**Python Example:**

```python
# Simulating future stock prices
n_simulations = 1000
simulated_prices = np.zeros(n_simulations)
initial_price = 100
for i in range(n_simulations):
    simulated_prices[i] = initial_price * np.exp(np.cumsum(daily_return)[-1])

plt.hist(simulated_prices, bins=30)
plt.title("Simulated Stock Prices")
plt.show()
```
