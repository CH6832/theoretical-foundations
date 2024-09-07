# Elective III: Advanced Portfolio Management

## Course Overview
This course provides an in-depth exploration of advanced strategies and theories in portfolio management. Students will delve into modern portfolio theory, alternative investments, behavioral finance, and dynamic portfolio strategies. The course aims to equip students with the skills necessary to manage portfolios effectively, optimize returns, and control risks using quantitative techniques and an understanding of market behavior.

## Topics Covered

### **Mean-Variance Optimization**

#### **Efficient Frontier**

**Introduction to the Efficient Frontier:**
- The efficient frontier represents the set of optimal portfolios that offer the highest expected return \( \mathbb{E}[R_p] \) for a given level of risk \( \sigma_p \), or equivalently, the lowest risk for a given level of expected return. It is derived from the mean-variance optimization framework developed by Harry Markowitz.

**Mathematical Formulation:**
- Let \( w \) be the vector of portfolio weights, \( \mu \) the vector of expected returns, and \( \Sigma \) the covariance matrix of asset returns. The expected return and variance of the portfolio are given by:

\[
\mathbb{E}[R_p] = w^T \mu
\]

\[
\sigma_p^2 = w^T \Sigma w
\]

**Constructing the Efficient Frontier:**
- The efficient frontier is obtained by solving the following optimization problem for different levels of expected return:

\[
\min_w \, w^T \Sigma w
\]

\[
\text{subject to} \, \mathbb{E}[R_p] = w^T \mu, \, \sum_{i=1}^n w_i = 1, \, w_i \geq 0 \, \text{for all } i
\]

**Python Example: Constructing the Efficient Frontier**

```python
import numpy as np
import matplotlib.pyplot as plt

# Sample returns and covariance matrix
returns = np.array([0.12, 0.18, 0.15])
cov_matrix = np.array([[0.005, -0.010, 0.004],
                       [-0.010, 0.040, -0.002],
                       [0.004, -0.002, 0.023]])

# Number of portfolios to simulate
num_portfolios = 10000

# Arrays to store results
results = np.zeros((3, num_portfolios))

for i in range(num_portfolios):
    weights = np.random.random(3)
    weights /= np.sum(weights)
    
    portfolio_return = np.sum(weights * returns)
    portfolio_stddev = np.sqrt(np.dot(weights.T, np.dot(cov_matrix, weights)))
    
    results[0,i] = portfolio_return
    results[1,i] = portfolio_stddev
    results[2,i] = results[0,i] / results[1,i]

# Plotting the efficient frontier
plt.scatter(results[1,:], results[0,:], c=results[2,:], cmap='YlGnBu')
plt.xlabel('Risk (Standard Deviation)')
plt.ylabel('Return')
plt.title('Efficient Frontier')
plt.colorbar(label='Sharpe Ratio')
plt.show()
```

**Practical Application: Identifying Optimal Portfolios on the Efficient Frontier**
- Optimal portfolios are typically selected based on the highest Sharpe ratio \( \text{Sharpe} = \frac{\mathbb{E}[R_p] - R_f}{\sigma_p} \), where \( R_f \) is the risk-free rate. The portfolio with the highest Sharpe ratio lies at the tangent point between the efficient frontier and the Capital Market Line (CML).

#### **Markowitz Model**

**In-Depth Study of the Markowitz Model:**
- Markowitz’s mean-variance optimization model focuses on creating a portfolio that maximizes expected return for a given level of risk, or minimizes risk for a given level of return.

**Mathematical Formulation:**
- The optimization problem is as follows:

\[
\max_w \, \frac{w^T \mu - R_f}{\sqrt{w^T \Sigma w}}
\]

**Portfolio Diversification Strategies Based on the Markowitz Model:**
- Diversification reduces the portfolio's overall risk by investing in assets that are not perfectly correlated. The goal is to minimize the portfolio’s variance while achieving a desired return.

**Mathematical Justification for Diversification:**
- The portfolio variance is given by:

\[
\sigma_p^2 = \sum_{i=1}^n \sum_{j=1}^n w_i w_j \sigma_{ij}
\]

Where \( \sigma_{ij} \) is the covariance between the returns of assets \( i \) and \( j \). Diversification works because the off-diagonal elements (covariances) tend to reduce overall portfolio variance when assets are not perfectly correlated (\( \rho_{ij} < 1 \)).

