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

```bash
// Function to calculate the PDF of a normal distribution
function NormalDistributionPDF(x, mu, sigma):
    // Step 1: Calculate the variance
    variance = sigma^2
    
    // Step 2: Calculate the coefficient
    coefficient = 1 / (SquareRoot(2 * PI * variance))
    
    // Step 3: Calculate the exponent
    exponent = -((x - mu)^2) / (2 * variance)
    
    // Step 4: Calculate the PDF value
    pdf_value = coefficient * Exponential(exponent)
    
    return pdf_value

// Function to calculate the square root
function SquareRoot(value):
    return value^(0.5)  // Using exponentiation for square root

// Function to calculate the exponential
function Exponential(value):
    return e^(value)  // Using Euler's number for the exponential function

// Example usage
mu = 0               // Mean of the distribution
sigma = 1            // Standard deviation of the distribution
x = 1.5              // Value at which to calculate the PDF

// Calculate PDF for normal distribution at x
pdf_result = NormalDistributionPDF(x, mu, sigma)

// Output the result
Print("PDF of Normal Distribution at x =", x, "is", pdf_result)
```

2. **Log-Normal Distribution**:
    - A random variable \( X \) is **log-normally** distributed if \( \log(X) \) follows a normal distribution. That is, \( \log(X) \sim \mathcal{N}(\mu, \sigma^2) \).
    - The PDF of a log-normal distribution is:

            f_X(x) = \frac{1}{x\sigma\sqrt{2\pi}} \exp \left( -\frac{(\log(x) - \mu)^2}{2\sigma^2} \right)
$$

    - Log-normal distributions are often used in finance to model stock prices because stock prices cannot be negative and tend to exhibit exponential growth.

```bash
// Function to calculate the PDF of a log-normal distribution
function LogNormalDistributionPDF(x, mu, sigma):
    // Step 1: Check if x is positive
    if x <= 0:
        return 0  // Log-normal distribution is only defined for x > 0

    // Step 2: Calculate the variance
    variance = sigma^2

    // Step 3: Calculate the coefficient
    coefficient = 1 / (x * sigma * SquareRoot(2 * PI))

    // Step 4: Calculate the exponent
    log_value = Logarithm(x)  // Calculate the natural logarithm of x
    exponent = -((log_value - mu)^2) / (2 * variance)

    // Step 5: Calculate the PDF value
    pdf_value = coefficient * Exponential(exponent)

    return pdf_value

// Function to calculate the square root
function SquareRoot(value):
    return value^(0.5)  // Using exponentiation for square root

// Function to calculate the natural logarithm
function Logarithm(value):
    return ln(value)  // Using natural logarithm function

// Function to calculate the exponential
function Exponential(value):
    return e^(value)  // Using Euler's number for the exponential function

// Example usage
mu = 0               // Mean of the log-normal distribution
sigma = 1            // Standard deviation of the log-normal distribution
x = 2.5              // Value at which to calculate the PDF

// Calculate PDF for log-normal distribution at x
pdf_result = LogNormalDistributionPDF(x, mu, sigma)

// Output the result
Print("PDF of Log-Normal Distribution at x =", x, "is", pdf_result)
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

##### Example: Calculating Moments

```bash
// Function to calculate mean
function CalculateMean(data):
    total_sum = 0
    n = Length(data)  // Get the number of data points
    for each value in data:
        total_sum = total_sum + value
    return total_sum / n  // Return the mean

// Function to calculate variance
function CalculateVariance(data, mean):
    total_squared_difference = 0
    n = Length(data)
    for each value in data:
        total_squared_difference = total_squared_difference + (value - mean)^2
    return total_squared_difference / n  // Return the variance

// Function to calculate skewness
function CalculateSkewness(data, mean, std_dev):
    total_cubed_difference = 0
    n = Length(data)
    for each value in data:
        total_cubed_difference = total_cubed_difference + (value - mean)^3
    return total_cubed_difference / (n * std_dev^3)  // Return skewness

