# Lecture Notes: Stochastic Calculus and Financial Derivatives

## Introduction
This document provides an in-depth exploration of stochastic calculus and its applications in financial derivatives. We will cover the theoretical foundations such as **Brownian motion**, **stochastic differential equations (SDEs)**, and their application in various option pricing models like the **Black-Scholes model**. The aim is to provide a solid understanding of these mathematical concepts and how they are applied in the financial industry, especially in **option pricing**, **risk management**, and **hedging strategies**.

## Brownian Motion
Brownian motion is a central concept in stochastic processes, often used to model the random movement of particles. In finance, it represents the unpredictable fluctuations in stock prices, interest rates, or other financial variables over time.

### Properties of Brownian Motion
Brownian motion \( B_t \) is a stochastic process with the following properties:

- **Martingale Property:** Brownian motion is a martingale, meaning the expected future value of the process is equal to its current value, given all the information up to now. This reflects that there's no "drift" or trend in Brownian motion — future movements are entirely random. In finance, this implies that stock prices do not have a predictable trend but are instead subject to random fluctuations:

  $  \mathbb{E}[B_{t+s} \mid \mathcal{F}_t] = B_t
$

  where \( \mathcal{F}_t \) represents the set of all information available up to time \( t \).

- **Markov Property:** The Markov property states that Brownian motion has no memory. Its future values depend only on its current position, not on the path it took to get there. This means that past price movements don't directly influence future movements, simplifying the modeling of financial markets:

  $  \mathbb{P}(B_{t+s} \in A \mid \mathcal{F}_t) = \mathbb{P}(B_{t+s} \in A \mid B_t)
$

  where \( A \) is any event at a future time.

- **Path Behavior:** The paths of Brownian motion are continuous, but they are extremely "rough" and nowhere differentiable. In other words, while there are no sudden jumps, the motion is highly erratic at every moment. This reflects how asset prices can change very rapidly, even in small time intervals, making it a suitable model for capturing the erratic nature of financial markets.

### Geometric Brownian Motion
Geometric Brownian Motion (GBM) is used extensively in financial modeling, particularly for modeling stock prices. GBM incorporates two components:

1. **Drift:** The expected return of the stock.
2. **Volatility:** The randomness or uncertainty of returns.

GBM is described by the following stochastic differential equation (SDE):

$dS_t = \mu S_t \, dt + \sigma S_t \, dB_t$

where:

- \( S_t \) is the stock price at time \( t \),
- \( \mu \) is the drift rate (expected return),
- \( \sigma \) is the volatility (a measure of risk or uncertainty),
- \( dB_t \) is an increment of Brownian motion, representing random changes.

The solution to this equation is:

$S_t = S_0 \exp\left((\mu - \frac{\sigma^2}{2})t + \sigma B_t\right)$

This shows that the stock price \( S_t \) follows a log-normal distribution, which matches observed behavior in financial markets, where stock prices can't be negative and exhibit exponential growth patterns.

## Stochastic Differential Equations (SDEs)
SDEs describe the evolution of a system affected by random shocks, such as the price of a financial asset influenced by market fluctuations. They are crucial in finance for modeling how asset prices evolve over time in a stochastic (random) environment.

### Ito’s Lemma
Ito's Lemma is a fundamental result in stochastic calculus that allows us to determine how a function of a stochastic process changes over time. For instance, if we know how a stock price evolves, Ito's Lemma helps us find how the value of an option on that stock evolves.

Suppose \( X_t \) follows an SDE like this:

$dX_t = \mu(X_t, t) \, dt + \sigma(X_t, t) \, dB_t$

where \( \mu(X_t, t) \) is the drift term (expected change) and \( \sigma(X_t, t) \) is the diffusion term (random shock). For a function \( f(X_t, t) \), Ito's Lemma gives:

$df(X_t, t) = \frac{\partial f}{\partial t} \, dt + \frac{\partial f}{\partial X_t} \, dX_t + \frac{1}{2} \frac{\partial^2 f}{\partial X_t^2} \, \sigma^2(X_t, t) \, dt$