**Case Studies: Real-World Application of the Markowitz Model in Portfolio Construction**
- These could involve examining how diversified portfolios have performed historically, focusing on periods of market stress and recovery, and demonstrating the benefits of diversification in reducing drawdowns and enhancing long-term returns.

#### **Capital Market Line (CML)**

**Understanding the Capital Market Line:**
- The CML represents portfolios that optimally combine a risk-free asset with the market portfolio. It is a graphical representation of the risk-return trade-off for these portfolios.

**Mathematical Expression of the CML:**
- The CML is given by the equation:

\[
\mathbb{E}[R_p] = R_f + \frac{\mathbb{E}[R_m] - R_f}{\sigma_m} \sigma_p
\]

Where \( \mathbb{E}[R_m] \) is the expected return of the market portfolio, \( \sigma_m \) is the standard deviation of the market portfolio, and \( \sigma_p \) is the standard deviation of the portfolio.

**Python Example: Constructing the Optimal Risky Portfolio**

```python
import numpy as np
import matplotlib.pyplot as plt

# Sample data for two risky assets and a risk-free asset
rf = 0.03  # Risk-free rate
returns = np.array([0.12, 0.18])
cov_matrix = np.array([[0.005, -0.010],
                       [-0.010, 0.040]])

# Finding the tangency portfolio (maximum Sharpe ratio)
def portfolio_performance(weights, returns, cov_matrix):
    portfolio_return = np.sum(weights * returns)
    portfolio_stddev = np.sqrt(np.dot(weights.T, np.dot(cov_matrix, weights)))
    sharpe_ratio = (portfolio_return - rf) / portfolio_stddev
    return portfolio_return, portfolio_stddev, sharpe_ratio

from scipy.optimize import minimize

def neg_sharpe_ratio(weights, returns, cov_matrix, rf):
    p_return, p_stddev, p_sharpe = portfolio_performance(weights, returns, cov_matrix)
    return -p_sharpe

constraints = ({'type': 'eq', 'fun': lambda weights: np.sum(weights) - 1})
bounds = tuple((0, 1) for asset in range(returns.shape[0]))
result = minimize(neg_sharpe_ratio, len(returns) * [1. / len(returns)], args=(returns, cov_matrix, rf), method='SLSQP', bounds=bounds, constraints=constraints)

optimal_weights = result.x
optimal_return, optimal_stddev, optimal_sharpe = portfolio_performance(optimal_weights, returns, cov_matrix)

# Plotting CML
x = np.linspace(0, 0.3, 100)
cml = rf + (optimal_sharpe * x)
plt.plot(x, cml, label='CML', color='green')
plt.scatter(optimal_stddev, optimal_return, color='red', marker='*', s=100, label='Optimal Risky Portfolio')
plt.xlabel('Risk (Standard Deviation)')
plt.ylabel('Return')
plt.legend()
plt.show()
```

### **Alternative Investments**

#### **Hedge Funds**

**Overview of Hedge Funds:**
- Hedge funds are private investment vehicles that use a variety of strategies to achieve high returns. They are known for employing leverage, short selling, derivatives, and other complex instruments.

**Strategies Employed by Hedge Funds:**
- **Long/Short Equity:** Involves taking long positions in undervalued stocks and short positions in overvalued stocks to exploit pricing inefficiencies.
- **Market Neutral:** Focuses on achieving returns independent of market movements by balancing long and short positions to neutralize market risk.
- **Event-Driven:** Strategies based on exploiting opportunities from corporate events like mergers, acquisitions, bankruptcies, etc.

**Risk and Return Characteristics of Hedge Funds:**
- Hedge funds typically aim for absolute returns, meaning they seek to make profits regardless of market conditions. However, these strategies can also introduce significant risk due to leverage and complex instruments.

**Mathematical Risk-Return Measures for Hedge Funds:**
- **Sharpe Ratio:** A common measure of risk-adjusted return:

\[
\text{Sharpe Ratio} = \frac{\mathbb{E}[R_{hf}] - R_f}{\sigma_{hf}}
\]

Where \( \mathbb{E}[R_{hf}] \) is the expected return of the hedge fund, \( R_f \) is the risk-free rate, and \( \sigma_{hf} \) is the standard deviation of the hedge fund's returns.

#### **Private Equity**

**Introduction to Private Equity:**
- Private equity involves investments in private companies

 or public companies that are taken private. It includes venture capital, growth capital, and buyouts.

