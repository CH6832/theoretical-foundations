# Quantitative Methods in Finance

## 1. Course Overview

This course provides a comprehensive introduction to quantitative methods used in finance. These methods rely on statistical and mathematical tools essential for financial analysis, decision-making, and risk management. We will cover topics ranging from probability theory, hypothesis testing, and statistical inference to time series analysis, including ARIMA and GARCH models.

By the end of this course, you will be equipped with the knowledge to apply these quantitative techniques to real-world financial problems.

---

## 2. Topics Covered

### 2.1 Probability Theory

Probability theory forms the backbone of quantitative finance by providing models for uncertainty and risk. We begin with an introduction to **random variables** and their distributions.

#### 2.1.1 Random Variables and Distributions

A **random variable** is a function that assigns a real number to each outcome in a sample space. Random variables are either:

- **Discrete Random Variables**: These take on a finite or countable number of values.
  
- **Continuous Random Variables**: These take values from a continuous range, such as any real number between a given range.

##### Probability Distribution

The **probability distribution** of a random variable tells us how likely different outcomes are. It is often described using a **Probability Density Function (PDF)** or **Cumulative Distribution Function (CDF)**.

- **Discrete Probability Distribution**: Given a discrete random variable \( X \), its probability distribution is:
  
    $P(X = x_i) = p(x_i)$

  Where \( p(x_i) \) is the probability of \( X \) taking on value \( x_i \).

- **Continuous Probability Distribution**: For continuous random variables, we describe probabilities using a **probability density function** \( f_X(x) \). The probability that \( X \) falls within a specific interval is given by the area under the curve of \( f_X(x) \) over that interval:
  
    $P(a \leq X \leq b) = \int_a^b f_X(x) \, dx$

##### Important Distributions in Finance

1. **Normal Distribution**:
    - Denoted \( X \sim \mathcal{N}(\mu, \sigma^2) \), where \( \mu \) is the mean and \( \sigma^2 \) is the variance.
    - The PDF of a normal distribution is:

            f_X(x) = \frac{1}{\sqrt{2\pi\sigma^2}} \exp \left( -\frac{(x - \mu)^2}{2\sigma^2} \right)
$$

    - The normal distribution is symmetric around the mean \( \mu \) and has a bell-shaped curve, which makes it a common model for asset returns under the assumption that they are normally distributed.

2. **Log-Normal Distribution**:
    - A random variable \( X \) is **log-normally** distributed if \( \log(X) \) follows a normal distribution. That is, \( \log(X) \sim \mathcal{N}(\mu, \sigma^2) \).
    - The PDF of a log-normal distribution is:

            f_X(x) = \frac{1}{x\sigma\sqrt{2\pi}} \exp \left( -\frac{(\log(x) - \mu)^2}{2\sigma^2} \right)
$$

    - Log-normal distributions are often used in finance to model stock prices because stock prices cannot be negative and tend to exhibit exponential growth.

##### Python Example: Simulating Normal and Log-Normal Data

```python
import numpy as np
import matplotlib.pyplot as plt

# Simulate normal and log-normal random variables
normal_data = np.random.normal(0, 1, 1000)
log_normal_data = np.random.lognormal(0, 0.1, 1000)

# Plot histograms
plt.figure(figsize=(12, 5))
plt.subplot(1, 2, 1)
plt.hist(normal_data, bins=30, density=True, alpha=0.6, color='g')
plt.title('Normal Distribution')

plt.subplot(1, 2, 2)
plt.hist(log_normal_data, bins=30, density=True, alpha=0.6, color='b')
plt.title('Log-Normal Distribution')

plt.show()
```

---

#### 2.1.2 Expectation and Moments

Moments are key descriptive statistics that provide insights into the shape of a probability distribution.

1. **Expectation (Mean)**:
   - The expectation (or mean) of a random variable \( X \), denoted \( E[X] \), represents the average value that \( X \) takes on. It is calculated differently for discrete and continuous random variables:
   
   - **For Discrete Random Variables**:
          E[X] = \sum_{i} x_i \cdot p(x_i)
$$
     Where \( x_i \) are the possible values of \( X \), and \( p(x_i) \) are their associated probabilities.
     
   - **For Continuous Random Variables**:
          E[X] = \int_{-\infty}^{\infty} x \cdot f_X(x) \, dx
$$
     Where \( f_X(x) \) is the PDF of \( X \).

2. **Variance**:
   - The variance \( \text{Var}(X) \) measures the spread or dispersion of \( X \) around its mean. The formula is:
   
          \text{Var}(X) = E[(X - E[X])^2]
$$

     Alternatively, using the law of total expectation:
          \text{Var}(X) = E[X^2] - (E[X])^2
$$

3. **Skewness**:
   - Skewness measures the asymmetry of the probability distribution. A positive skew indicates a long right tail, and a negative skew indicates a long left tail. It is calculated as:
   
          \text{Skewness} = \frac{E[(X - E[X])^3]}{(\text{Var}(X))^{3/2}}
$$