// Function to calculate kurtosis
function CalculateKurtosis(data, mean, std_dev):
    total_quartic_difference = 0
    n = Length(data)
    for each value in data:
        total_quartic_difference = total_quartic_difference + (value - mean)^4
    return (total_quartic_difference / (n * std_dev^4)) - 3  // Return excess kurtosis

// Example usage
normal_data = [value1, value2, value3, ..., valueN]  // Replace with actual data

// Step 1: Calculate mean
mean = CalculateMean(normal_data)

// Step 2: Calculate variance
variance = CalculateVariance(normal_data, mean)

// Step 3: Calculate standard deviation
std_dev = SquareRoot(variance)  // Assuming a SquareRoot function exists

// Step 4: Calculate skewness
skewness = CalculateSkewness(normal_data, mean, std_dev)

// Step 5: Calculate kurtosis
kurtosis = CalculateKurtosis(normal_data, mean, std_dev)

// Step 6: Output the results
Print("Mean: ", mean)
Print("Variance: ", variance)
Print("Skewness: ", skewness)
Print("Kurtosis: ", kurtosis)
```

---

### 2.2 Statistical Inference

Statistical inference allows us to draw conclusions about a population based on sample data. Two fundamental components of statistical inference are **estimation** and **hypothesis testing**.

#### 2.2.1 Hypothesis Testing

In hypothesis testing, we start by formulating two hypotheses:

- **Null Hypothesis (H₀)**: The assumption we are testing, typically a statement of "no effect" or "no difference".
- **Alternative Hypothesis (H₁)**: What we seek to support, often representing a difference or an effect.

We use sample data to evaluate whether the null hypothesis can be rejected in favor of the alternative hypothesis. 

```
// Step 1: Define Hypotheses
function DefineHypotheses():
    // Null Hypothesis (H₀)
    H0 = "There is no effect or no difference"  
    // Alternative Hypothesis (H₁)
    H1 = "There is an effect or a difference"
    return H0, H1

// Step 2: Collect Sample Data
function CollectSampleData():
    sample_data = []  // Initialize an empty list for sample data
    // Assuming we have a function to input or generate sample data
    while (length of sample_data < desired_sample_size):
        value = InputSampleValue()  // Function to input sample values
        Append(sample_data, value)  // Add value to sample data
    return sample_data

// Step 3: Perform Statistical Test
function PerformStatisticalTest(sample_data):
    // Calculate sample mean, sample size, and sample standard deviation
    sample_mean = CalculateMean(sample_data)  // Call function to calculate mean
    sample_size = Length(sample_data)          // Get the number of observations
    sample_std_dev = CalculateStandardDeviation(sample_data)  // Call function for standard deviation

    // Choose significance level (e.g., alpha = 0.05)
    alpha = 0.05

    // Calculate test statistic (e.g., t-test or z-test depending on sample size and distribution)
    test_statistic = CalculateTestStatistic(sample_mean, sample_std_dev, sample_size) 

    // Step 4: Determine Critical Value or P-value
    critical_value = CalculateCriticalValue(alpha, sample_size)  // Define based on test type (t-test or z-test)
    p_value = CalculatePValue(test_statistic, sample_size)  // Function to calculate p-value

    return test_statistic, critical_value, p_value

// Step 5: Evaluate Null Hypothesis
function EvaluateNullHypothesis(test_statistic, critical_value, p_value, alpha):
    // Decision rule based on the test
    if (test_statistic > critical_value or p_value < alpha):
        decision = "Reject H₀"  // Null hypothesis is rejected
    else:
        decision = "Fail to Reject H₀"  // Null hypothesis is not rejected
    return decision

// Step 6: Conclusion
function Conclusion(decision, H0, H1):
    if (decision == "Reject H₀"):
        Print("We have sufficient evidence to support H₁: ", H1)
    else:
        Print("We do not have sufficient evidence to reject H₀: ", H0)

