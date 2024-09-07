# Lecture Notes: Stochastic Calculus and Financial Derivatives

## Introduction

This document provides an in-depth exploration of stochastic calculus and its applications in financial derivatives. We will cover the theoretical foundations such as Brownian motion, stochastic differential equations (SDEs), and their application in various option pricing models. The aim is to provide a solid understanding of the concepts and how they are applied in the financial industry.

## Brownian Motion

Brownian motion is a central concept in stochastic processes, serving as a mathematical model for the random motion observed in particles suspended in fluid, and more broadly, as a model for various types of random behavior in financial markets.

### Properties of Brownian Motion

Brownian motion \( B_t \) is a stochastic process with the following properties:

- **Martingale Property:** Brownian motion is a martingale, meaning the expected future value of the process is equal to its current value, given the present information:
  $  \mathbb{E}[B_{t+s} \mid \mathcal{F}_t] = B_t
$
  Here, \( \mathcal{F}_t \) represents the information available up to time \( t \).

- **Markov Property:** The process \( B_t \) has no memory, meaning its future evolution depends only on its current state and not on how it arrived there:
  $  \mathbb{P}(B_{t+s} \in A \mid \mathcal{F}_t) = \mathbb{P}(B_{t+s} \in A \mid B_t)
$
  where \( A \) is any event in the future.

- **Path Behavior:** The paths of Brownian motion are continuous, but they are nowhere differentiable. This implies that while the motion is smooth in the sense that there are no jumps, it is also highly irregular:
  $  \lim_{h \to 0} \frac{B_{t+h} - B_t}{h} \text{ does not exist.}
$

### Geometric Brownian Motion

Geometric Brownian Motion (GBM) is used extensively in financial modeling, particularly for modeling stock prices. It is given by the stochastic differential equation (SDE):

$dS_t = \mu S_t \, dt + \sigma S_t \, dB_t$

where:
- \( S_t \) is the price of the stock at time \( t \),
- \( \mu \) is the drift rate, representing the expected return of the stock,
- \( \sigma \) is the volatility, representing the standard deviation of the stock's returns,
- \( dB_t \) is the increment of a Brownian motion.

The solution to this SDE, using Ito's Lemma, is:

$S_t = S_0 \exp\left((\mu - \frac{\sigma^2}{2})t + \sigma B_t\right)$

This shows that the stock price \( S_t \) follows a log-normal distribution, which is consistent with observed market behavior.

## Stochastic Differential Equations (SDEs)

SDEs are equations that describe the evolution of a system subject to random shocks, such as the price of a financial asset influenced by random market movements.

### Ito’s Lemma

Ito's Lemma is a key result in stochastic calculus, allowing us to determine the differential of a function of a stochastic process. Suppose \( X_t \) is a stochastic process that follows:

$dX_t = \mu(X_t, t) \, dt + \sigma(X_t, t) \, dB_t$

where \( \mu(X_t, t) \) is the drift term and \( \sigma(X_t, t) \) is the diffusion term. For a twice continuously differentiable function \( f(X_t, t) \), Ito's Lemma gives:

$df(X_t, t) = \frac{\partial f}{\partial t} \, dt + \frac{\partial f}{\partial X_t} \, dX_t + \frac{1}{2} \frac{\partial^2 f}{\partial X_t^2} \, \sigma^2(X_t, t) \, dt$

Substituting the SDE for \( dX_t \):

$df(X_t, t) = \left(\frac{\partial f}{\partial t} + \mu(X_t, t) \frac{\partial f}{\partial X_t} + \frac{1}{2} \sigma^2(X_t, t) \frac{\partial^2 f}{\partial X_t^2}\right) dt + \sigma(X_t, t) \frac{\partial f}{\partial X_t} \, dB_t$

This lemma is crucial in deriving the Black-Scholes PDE and other results in finance.

### Girsanov’s Theorem

Girsanov’s Theorem is fundamental in changing the probability measure, which is essential in pricing derivatives under a risk-neutral measure. It states that if \( X_t \) is a Brownian motion under the original probability measure \( \mathbb{P} \), then under a new measure \( \mathbb{Q} \) defined by the Radon-Nikodym derivative:

$\frac{d\mathbb{Q}}{d\mathbb{P}} = \exp\left(-\int_0^t \theta_s \, dB_s - \frac{1}{2} \int_0^t \theta_s^2 \, ds\right)$