4. **Kurtosis**:
   - Kurtosis measures the "tailedness" of the distribution (i.e., how heavy the tails are relative to the normal distribution). Excess kurtosis is the difference between a distribution's kurtosis and the kurtosis of a normal distribution (which is 3):
   
          \text{Kurtosis} = \frac{E[(X - E[X])^4]}{(\text{Var}(X))^2} - 3
$$

##### Python Example: Calculating Moments

```python
import numpy as np

# Calculate moments for the normal distribution data
mean = np.mean(normal_data)
variance = np.var(normal_data)
skewness = np.mean((normal_data - mean)**3) / np.std(normal_data)**3
kurtosis = np.mean((normal_data - mean)**4) / np.std(normal_data)**4 - 3  # Excess kurtosis

print(f"Mean: {mean}, Variance: {variance}, Skewness: {skewness}, Kurtosis: {kurtosis}")
```

---

### 2.2 Statistical Inference

Statistical inference allows us to draw conclusions about a population based on sample data. Two fundamental components of statistical inference are **estimation** and **hypothesis testing**.

#### 2.2.1 Hypothesis Testing

In hypothesis testing, we start by formulating two hypotheses:

- **Null Hypothesis (H₀)**: The assumption we are testing, typically a statement of "no effect" or "no difference".
- **Alternative Hypothesis (H₁)**: What we seek to support, often representing a difference or an effect.

We use sample data to evaluate whether the null hypothesis can be rejected in favor of the alternative hypothesis. 

##### Test Statistic
The choice of the test statistic depends on the specific test being performed. Common tests include:

1. **t-Test**: Used to compare the means of two groups. The test statistic is:

      $t = \frac{\bar{X}_1 - \bar{X}_2}{s \sqrt{\frac{1}{n_1} + \frac{1}{n_2}}}$

   Where \( \bar{X}_1 \) and \( \bar{X}_2 \) are the sample means, \( s \) is the pooled standard deviation, and \( n_1 \), \( n_2 \) are the sample sizes.

2. **Chi-Square Test**: Used to assess independence in categorical data. The test statistic is:

      $\chi^2 = \sum \frac{(O_i - E_i)^2}{E_i}$

   Where \( O_i \) are the observed frequencies, and \( E_i \) are the expected frequencies under the null hypothesis.

##### Python Example: t-Test

```python
from scipy import stats

# Perform a t-test on two halves of the normal data
t_stat, p_value = stats.ttest_ind(normal_data[:500], normal_data[500:])
print(f"t-statistic: {t_stat}, p-value: {p_value}")
```

---

### 2.3 Time Series Analysis

Time series analysis is crucial in finance for modeling data that are collected over time, such as stock prices,

 interest rates, and economic indicators.

#### 2.3.1 ARIMA Models

**Autoregressive Integrated Moving Average (ARIMA)** models are used to describe and predict time series data. The ARIMA model is composed of three components:

1. **Autoregressive (AR) Term**: Relates the current value of the series to past values.
2. **Integrated (I) Term**: Represents differencing of the time series to make it stationary.
3. **Moving Average (MA) Term**: Relates the current value to past forecast errors.

An ARIMA model is denoted as \( ARIMA(p, d, q) \), where:

- \( p \) is the number of autoregressive terms.
- \( d \) is the number of differences required to make the series stationary.
- \( q \) is the number of moving average terms.

##### Python Example: Fitting an ARIMA Model

```python
import statsmodels.api as sm

# Fit an ARIMA model to the normal data
model = sm.tsa.ARIMA(normal_data, order=(1, 1, 1))
results = model.fit()
print(results.summary())
```

#### 2.3.2 GARCH Models

**Generalized Autoregressive Conditional Heteroskedasticity (GARCH)** models are used to model time series data where volatility changes over time. GARCH models capture "volatility clustering", a common phenomenon in financial time series.

The GARCH(1,1) model is given by:

$\sigma_t^2 = \alpha_0 + \alpha_1 \epsilon_{t-1}^2 + \beta_1 \sigma_{t-1}^2$

Where \( \sigma_t^2 \) is the conditional variance at time \( t \), and \( \epsilon_{t-1} \) is the error term at time \( t-1 \).

##### Python Example: Fitting a GARCH Model

```python
from arch import arch_model

# Fit a GARCH(1,1) model
garch_model = arch_model(normal_data, vol='Garch', p=1, q=1)
garch_results = garch_model.fit()
print(garch_results.summary())
```

---

## 3. Assessment Methods

Students will be evaluated based on:

- **Assignments**: Hands-on practice involving real-world data analysis and financial modeling.
- **Midterm Exam**: Tests theoretical understanding of the covered concepts.
- **Final Project**: A comprehensive project requiring you to collect data, build financial models, and interpret the results.

---

## 4. Additional Resources

### 4.1 Recommended Textbooks

- James, G., Witten, D., Hastie, T., & Tibshirani, R. (2013). *An Introduction to Statistical Learning*. Springer.
- Tsay, R. S. (2010). *Analysis of Financial Time Series*. Wiley.

### 4.2 Online Resources

- [Khan Academy](https://www.khanacademy.org/)
- [Coursera Finance Courses](https://www.coursera.org/)
