# Lecture Notes: Stochastic Calculus and Financial Derivatives

## Introduction
This document provides an in-depth exploration of stochastic calculus and its applications in financial derivatives. We will cover the theoretical foundations such as **Brownian motion**, **stochastic differential equations (SDEs)**, and their application in various option pricing models like the **Black-Scholes model**. The aim is to provide a solid understanding of these mathematical concepts and how they are applied in the financial industry, especially in **option pricing**, **risk management**, and **hedging strategies**.

## Brownian Motion
Brownian motion is a central concept in stochastic processes, often used to model the random movement of particles. In finance, it represents the unpredictable fluctuations in stock prices, interest rates, or other financial variables over time.

### Properties of Brownian Motion
Brownian motion ( B_t ) is a stochastic process with the following properties:

- **Martingale Property:** Brownian motion is a martingale, meaning the expected future value of the process is equal to its current value, given all the information up to now. This reflects that there's no "drift" or trend in Brownian motion — future movements are entirely random. In finance, this implies that stock prices do not have a predictable trend but are instead subject to random fluctuations:

  $\mathbb{E}[B_{t+s} \mid \mathcal{F}_t] = B_t$

  where ( \mathcal{F}_t ) represents the set of all information available up to time ( t ).

- **Markov Property:** The Markov property states that Brownian motion has no memory. Its future values depend only on its current position, not on the path it took to get there. This means that past price movements don't directly influence future movements, simplifying the modeling of financial markets:

  $\mathbb{P}(B_{t+s} \in A \mid \mathcal{F}_t) = \mathbb{P}(B_{t+s} \in A \mid B_t)$

  where ( A ) is any event at a future time.

- **Path Behavior:** The paths of Brownian motion are continuous, but they are extremely "rough" and nowhere differentiable. In other words, while there are no sudden jumps, the motion is highly erratic at every moment. This reflects how asset prices can change very rapidly, even in small time intervals, making it a suitable model for capturing the erratic nature of financial markets.

```bash
// Class definition for Brownian Motion
class BrownianMotion:
    // Constructor to initialize Brownian motion parameters
    function __init__(self, B0, T, dt):
        self.B0 = B0  // Initial value of Brownian motion
        self.T = T  // Total time
        self.dt = dt  // Time step size
        self.N = T / dt  // Number of steps
        self.path = array of size N + 1  // Initialize array for path
        self.path[0] = B0  // Set initial value

    // Method to generate a sample path of Brownian motion
    function generatePath():
        for i from 1 to N:
            // Generate random increment from standard normal distribution
            increment = generateStandardNormal() * sqrt(dt)
            self.path[i] = self.path[i - 1] + increment  // Update the path

    // Method to check Martingale property
    function checkMartingaleExpectation(t, s):
        // Calculate expected future value at time t + s
        expected_future_value = self.path[t]  // Martingale property: E[B_{t+s} | F_t] = B_t
        return expected_future_value

    // Method to check Markov property
    function checkMarkovProperty(t, s, event):
        // Determine if future value depends only on current value
        current_value = self.path[t]  // Current value of Brownian motion
        // Check probability of future event given current value
        future_event_probability = computeProbability(event, current_value)
        return future_event_probability

    // Method to describe path behavior
    function describePathBehavior():
        // Analyze the continuity and roughness of the path
        for i from 1 to N:
            if abs(self.path[i] - self.path[i - 1]) < epsilon:  // Check for continuity
                // Path is continuous
                print("Path is continuous at step:", i)
            // Discuss the roughness (high variability) of the path
            // This part is conceptual and may not be represented by code

// Main execution
initial_B0 = initial value of Brownian motion
total_time = total simulation time (T)
time_step_size = size of time steps (dt)

// Create an instance of Brownian motion
bm = BrownianMotion(initial_B0, total_time, time_step_size)

// Generate a sample path of Brownian motion
bm.generatePath()

// Check the Martingale property at time t and future time t+s
t = current time
s = future time increment
martingale_value = bm.checkMartingaleExpectation(t, s)
print("Expected future value (Martingale):", martingale_value)

// Check the Markov property for an event A
event = define an event for future time
markov_probability = bm.checkMarkovProperty(t, s, event)
print("Probability of future event given current value (Markov):", markov_probability)

// Describe the path behavior of Brownian motion
bm.describePathBehavior()
```