where \( \theta_t \) is a predictable process, the process:

$W_t = B_t + \int_0^t \theta_s \, ds$

is a Brownian motion under \( \mathbb{Q} \). This theorem allows us to move from the real-world probability measure to the risk-neutral measure, facilitating the pricing of financial derivatives.

## Option Pricing Models

Option pricing models, such as the Black-Scholes model, are designed to determine the fair value of options based on underlying asset dynamics.

### Black-Scholes Model

The Black-Scholes Model is one of the most important models in financial economics. It provides a theoretical estimate for the price of European-style options. The model assumes that the stock price follows a Geometric Brownian Motion:

$dS_t = \mu S_t \, dt + \sigma S_t \, dB_t$

By assuming a risk-neutral world (where the expected return on the stock is the risk-free rate \( r \)), and using Ito's Lemma, the Black-Scholes PDE is derived:

$\frac{\partial C}{\partial t} + rS \frac{\partial C}{\partial S} + \frac{1}{2} \sigma^2 S^2 \frac{\partial^2 C}{\partial S^2} = rC$

where \( C(S,t) \) is the price of the option. The solution to this PDE for a European call option is given by the Black-Scholes formula:

$C = S_0 \cdot N(d_1) - K e^{-rT} \cdot N(d_2)$

where:

$d_1 = \frac{\ln(S_0 / K) + (r + \sigma^2 / 2) T}{\sigma \sqrt{T}}, \quad d_2 = d_1 - \sigma \sqrt{T}$

Here, \( N(d) \) represents the cumulative distribution function of the standard normal distribution.

### The Greeks

The Greeks are derivatives of the option price with respect to various parameters. They provide insights into how the option's price will change with changes in underlying factors.

- **Delta (\( \Delta \)):** Measures the sensitivity of the option price to changes in the underlying asset price:
  
  $\Delta = \frac{\partial C}{\partial S}$
  
  Delta represents the rate of change of the option value with respect to the price of the underlying asset.

- **Gamma (\( \Gamma \)):** Measures the rate of change of Delta with respect to changes in the underlying asset price:
  
  $\Gamma = \frac{\partial^2 C}{\partial S^2}$
  
  Gamma provides information on the curvature of the option price as a function of the underlying asset price.

- **Vega:** Measures the sensitivity of the option price to changes in the volatility of the underlying asset:
  
  $\text{Vega} = \frac{\partial C}{\partial \sigma}$
  
  Vega indicates how much the option price will change as the volatility of the underlying asset changes.

- **Theta (\( \Theta \)):** Measures the sensitivity of the option price to the passage of time, also known as the time decay:
  
  $\Theta = \frac{\partial C}{\partial t}$
  
  Theta represents the rate at which the option loses value as time progresses.

- **Rho (\( \rho \)):** Measures the sensitivity of the option price to changes in the risk-free interest rate:
  
  $\rho = \frac{\partial C}{\partial r}$
  
  Rho indicates how much the option price will change in response to changes in the interest rate.

### Volatility Surface

The volatility surface represents the implied volatility of options across different strikes and maturities. It reflects market participants' expectations of future volatility and can exhibit patterns such as the volatility smile or skew.

- **Volatility Smile:** A pattern where implied volatility tends to be higher for options that are deep in or out of the money compared to at-the-money options.

- **Volatility Skew:** A phenomenon where implied volatility varies with the strike price, often observed in equity markets where out-of-the-money puts may have higher implied volatilities than at-the-money puts.

## Conclusion

Stochastic calculus provides a robust framework for modeling and understanding the randomness in financial markets. From Brownian motion to the Black-Scholes model and beyond, these tools and theories are crucial for pricing financial derivatives and managing risk.

## References

1. Black, F., & Scholes, M. (1973). The Pricing of Options and Corporate Liabilities. *Journal of Political Economy, 81*(3), 637-654.
2. Hull, J. (2017). *Options, Futures, and Other Derivatives* (10th ed.). Pearson.
3. Shreve, S. E. (2004). *Stochastic Calculus for Finance I: The Binomial Asset Pricing Model*. Springer.

For further reading and a deeper understanding of these concepts, refer to the textbooks and papers listed in the references.