// Main execution flow
H0, H1 = DefineHypotheses()  // Step 1
sample_data = CollectSampleData()  // Step 2
test_statistic, critical_value, p_value = PerformStatisticalTest(sample_data)  // Step 3
decision = EvaluateNullHypothesis(test_statistic, critical_value, p_value, alpha)  // Step 4
Conclusion(decision, H0, H1)  // Step 5
```

##### Test Statistic
The choice of the test statistic depends on the specific test being performed. Common tests include:

1. **t-Test**: Used to compare the means of two groups. The test statistic is:

      $t = \frac{\bar{X}_1 - \bar{X}_2}{s \sqrt{\frac{1}{n_1} + \frac{1}{n_2}}}$

   Where \( \bar{X}_1 \) and \( \bar{X}_2 \) are the sample means, \( s \) is the pooled standard deviation, and \( n_1 \), \( n_2 \) are the sample sizes.

```bash
// Function to calculate t-Test statistic
function CalculateTTestStatistic(sample1, sample2):
    // Step 1: Calculate sample means
    mean1 = CalculateMean(sample1)  // Function to calculate mean of sample1
    mean2 = CalculateMean(sample2)  // Function to calculate mean of sample2

    // Step 2: Calculate sample sizes
    n1 = Length(sample1)  // Size of sample1
    n2 = Length(sample2)  // Size of sample2

    // Step 3: Calculate sample standard deviations
    std1 = CalculateStandardDeviation(sample1)  // Function to calculate std deviation of sample1
    std2 = CalculateStandardDeviation(sample2)  // Function to calculate std deviation of sample2

    // Step 4: Calculate pooled standard deviation
    pooled_std = sqrt(((n1 - 1) * std1^2 + (n2 - 1) * std2^2) / (n1 + n2 - 2))

    // Step 5: Calculate t-statistic
    t_statistic = (mean1 - mean2) / (pooled_std * sqrt((1/n1) + (1/n2)))

    return t_statistic  // Return the calculated t-statistic
```

2. **Chi-Square Test**: Used to assess independence in categorical data. The test statistic is:

      $\chi^2 = \sum \frac{(O_i - E_i)^2}{E_i}$

   Where \( O_i \) are the observed frequencies, and \( E_i \) are the expected frequencies under the null hypothesis.

```bash
// Function to calculate Chi-Square test statistic
function CalculateChiSquareStatistic(observed_frequencies, expected_frequencies):
    // Initialize chi-square statistic
    chi_square_statistic = 0

    // Step 1: Ensure observed and expected frequencies are of the same length
    if Length(observed_frequencies) != Length(expected_frequencies):
        Print("Error: Observed and expected frequencies must have the same length.")
        return null  // Return null if the lengths don't match

    // Step 2: Calculate the chi-square statistic
    for i from 0 to Length(observed_frequencies) - 1 do:
        O_i = observed_frequencies[i]  // Observed frequency for category i
        E_i = expected_frequencies[i]  // Expected frequency for category i
        
        if E_i > 0 then:
            chi_square_statistic += (O_i - E_i)^2 / E_i  // Update chi-square statistic

    return chi_square_statistic  // Return the calculated chi-square statistic
```

##### Python Example: t-Test

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

#### 2.3.2 GARCH Models

**Generalized Autoregressive Conditional Heteroskedasticity (GARCH)** models are used to model time series data where volatility changes over time. GARCH models capture "volatility clustering", a common phenomenon in financial time series.

The GARCH(1,1) model is given by:

$\sigma_t^2 = \alpha_0 + \alpha_1 \epsilon_{t-1}^2 + \beta_1 \sigma_{t-1}^2$

Where \( \sigma_t^2 \) is the conditional variance at time \( t \), and \( \epsilon_{t-1} \) is the error term at time \( t-1 \).

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