### Geometric Brownian Motion
Geometric Brownian Motion (GBM) is used extensively in financial modeling, particularly for modeling stock prices. GBM incorporates two components:

1. **Drift:** The expected return of the stock.
2. **Volatility:** The randomness or uncertainty of returns.

GBM is described by the following stochastic differential equation (SDE):

  $dS_t = \mu S_t \, dt + \sigma S_t \, dB_t$

where:

- ( S_t ) is the stock price at time ( t ),
- ( \mu ) is the drift rate (expected return),
- ( \sigma ) is the volatility (a measure of risk or uncertainty),
- ( dB_t ) is an increment of Brownian motion, representing random changes.

The solution to this equation is:

$S_t = S_0 \exp\left((\mu - \frac{\sigma^2}{2})t + \sigma B_t\right)$

This shows that the stock price ( S_t ) follows a log-normal distribution, which matches observed behavior in financial markets, where stock prices can't be negative and exhibit exponential growth patterns.

```bash
// Function to generate increments of Brownian motion
function generateBrownianIncrements(T, dt):
    N = T / dt  // Number of time steps
    dB = array of size N  // Initialize array for Brownian increments
    for i from 1 to N:
        dB[i] = generateStandardNormal() * sqrt(dt)  // Generate standard normal increment
    return dB  // Return the array of increments

// Function to simulate Geometric Brownian Motion
function simulateGBM(S0, mu, sigma, T, dt):
    N = T / dt  // Number of time steps
    S = array of size N + 1  // Initialize array to hold stock prices
    S[0] = S0  // Set initial stock price

    // Generate increments of Brownian motion
    dB = generateBrownianIncrements(T, dt)

    // Iterate over each time step
    for i from 1 to N:
        // Calculate stock price at next time step
        S[i] = S[i-1] * exp((mu - 0.5 * sigma^2) * dt + sigma * dB[i-1])

    return S  // Return the simulated stock prices

// Main execution
initial_S = initial stock price (S0)
mu = expected return (drift)
sigma = volatility (risk)
T = total time period for simulation
dt = time step size

// Simulate the Geometric Brownian Motion for stock prices
simulated_prices = simulateGBM(initial_S, mu, sigma, T, dt)
```

## Stochastic Differential Equations (SDEs)
SDEs describe the evolution of a system affected by random shocks, such as the price of a financial asset influenced by market fluctuations. They are crucial in finance for modeling how asset prices evolve over time in a stochastic (random) environment.

### Ito’s Lemma
Ito's Lemma is a fundamental result in stochastic calculus that allows us to determine how a function of a stochastic process changes over time. For instance, if we know how a stock price evolves, Ito's Lemma helps us find how the value of an option on that stock evolves.

Suppose ( X_t ) follows an SDE like this:

  $dX_t = \mu(X_t, t) \, dt + \sigma(X_t, t) \, dB_t$

where ( \mu(X_t, t) ) is the drift term (expected change) and ( \sigma(X_t, t) ) is the diffusion term (random shock). For a function ( f(X_t, t) ), Ito's Lemma gives:

  $df(X_t, t) = \frac{\partial f}{\partial t} \, dt + \frac{\partial f}{\partial X_t} \, dX_t + \frac{1}{2} \frac{\partial^2 f}{\partial X_t^2} \, \sigma^2(X_t, t) \, dt$

Ito’s Lemma adjusts for both the deterministic drift and the random fluctuations in the system, enabling us to understand how complex financial instruments, like options, will evolve over time.