**Stages of Private Equity Investment:**
- **Venture Capital:** Early-stage investment in startups with high growth potential.
- **Growth Capital:** Investment in more mature companies seeking capital for expansion.
- **Buyouts:** Acquisition of a company, often using significant leverage (leveraged buyouts).

**Valuation Methods and Risk Management:**
- **DCF Valuation:** Private equity investments are often valued using Discounted Cash Flow (DCF) analysis, which estimates the present value of expected future cash flows.
- **Risk Management:** Involves assessing the risks of the underlying business, market conditions, and exit strategies.

#### **Commodities**

**Role of Commodities in Portfolio Diversification:**
- Commodities like gold, oil, and agricultural products can provide diversification benefits due to their low or negative correlation with traditional asset classes like stocks and bonds.

**Risk-Return Profile of Commodity Investments:**
- Commodities can exhibit high volatility but offer protection against inflation and geopolitical risks. The Sharpe ratio and Sortino ratio are often used to assess their risk-adjusted returns.

#### **Real Estate**

**Real Estate as a Component of a Diversified Portfolio:**
- Real estate investments can include direct property ownership or indirect investments through Real Estate Investment Trusts (REITs). These investments provide income through rent and capital appreciation.

**Valuation Methods for Real Estate Investments:**
- **Cap Rate:** The capitalization rate, which is the ratio of Net Operating Income (NOI) to property value, is a key metric for valuing income-generating real estate.
  
\[
\text{Cap Rate} = \frac{\text{NOI}}{\text{Property Value}}
\]

### **Behavioral Finance**

#### **Investor Psychology**

**Overview of Key Psychological Factors:**
- Behavioral finance studies how psychological factors and cognitive biases affect investment decisions, often leading to irrational behavior and market inefficiencies.