Ito’s Lemma adjusts for both the deterministic drift and the random fluctuations in the system, enabling us to understand how complex financial instruments, like options, will evolve over time.

### Girsanov’s Theorem
Girsanov’s Theorem is a key result that allows us to change from the real-world probability measure (where we model actual stock returns) to the **risk-neutral measure** (used in pricing derivatives). This change of measure simplifies the problem by removing the drift term, leaving only the volatility. 

In practice, this theorem tells us how to modify the Brownian motion under one probability measure to obtain a Brownian motion under a different probability measure. This is crucial for determining the "fair price" of financial derivatives, as it allows us to price them using the risk-neutral measure where all the drift terms are accounted for in the discounting.

## Option Pricing Models
Option pricing models are mathematical models used to determine the fair value of options based on the price dynamics of the underlying asset. The **Black-Scholes model** is one of the most famous and widely used models in this field.

### Black-Scholes Model
The Black-Scholes Model provides a formula to price European-style options (which can only be exercised at expiration). It assumes that the stock price follows a Geometric Brownian Motion, and uses this to derive a partial differential equation (PDE) that the option price must satisfy:

$\frac{\partial C}{\partial t} + rS \frac{\partial C}{\partial S} + \frac{1}{2} \sigma^2 S^2 \frac{\partial^2 C}{\partial S^2} = rC$

where \( C(S,t) \) is the price of the option, \( S \) is the stock price, \( r \) is the risk-free interest rate, and \( \sigma \) is the stock's volatility. This PDE reflects how the option's price changes over time, with contributions from the underlying asset's price movement, volatility, and time decay.

The solution for a European call option (the right to buy) is given by the Black-Scholes formula:

$C = S_0 \cdot N(d_1) - K e^{-rT} \cdot N(d_2)$

where:

$d_1 = \frac{\ln(S_0 / K) + (r + \sigma^2 / 2) T}{\sigma \sqrt{T}}, \quad d_2 = d_1 - \sigma \sqrt{T}$

Here, \( N(d) \) is the cumulative distribution function of the standard normal distribution, \( S_0 \) is the current stock price, \( K \) is the strike price, and \( T \) is the time to maturity. This formula provides the theoretical price of the option based on current market conditions.

### The Greeks
The **Greeks** are key metrics used to understand how the price of an option will change in response to different variables. They help traders and risk managers assess the sensitivity of an option’s price to changes in the underlying asset, volatility, interest rates, and time.

- **Delta ( \( \Delta \)):** Measures the sensitivity of the option price to changes in the underlying asset price. A Delta of 0.5 means that for every $1 change in the asset price, the option's price will change by $0.50. Delta helps in understanding the directional risk of an option.

- **Gamma ( \( \Gamma \)):** Measures how fast Delta changes with respect to the underlying asset price. A high Gamma means that Delta is very sensitive to changes in the asset price, indicating more risk in hedging the position. Gamma provides insights into the convexity of the option's price curve.

- **Vega:** Measures how sensitive the option price is to changes in the volatility of the underlying asset. Higher Vega means that the option's price is more sensitive to changes in volatility, making it crucial for understanding how volatility impacts option pricing.

- **Theta ( \( \Theta \)):** Represents the time decay of the option, meaning how much the option's price decreases as time passes, all else being equal. As expiration approaches, Theta typically becomes more negative for options, indicating that options lose value over time if other factors remain constant.

- **Rho ( \( \rho \)):** Measures the sensitivity of the option price to changes in the risk-free interest rate. Rho is important for long-dated options, where changes in interest rates can have a more significant impact on the option's value.

## Conclusion
Understanding stochastic calculus and its application in finance is crucial for pricing derivatives, managing risk, and making informed trading decisions. The concepts covered in this document — from Brownian motion to the Black-Scholes model and the Greeks — provide a comprehensive framework for analyzing and understanding financial derivatives. Mastery of these concepts enables better decision-making and risk management in the financial markets.