```bash
// Function to calculate the change in the function using Ito's Lemma
function applyItosLemma(X_t, t, mu, sigma, dt):
    // Compute partial derivatives
    df_dt = partialDerivative(f, X_t, t)  // df/dt
    df_dX = partialDerivative(f, X_t, t)   // df/dX
    df_dX2 = secondPartialDerivative(f, X_t, t)  // d^2f/dX^2

    // Calculate dX_t (stochastic process)
    dX_t = mu(X_t, t) * dt + sigma(X_t, t) * dB_t  // dB_t: increment of Brownian motion

    // Calculate df(X_t, t) using Ito's Lemma
    df = df_dt * dt + df_dX * dX_t + 0.5 * df_dX2 * (sigma(X_t, t)^2) * dt

    return df  // Return the change in f(X_t, t)

// Function to simulate the stochastic process and apply Ito's Lemma
function simulateProcess(initial_X, initial_t, mu, sigma, T, dt):
    // Parameters
    N = T / dt  // Number of time steps
    X = array of size N + 1  // Initialize array to hold values of X
    X[0] = initial_X  // Set initial value of X

    // Iterate over each time step
    for i from 1 to N:
        // Calculate increment of Brownian motion dB_t
        dB_t = generateStandardNormal() * sqrt(dt)  // Standard normal increment
        // Update time
        current_t = initial_t + i * dt
        // Apply Ito's Lemma
        df = applyItosLemma(X[i-1], current_t, mu, sigma, dt)
        // Update value of X
        X[i] = X[i-1] + df

    return X  // Return the simulated process values

// Main execution
initial_X = initial value of the stochastic process
initial_t = initial time
T = total time period for simulation
dt = time step size
mu = function for drift term
sigma = function for diffusion term

// Simulate the stochastic process
simulated_values = simulateProcess(initial_X, initial_t, mu, sigma, T, dt)
```

### Girsanov’s Theorem
Girsanov’s Theorem is a key result that allows us to change from the real-world probability measure (where we model actual stock returns) to the **risk-neutral measure** (used in pricing derivatives). This change of measure simplifies the problem by removing the drift term, leaving only the volatility. 

In practice, this theorem tells us how to modify the Brownian motion under one probability measure to obtain a Brownian motion under a different probability measure. This is crucial for determining the "fair price" of financial derivatives, as it allows us to price them using the risk-neutral measure where all the drift terms are accounted for in the discounting.

```bash
// Function to simulate stock prices under the real-world measure
function simulateStockPrices(S0, mu, sigma, T, dt, n):
    // Parameters
    N = T / dt  // Number of time steps
    S = array of size N + 1  // Initialize array to hold stock prices
    S[0] = S0  // Set initial stock price

    for i from 1 to N:
        // Generate a standard normal random variable Z
        Z = generateStandardNormal()  
        
        // Calculate stock price at next time step using real-world drift mu
        S[i] = S[i-1] * exp((mu - (sigma^2) / 2) * dt + sigma * sqrt(dt) * Z)

    return S  // Return simulated stock price path

// Function to simulate stock prices under the risk-neutral measure
function simulateRiskNeutralStockPrices(S0, r, sigma, T, dt, n):
    // Parameters
    N = T / dt  // Number of time steps
    S = array of size N + 1  // Initialize array to hold stock prices
    S[0] = S0  // Set initial stock price

    for i from 1 to N:
        // Generate a standard normal random variable Z
        Z = generateStandardNormal()  
        
        // Calculate stock price at next time step using risk-free rate r
        S[i] = S[i-1] * exp((r - (sigma^2) / 2) * dt + sigma * sqrt(dt) * Z)

    return S  // Return simulated stock price path

// Main execution
S0 = initial stock price
mu = drift of stock in real-world measure
r = risk-free interest rate
sigma = volatility of stock
T = time horizon
dt = time step size
n = number of simulations

// Simulate stock prices under real-world measure
realWorldPrices = simulateStockPrices(S0, mu, sigma, T, dt, n)

// Simulate stock prices under risk-neutral measure
riskNeutralPrices = simulateRiskNeutralStockPrices(S0, r, sigma, T, dt, n)
```