**Understanding Cognitive Biases:**
- **Overconfidence:** Investors may overestimate their ability to predict market movements, leading to excessive trading and risk-taking.
- **Anchoring:** Investors may rely too heavily on initial information (e.g., a stock's past price) when making decisions.
- **Herd Behavior:** Investors may follow the crowd rather than relying on their analysis, which can exacerbate market trends and contribute to bubbles and crashes.

#### **Market Anomalies**

**Exploration of Market Anomalies:**
- Market anomalies challenge the Efficient Market Hypothesis (EMH) and suggest that markets are not always perfectly efficient.

**Common Market Anomalies:**
- **Calendar Effects:** Phenomena like the January effect, where stocks tend to perform better in January.
- **Momentum:** The tendency for assets to continue performing in line with their recent trends.
- **Value Premium:** The tendency for stocks with lower price-to-earnings ratios to outperform those with higher ratios over the long term.

**Python Example: Analyzing Market Anomalies**

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load historical stock data
data = pd.read_csv('stock_data.csv')

# Calculate monthly returns
data['Return'] = data['Close'].pct_change()

# Calculate average monthly returns by month
monthly_returns = data.groupby(data['Date'].dt.month)['Return'].mean()

# Plotting the results
monthly_returns.plot(kind='bar', color='skyblue')
plt.title('Average Monthly Returns')
plt.xlabel('Month')
plt.ylabel('Average Return')
plt.show()
```

#### **Overconfidence**

**Impact of Overconfidence on Investor Decision-Making:**
- Overconfident investors are prone to excessive trading, underestimating risks, and poor diversification, which can lead to lower returns and higher transaction costs.

**Strategies to Mitigate Overconfidence:**
- **Diversification:** Helps reduce the impact of overconfidence by spreading risk across different assets.
- **Pre-Commitment:** Setting predefined rules or strategies, such as automatic rebalancing, can limit impulsive and overconfident decision-making.

#### **Loss Aversion**

**Understanding Loss Aversion:**
- Loss aversion, a key concept in behavioral finance, suggests that investors experience losses more intensely than gains. This can lead to irrational behavior, such as holding onto losing investments for too long or selling winners prematurely.

**Behavioral Finance Models Incorporating Loss Aversion:**
- **Prospect Theory:** Developed by Kahneman and Tversky, this theory models how people decide between probabilistic alternatives that involve risk, where the probabilities of outcomes are known.

\[
\text{Value Function: } V(x) = \begin{cases} 
(x - \lambda x^{\alpha}) & \text{if } x \geq 0 \\
-\lambda (-x)^{\beta} & \text{if } x < 0 
\end{cases}
\]

Where \( x \) is the gain or loss, \( \alpha \) and \( \beta \) are parameters that shape the curvature of the value function, and \( \lambda \) represents the degree of loss aversion.

### **Dynamic Portfolio Strategies**

#### **Black-Litterman Model**

**Introduction to the Black-Litterman Model:**
- The Black-Litterman model blends market equilibrium with investor views to provide a more stable and intuitive asset allocation. It improves on the Markowitz model by incorporating subjective views and mitigating the estimation errors often encountered in traditional mean-variance optimization.

**Mathematical Formulation:**
- Let \( \pi \) be the equilibrium excess returns, \( P \) the matrix representing the investor's views, \( Q \) the vector of expected returns from these views, and \( \Omega \) the uncertainty in the views. The Black-Litterman formula for the posterior expected returns \( \mu^* \) is:

\[
\mu^* = \left( (\tau \Sigma)^{-1} + P^T \Omega^{-1} P \right)^{-1} \left( (\tau \Sigma)^{-1} \pi + P^T \Omega^{-1} Q \right)
\]

Where \( \tau \) is a scalar representing the uncertainty in the equilibrium returns, and \( \Sigma \) is the covariance matrix of returns.

**Python Example: Constructing Portfolios Using the Black-Litterman Approach**

```python
import numpy as np
import matplotlib.pyplot as plt

# Market equilibrium returns
pi = np.array([0.05, 0.07, 0.10])

# Investor views
P = np.array([[1, -1, 0], [0, 1, -1]])
Q = np.array([0.02, 0.01])

# Uncertainty in views
Omega = np.diag([0.0004, 0.0001])

# Calculate posterior returns
tau = 0.05
Sigma = np.array([[0.001, 0.0002, 0.0001],
                  [0.0002, 0.0025, 0.0004],
                  [0.0001, 0.0004, 0.003]])

M_inverse = np.linalg.inv(np.linalg.inv(tau * Sigma) + P.T @ np.linalg.inv(Omega) @ P)
posterior_return = M_inverse @ (np.linalg.inv(tau * Sigma) @ pi + P.T @ np.linalg.inv(Omega) @ Q)

print("Posterior Expected Returns:", posterior_return)
```

#### **Bayesian Approaches**

**Overview of Bayesian Methods in Portfolio Management:**
- Bayesian approaches update the probabilities of different investment outcomes based on new information. This method is dynamic, allowing portfolios to adapt as market conditions change.

**Updating Portfolio Allocations:**
- Bayesian inference involves updating prior beliefs (prior distribution) with new evidence (likelihood) to obtain a posterior distribution, which can be used to adjust portfolio allocations.

**Mathematical Expression:**
- Bayes' Theorem in portfolio context is expressed as:

\[
P(\theta | X) = \frac{P(X | \theta) \cdot P(\theta)}{P(X)}
\]

Where \( P(\theta | X) \) is the posterior probability, \( P(X | \theta) \) is the likelihood, \( P(\theta) \) is the prior probability, and \( P(X) \) is the marginal likelihood.

#### **Multiperiod Portfolio Optimization**

**Introduction to Multiperiod Portfolio Optimization:**
- Multiperiod optimization considers the portfolio decisions across multiple time periods, accounting for changes in investment opportunities and the evolving preferences of investors.

**Dynamic Strategies for Asset Allocation:**
- These strategies involve periodically rebalancing the portfolio, considering transaction costs and changing market conditions.

**Mathematical Formulation:**
- The dynamic optimization problem can be expressed as a Bellman equation:

\[
V_t(W_t) = \max_{w_t} \left\{ U(w_t^T \mu_t) + \beta \mathbb{E}[V_{t+1}(W_{t+1}) | W_t, w_t] \right\}
\]

Where \( V_t(W_t) \) is the value function at time \( t \), \( W_t \) is the wealth at time \( t \), \( U(\cdot) \) is the utility function, and \( \beta \) is the discount factor.

**Python Example: Managing Portfolios with a Long-Term Investment Horizon**

```python
import numpy as np

# Simulate long-term investment horizon
num_years = 10
initial_wealth = 100000
annual_returns = np.random.normal(0.07, 0.15, num_years)

wealth = [initial_wealth]

for r in annual_returns:
    wealth

.append(wealth[-1] * (1 + r))

plt.plot(range(num_years + 1), wealth, marker='o')
plt.xlabel('Year')
plt.ylabel('Wealth')
plt.title('Portfolio Value Over Time')
plt.show()
```