## Option Pricing Models
Option pricing models are mathematical models used to determine the fair value of options based on the price dynamics of the underlying asset. The **Black-Scholes model** is one of the most famous and widely used models in this field.

### Black-Scholes Model
The Black-Scholes Model provides a formula to price European-style options (which can only be exercised at expiration). It assumes that the stock price follows a Geometric Brownian Motion, and uses this to derive a partial differential equation (PDE) that the option price must satisfy:

  $\frac{\partial C}{\partial t} + rS \frac{\partial C}{\partial S} + \frac{1}{2} \sigma^2 S^2 \frac{\partial^2 C}{\partial S^2} = rC$

where ( C(S,t) ) is the price of the option, ( S ) is the stock price, ( r ) is the risk-free interest rate, and ( \sigma ) is the stock's volatility. This PDE reflects how the option's price changes over time, with contributions from the underlying asset's price movement, volatility, and time decay.

The solution for a European call option (the right to buy) is given by the Black-Scholes formula:

  $C = S_0 \cdot N(d_1) - K e^{-rT} \cdot N(d_2)$

where:

  $d_1 = \frac{\ln(S_0 / K) + (r + \sigma^2 / 2) T}{\sigma \sqrt{T}}, \quad d_2 = d_1 - \sigma \sqrt{T}$

Here, ( N(d) ) is the cumulative distribution function of the standard normal distribution, ( S_0 ) is the current stock price, ( K ) is the strike price, and ( T ) is the time to maturity. This formula provides the theoretical price of the option based on current market conditions.

```bash
// Function to calculate the cumulative distribution function (CDF) of standard normal distribution
function N(d):
    return 0.5 * (1 + ErrorFunction(d / sqrt(2)))  // ErrorFunction calculates the error function

// Function to calculate the Black-Scholes price of a European call option
function BlackScholesCallOptionPrice(S0, K, T, r, sigma):
    // Step 1: Calculate d1 and d2
    d1 = (ln(S0 / K) + (r + (sigma^2) / 2) * T) / (sigma * sqrt(T))
    d2 = d1 - sigma * sqrt(T)

    // Step 2: Calculate the option price using the Black-Scholes formula
    C = S0 * N(d1) - K * exp(-r * T) * N(d2)

    return C  // Return the calculated call option price
```

### The Greeks

The **Greeks** are key metrics used to understand how the price of an option will change in response to different variables. They help traders and risk managers assess the sensitivity of an option’s price to changes in the underlying asset, volatility, interest rates, and time.

- **Delta (( \Delta )):** Measures the sensitivity of the option price to changes in the underlying asset price. A Delta of 0.5 means that for every$1 change in the asset price, the option's price will change by$0.50. Delta helps in understanding the directional risk of an option.

- **Gamma (( \Gamma )):** Measures how fast Delta changes with respect to the underlying asset price. A high Gamma means that Delta is very sensitive to changes in the asset price, indicating more risk in hedging the position. Gamma provides insights into the convexity of the option's price curve.

- **Vega:** Measures how sensitive the option price is to changes in the volatility of the underlying asset. Higher Vega means that the option's price is more sensitive to changes in volatility, making it crucial for understanding how volatility impacts option pricing.

- **Theta (( \Theta )):** Represents the time decay of the option, meaning how much the option's price decreases as time passes, all else being equal. As expiration approaches, Theta typically becomes more negative for options, indicating that options lose value over time if other factors remain constant.

- **Rho (( \rho )):** Measures the sensitivity of the option price to changes in the risk-free interest rate. Rho is important for long-dated options, where changes in interest rates can have a more significant impact on the option's value.

## Conclusion
Understanding stochastic calculus and its application in finance is crucial for pricing derivatives, managing risk, and making informed trading decisions. The concepts covered in this document — from Brownian motion to the Black-Scholes model and the Greeks — provide a comprehensive framework for analyzing and understanding financial derivatives. Mastery of these concepts enables better decision-making and risk management in the financial markets.
