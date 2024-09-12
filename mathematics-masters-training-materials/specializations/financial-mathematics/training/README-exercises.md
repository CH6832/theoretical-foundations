### **1. Time Value of Money**

1. **Discrete Compounding Future Value**

   ```cpp
   #include <iostream>
   #include <cmath>

   double futureValue(double pv, double rate, int n, int t) {
       return pv * std::pow(1 + rate / n, n * t);
   }

   int main() {
       double pv = 1000.0;
       double rate = 0.05;
       int n = 12;
       int t = 10;

       double fv = futureValue(pv, rate, n, t);
       std::cout << "Future Value: " << fv << std::endl;
       return 0;
   }
   ```

2. **Continuous Compounding Future Value**

   ```cpp
   #include <iostream>
   #include <cmath>

   double futureValueContinuous(double pv, double rate, int t) {
       return pv * std::exp(rate * t);
   }

   int main() {
       double pv = 1000.0;
       double rate = 0.05;
       int t = 10;

       double fv = futureValueContinuous(pv, rate, t);
       std::cout << "Future Value (Continuous): " << fv << std::endl;
       return 0;
   }
   ```

3. **Present Value Calculation**

   ```cpp
   #include <iostream>
   #include <cmath>

   double presentValue(double fv, double rate, int n, int t) {
       return fv / std::pow(1 + rate / n, n * t);
   }

   int main() {
       double fv = 1000.0;
       double rate = 0.05;
       int n = 12;
       int t = 10;

       double pv = presentValue(fv, rate, n, t);
       std::cout << "Present Value: " << pv << std::endl;
       return 0;
   }
   ```

4. **Effective Annual Rate**

   ```cpp
   #include <iostream>
   #include <cmath>

   double effectiveAnnualRate(double nominalRate, int n) {
       return std::pow(1 + nominalRate / n, n) - 1;
   }

   int main() {
       double nominalRate = 0.05;
       int n = 12;

       double ear = effectiveAnnualRate(nominalRate, n);
       std::cout << "Effective Annual Rate: " << ear << std::endl;
       return 0;
   }
   ```

5. **Present Value of Annuity**

   ```cpp
   #include <iostream>
   #include <cmath>

   double presentValueAnnuity(double payment, double rate, int periods) {
       return payment * (1 - std::pow(1 + rate, -periods)) / rate;
   }

   int main() {
       double payment = 100.0;
       double rate = 0.05;
       int periods = 10;

       double pvAnnuity = presentValueAnnuity(payment, rate, periods);
       std::cout << "Present Value of Annuity: " << pvAnnuity << std::endl;
       return 0;
   }
   ```

6. **Present Value of Perpetuity**

   ```cpp
   #include <iostream>

   double presentValuePerpetuity(double payment, double rate) {
       return payment / rate;
   }

   int main() {
       double payment = 100.0;
       double rate = 0.05;

       double pvPerpetuity = presentValuePerpetuity(payment, rate);
       std::cout << "Present Value of Perpetuity: " << pvPerpetuity << std::endl;
       return 0;
   }
   ```

7. **Bond Pricing**

   ```cpp
   #include <iostream>
   #include <cmath>

   double bondPrice(double faceValue, double coupon, double rate, int periods) {
       double price = 0.0;
       for (int i = 1; i <= periods; ++i) {
           price += coupon / std::pow(1 + rate, i);
       }
       price += faceValue / std::pow(1 + rate, periods);
       return price;
   }

   int main() {
       double faceValue = 1000.0;
       double coupon = 50.0;
       double rate = 0.05;
       int periods = 10;

       double price = bondPrice(faceValue, coupon, rate, periods);
       std::cout << "Bond Price: " << price << std::endl;
       return 0;
   }
   ```

8. **Dividend Discount Model**

   ```cpp
   #include <iostream>

   double dividendDiscountModel(double dividend, double growthRate, double discountRate) {
       return dividend * (1 + growthRate) / (discountRate - growthRate);
   }

   int main() {
       double dividend = 5.0;
       double growthRate = 0.04;
       double discountRate = 0.08;

       double stockPrice = dividendDiscountModel(dividend, growthRate, discountRate);
       std::cout << "Stock Price: " << stockPrice << std::endl;
       return 0;
   }
   ```

### **2. Probability and Statistics in Finance**

9. **Normal Distribution Sample**

   ```cpp
   #include <iostream>
   #include <random>

   double normalDistribution(double mean, double stddev) {
       std::random_device rd;
       std::mt19937 gen(rd());
       std::normal_distribution<> d(mean, stddev);
       return d(gen);
   }

   int main() {
       double mean = 0.0;
       double stddev = 1.0;
       std::cout << "Random sample from normal distribution: " << normalDistribution(mean, stddev) << std::endl;
       return 0;
   }
   ```

10. **Mean Calculation**

    ```cpp
    #include <iostream>
    #include <vector>
    #include <numeric>

    double mean(const std::vector<double>& data) {
        return std::accumulate(data.begin(), data.end(), 0.0) / data.size();
    }

    int main() {
        std::vector<double> data = {1.0, 2.0, 3.0, 4.0, 5.0};
        std::cout << "Mean: " << mean(data) << std::endl;
        return 0;
    }
    ```

11. **Variance Calculation**

    ```cpp
    #include <iostream>
    #include <vector>
    #include <cmath>
    #include <numeric>

    double variance(const std::vector<double>& data, double mean) {
        double sum = 0.0;
        for (double x : data) {
            sum += (x - mean) * (x - mean);
        }
        return sum / data.size();
    }

    int main() {
        std::vector<double> data = {1.0, 2.0, 3.0, 4.0, 5.0};
        double mean_val = mean(data);
        double variance_val = variance(data, mean_val);
        std::cout << "Variance: " << variance_val << std::endl;
        return 0;
    }
    ```

12. **Linear Regression Slope**

    ```cpp
    #include <iostream>
    #include <vector>
    #include <numeric>

    double linearRegressionSlope(const std::vector<double>& x, const std::vector<double>& y) {
        double x_mean = std::accumulate(x.begin(), x.end(), 0.0) / x.size();
        double y_mean = std::accumulate(y.begin(), y.end(), 0.0) / y.size();
        double numerator = 0.0, denominator = 0.0;

        for (size_t i = 0; i < x.size(); ++i) {
            numerator += (x[i] - x_mean) * (y[i] - y_mean);
            denominator += (x[i] - x_mean) * (x[i] - x_mean);
        }
        return numerator / denominator;
    }

    int main() {
        std::vector<double> x = {1.0, 2.0, 3.0, 4.0};
        std::vector<double> y = {2.0, 2.8, 3.6, 4.4};

        double slope = linearRegressionSlope(x, y);
        std::cout << "Slope of Linear Regression: " << slope << std::endl;
        return 0;
    }
    ```

### **3. Stochastic Processes in Finance**

13. **Geometric Brownian Motion**

    ```cpp
    #include <iostream>
    #include <random>
    #include <cmath>

    double geometricBrownianMotion(double S0, double mu, double sigma, double dt) {
        std::random_device rd;
        std::mt19937 gen(rd());
        std::normal_distribution<> d(0, 1);
        return S0 * std::exp((mu - 0.5 * sigma * sigma) * dt + sigma * d(gen) * std::sqrt(dt));
    }

    int main() {
        double S0 = 100.0;
        double mu = 0.05;
        double sigma = 0.2;
        double dt = 1.0;

        double

 S1 = geometricBrownianMotion(S0, mu, sigma, dt);
        std::cout << "Stock Price after one time step: " << S1 << std::endl;
        return 0;
    }
    ```

14. **Simulate Stochastic Differential Equation**

    ```cpp
    #include <iostream>
    #include <random>
    #include <cmath>

    double simulateSDE(double X0, double mu, double sigma, double dt) {
        std::random_device rd;
        std::mt19937 gen(rd());
        std::normal_distribution<> d(0, 1);
        return X0 + mu * dt + sigma * std::sqrt(dt) * d(gen);
    }

    int main() {
        double X0 = 100.0;
        double mu = 0.01;
        double sigma = 0.02;
        double dt = 1.0;

        double X1 = simulateSDE(X0, mu, sigma, dt);
        std::cout << "Value after one time step: " << X1 << std::endl;
        return 0;
    }
    ```

15. **Monte Carlo Simulation for Option Pricing**

    ```cpp
    #include <iostream>
    #include <random>
    #include <cmath>

    double monteCarloOptionPrice(double S0, double K, double T, double r, double sigma, int numSimulations) {
        std::random_device rd;
        std::mt19937 gen(rd());
        std::normal_distribution<> d(0, 1);

        double sumPayoffs = 0.0;
        double dt = T / 365.0;

        for (int i = 0; i < numSimulations; ++i) {
            double S = S0;
            for (int t = 0; t < 365; ++t) {
                S *= std::exp((r - 0.5 * sigma * sigma) * dt + sigma * std::sqrt(dt) * d(gen));
            }
            sumPayoffs += std::max(S - K, 0.0);
        }
        return std::exp(-r * T) * (sumPayoffs / numSimulations);
    }

    int main() {
        double S0 = 100.0;
        double K = 100.0;
        double T = 1.0;
        double r = 0.05;
        double sigma = 0.2;
        int numSimulations = 10000;

        double optionPrice = monteCarloOptionPrice(S0, K, T, r, sigma, numSimulations);
        std::cout << "Option Price: " << optionPrice << std::endl;
        return 0;
    }
    ```

16. **Black-Scholes Option Pricing Formula**

    ```cpp
    #include <iostream>
    #include <cmath>

    double blackScholesCall(double S, double K, double T, double r, double sigma) {
        double d1 = (std::log(S / K) + (r + 0.5 * sigma * sigma) * T) / (sigma * std::sqrt(T));
        double d2 = d1 - sigma * std::sqrt(T);

        double Nd1 = 0.5 * (1 + std::erf(d1 / std::sqrt(2)));
        double Nd2 = 0.5 * (1 + std::erf(d2 / std::sqrt(2)));

        return S * Nd1 - K * std::exp(-r * T) * Nd2;
    }

    int main() {
        double S = 100.0;
        double K = 100.0;
        double T = 1.0;
        double r = 0.05;
        double sigma = 0.2;

        double callPrice = blackScholesCall(S, K, T, r, sigma);
        std::cout << "Call Option Price: " << callPrice << std::endl;
        return 0;
    }
    ```

17. **GARCH Model for Volatility Forecasting**

    ```cpp
    #include <iostream>
    #include <vector>

    // This is a simplified implementation of GARCH(1,1)
    double garchVolatility(double alpha0, double alpha1, double beta1, double previousReturn, double previousVolatility) {
        return alpha0 + alpha1 * (previousReturn * previousReturn) + beta1 * (previousVolatility * previousVolatility);
    }

    int main() {
        double alpha0 = 0.1;
        double alpha1 = 0.1;
        double beta1 = 0.8;
        double previousReturn = 0.02;
        double previousVolatility = 0.15;

        double forecastedVolatility = garchVolatility(alpha0, alpha1, beta1, previousReturn, previousVolatility);
        std::cout << "Forecasted Volatility: " << forecastedVolatility << std::endl;
        return 0;
    }
    ```

18. **Value at Risk (VaR) Calculation**

    ```cpp
    #include <iostream>
    #include <vector>
    #include <algorithm>

    double valueAtRisk(std::vector<double>& returns, double alpha) {
        std::sort(returns.begin(), returns.end());
        size_t index = static_cast<size_t>(alpha * returns.size());
        return returns[index];
    }

    int main() {
        std::vector<double> returns = {-0.03, -0.02, -0.01, 0.00, 0.01, 0.02, 0.03};
        double alpha = 0.05; // 5% VaR

        double var = valueAtRisk(returns, alpha);
        std::cout << "Value at Risk: " << var << std::endl;
        return 0;
    }
    ```

19. **Sharpe Ratio Calculation**

    ```cpp
    #include <iostream>
    #include <vector>
    #include <numeric>
    #include <cmath>

    double mean(const std::vector<double>& data) {
        return std::accumulate(data.begin(), data.end(), 0.0) / data.size();
    }

    double variance(const std::vector<double>& data, double mean) {
        double sum = 0.0;
        for (double x : data) {
            sum += (x - mean) * (x - mean);
        }
        return sum / data.size();
    }

    double sharpeRatio(const std::vector<double>& returns, double riskFreeRate) {
        double meanReturn = mean(returns);
        double vol = std::sqrt(variance(returns, meanReturn));
        return (meanReturn - riskFreeRate) / vol;
    }

    int main() {
        std::vector<double> returns = {0.01, 0.02, 0.03, 0.04, 0.05};
        double riskFreeRate = 0.01;

        double ratio = sharpeRatio(returns, riskFreeRate);
        std::cout << "Sharpe Ratio: " << ratio << std::endl;
        return 0;
    }
    ```

20. **Monte Carlo Simulation for Portfolio Value**

    ```cpp
    #include <iostream>
    #include <random>
    #include <vector>
    #include <cmath>

    double simulatePortfolioValue(const std::vector<double>& initialValues, double r, double sigma, int numSimulations) {
        std::random_device rd;
        std::mt19937 gen(rd());
        std::normal_distribution<> d(0, 1);

        double sum = 0.0;
        int numAssets = initialValues.size();

        for (int i = 0; i < numSimulations; ++i) {
            double portfolioValue = 0.0;
            for (double value : initialValues) {
                portfolioValue += value * std::exp(r + sigma * d(gen));
            }
            sum += portfolioValue;
        }

        return sum / numSimulations;
    }

    int main() {
        std::vector<double> initialValues = {100.0, 150.0, 200.0};
        double r = 0.05;
        double sigma = 0.2;
        int numSimulations = 10000;

        double portfolioValue = simulatePortfolioValue(initialValues, r, sigma, numSimulations);
        std::cout << "Simulated Portfolio Value: " << portfolioValue << std::endl;
        return 0;
    }
    ```

21. **Option Greeks: Delta Calculation**

    ```cpp
    #include <iostream>
    #include <cmath>

    double blackScholesDelta(double S, double K, double T, double r, double sigma) {
        double d1 = (std::log(S / K) + (r + 0.5 * sigma * sigma) * T) / (sigma * std::sqrt(T));
        return std::exp(-r * T) * (0.5 * (1 + std::erf(d1 / std::sqrt(2))));
    }

    int main() {
        double S = 100.0;
        double K = 100.0;
        double T = 1.0;
        double r = 0.05;
        double sigma = 0.2;

        double delta = blackScholesDelta(S, K, T, r, sigma);
        std::cout << "Delta of the Call Option: " << delta << std::endl;
        return 0;
    }
    ``

`

22. **Delta-Gamma Hedging**

    ```cpp
    #include <iostream>

    double deltaGammaHedging(double delta, double gamma, double position, double hedgeRatio) {
        return position - hedgeRatio * delta / gamma;
    }

    int main() {
        double delta = 0.5;
        double gamma = 0.1;
        double position = 100000;
        double hedgeRatio = 1.0;

        double hedgedPosition = deltaGammaHedging(delta, gamma, position, hedgeRatio);
        std::cout << "Hedged Position: " << hedgedPosition << std::endl;
        return 0;
    }
    ```

23. **Portfolio Optimization: Mean-Variance Analysis**

    ```cpp
    #include <iostream>
    #include <vector>
    #include <numeric>
    #include <cmath>

    double portfolioVariance(const std::vector<double>& weights, const std::vector<std::vector<double>>& covarianceMatrix) {
        double variance = 0.0;
        int numAssets = weights.size();

        for (int i = 0; i < numAssets; ++i) {
            for (int j = 0; j < numAssets; ++j) {
                variance += weights[i] * weights[j] * covarianceMatrix[i][j];
            }
        }
        return variance;
    }

    int main() {
        std::vector<double> weights = {0.4, 0.6};
        std::vector<std::vector<double>> covarianceMatrix = {{0.0004, 0.0002}, {0.0002, 0.0003}};

        double variance = portfolioVariance(weights, covarianceMatrix);
        std::cout << "Portfolio Variance: " << variance << std::endl;
        return 0;
    }
    ```

24. **Calculating Forward Price of a Commodity**

    ```cpp
    #include <iostream>
    #include <cmath>

    double forwardPrice(double spotPrice, double costOfCarry, double time) {
        return spotPrice * std::exp(costOfCarry * time);
    }

    int main() {
        double spotPrice = 100.0;
        double costOfCarry = 0.05;
        double time = 1.0;

        double fPrice = forwardPrice(spotPrice, costOfCarry, time);
        std::cout << "Forward Price: " << fPrice << std::endl;
        return 0;
    }
    ```

25. **Interest Rate Swaps: Present Value Calculation**

    ```cpp
    #include <iostream>
    #include <cmath>

    double presentValueInterestRateSwap(double fixedRate, double floatingRate, double notional, double time, double discountFactor) {
        return notional * (fixedRate - floatingRate) * time * discountFactor;
    }

    int main() {
        double fixedRate = 0.03;
        double floatingRate = 0.02;
        double notional = 1000000.0;
        double time = 1.0;
        double discountFactor = 0.98;

        double pvSwap = presentValueInterestRateSwap(fixedRate, floatingRate, notional, time, discountFactor);
        std::cout << "Present Value of Interest Rate Swap: " << pvSwap << std::endl;
        return 0;
    }
    ```

26. **Real Option Valuation Using Binomial Tree**

    ```cpp
    #include <iostream>
    #include <vector>
    #include <cmath>

    double binomialOptionPrice(double S, double K, double r, double T, double sigma, int n, bool isCall) {
        double dt = T / n;
        double u = std::exp(sigma * std::sqrt(dt));
        double d = 1 / u;
        double p = (std::exp(r * dt) - d) / (u - d);
        std::vector<double> optionPrices(n + 1);

        for (int i = 0; i <= n; ++i) {
            double ST = S * std::pow(u, n - i) * std::pow(d, i);
            optionPrices[i] = isCall ? std::max(ST - K, 0.0) : std::max(K - ST, 0.0);
        }

        for (int j = n - 1; j >= 0; --j) {
            for (int i = 0; i <= j; ++i) {
                optionPrices[i] = (p * optionPrices[i] + (1 - p) * optionPrices[i + 1]) / std::exp(r * dt);
            }
        }

        return optionPrices[0];
    }

    int main() {
        double S = 100.0;
        double K = 100.0;
        double r = 0.05;
        double T = 1.0;
        double sigma = 0.2;
        int n = 100;
        bool isCall = true;

        double optionPrice = binomialOptionPrice(S, K, r, T, sigma, n, isCall);
        std::cout << "Option Price (Binomial Tree): " << optionPrice << std::endl;
        return 0;
    }
    ```

27. **Pricing Barrier Options**

    ```cpp
    #include <iostream>
    #include <cmath>
    #include <vector>

    double barrierOptionPrice(double S, double K, double r, double T, double sigma, double barrier, int n, bool isCall) {
        double dt = T / n;
        double u = std::exp(sigma * std::sqrt(dt));
        double d = 1 / u;
        double p = (std::exp(r * dt) - d) / (u - d);
        std::vector<double> optionPrices(n + 1);

        for (int i = 0; i <= n; ++i) {
            double ST = S * std::pow(u, n - i) * std::pow(d, i);
            optionPrices[i] = ST > barrier ? (isCall ? std::max(ST - K, 0.0) : std::max(K - ST, 0.0)) : 0.0;
        }

        for (int j = n - 1; j >= 0; --j) {
            for (int i = 0; i <= j; ++i) {
                optionPrices[i] = (p * optionPrices[i] + (1 - p) * optionPrices[i + 1]) / std::exp(r * dt);
            }
        }

        return optionPrices[0];
    }

    int main() {
        double S = 100.0;
        double K = 100.0;
        double r = 0.05;
        double T = 1.0;
        double sigma = 0.2;
        double barrier = 120.0;
        int n = 100;
        bool isCall = true;

        double optionPrice = barrierOptionPrice(S, K, r, T, sigma, barrier, n, isCall);
        std::cout << "Barrier Option Price: " << optionPrice << std::endl;
        return 0;
    }
    ```

28. **Hull-White Interest Rate Model**

    ```cpp
    #include <iostream>
    #include <random>
    #include <cmath>

    double hullWhiteRate(double r0, double theta, double kappa, double sigma, double dt) {
        std::random_device rd;
        std::mt19937 gen(rd());
        std::normal_distribution<> d(0, 1);
        double dr = kappa * (theta - r0) * dt + sigma * std::sqrt(dt) * d(gen);
        return r0 + dr;
    }

    int main() {
        double r0 = 0.05;
        double theta = 0.03;
        double kappa = 0.1;
        double sigma = 0.02;
        double dt = 1.0;

        double rate = hullWhiteRate(r0, theta, kappa, sigma, dt);
        std::cout << "Hull-White Interest Rate: " << rate << std::endl;
        return 0;
    }
    ```

29. **Copula Models for Dependence Structure**

    ```cpp
    #include <iostream>
    #include <cmath>

    double gaussianCopula(double u, double v, double rho) {
        double z1 = std::sqrt(-2 * std::log(u));
        double z2 = std::sqrt(-2 * std::log(v));
        double p = std::erf(rho * (z1 * z2) / (std::sqrt(1 - rho * rho)));
        return p;
    }

    int main() {
        double u = 0.5;
        double v = 0.5;
        double rho = 0.3;

        double copulaValue = gaussianCopula(u, v, rho);
        std::cout << "Gaussian Copula Value: " << copulaValue << std::endl;
        return 0;
    }
    ```

30. **Risk Management: Stop-Loss Calculation**

    ```cpp
    #include <iostream>

    double stopLoss(double initialInvestment, double stopLossPercentage) {
        return initialInvestment * (1 - stopLossPercentage);
    }

    int main() {
        double initialInvestment = 10000.0;
        double stopLossPercentage = 0.1; // 10%

        double stopLossValue = stop

Loss(initialInvestment, stopLossPercentage);
        std::cout << "Stop-Loss Value: " << stopLossValue << std::endl;
        return 0;
    }
    ```

Here's a detailed explanation and C++ implementation for various derivatives and option pricing topics:

### **4. Derivatives and Option Pricing**

**Basic Derivative Pricing:**

- **Forward and Futures Contracts:**

  - **Pricing Formula:**
    \[ F_0 = S_0 \times e^{(r - q)T} \]
    Where:
    - \( F_0 \) = Forward price
    - \( S_0 \) = Spot price
    - \( r \) = Risk-free rate
    - \( q \) = Dividend yield
    - \( T \) = Time to maturity

  **C++ Implementation:**
  ```cpp
  #include <iostream>
  #include <cmath>

  double forwardPrice(double spotPrice, double rate, double dividendYield, double time) {
      return spotPrice * std::exp((rate - dividendYield) * time);
  }

  int main() {
      double spotPrice = 100.0;       // Current spot price
      double rate = 0.03;             // Risk-free rate
      double dividendYield = 0.02;    // Dividend yield
      double time = 1.0;              // Time to maturity

      double forward = forwardPrice(spotPrice, rate, dividendYield, time);
      std::cout << "Forward Price: " << forward << std::endl;

      return 0;
  }
  ```

- **Options:**

  - **Call and Put Options:** Rights to buy (call) or sell (put) an asset at a predetermined price before expiration.

**Black-Scholes Model:**

The Black-Scholes model provides a theoretical price for European call and put options.

- **Black-Scholes Formula for Call Options:**
  \[ C = S_0 \Phi(d_1) - K e^{-rT} \Phi(d_2) \]
  Where:
  - \( d_1 = \frac{\ln(S_0 / K) + (r + \sigma^2 / 2)T}{\sigma \sqrt{T}} \)
  - \( d_2 = d_1 - \sigma \sqrt{T} \)
  - \( \Phi \) is the cumulative distribution function of the standard normal distribution

  **C++ Implementation:**
  ```cpp
  #include <iostream>
  #include <cmath>
  #include <random>

  double normCDF(double x) {
      std::normal_distribution<> dist(0, 1);
      std::random_device rd;
      std::mt19937 gen(rd());
      return 0.5 * (1 + std::erf(x / std::sqrt(2.0)));
  }

  double blackScholesCall(double S0, double K, double r, double T, double sigma) {
      double d1 = (std::log(S0 / K) + (r + 0.5 * sigma * sigma) * T) / (sigma * std::sqrt(T));
      double d2 = d1 - sigma * std::sqrt(T);
      return S0 * normCDF(d1) - K * std::exp(-r * T) * normCDF(d2);
  }

  int main() {
      double S0 = 100.0; // Current stock price
      double K = 100.0;  // Strike price
      double r = 0.05;   // Risk-free rate
      double T = 1.0;    // Time to expiration
      double sigma = 0.2; // Volatility

      double callPrice = blackScholesCall(S0, K, r, T, sigma);
      std::cout << "Call Option Price: " << callPrice << std::endl;

      return 0;
  }
  ```

**Binomial Model:**

The binomial model uses a discrete-time approach to estimate option prices by constructing a binomial tree.

- **Binomial Tree Construction:** Models the possible paths of asset prices over time.

  **C++ Implementation:**
  ```cpp
  #include <iostream>
  #include <vector>
  #include <algorithm>

  double binomialCallPrice(double S0, double K, double T, double r, double sigma, int n) {
      double dt = T / n;
      double u = std::exp(sigma * std::sqrt(dt));
      double d = 1 / u;
      double p = (std::exp(r * dt) - d) / (u - d);
      std::vector<double> prices(n + 1);
      std::vector<double> values(n + 1);

      for (int i = 0; i <= n; ++i) {
          prices[i] = S0 * std::pow(u, n - i) * std::pow(d, i);
          values[i] = std::max(0.0, prices[i] - K);
      }

      for (int j = n - 1; j >= 0; --j) {
          for (int i = 0; i <= j; ++i) {
              values[i] = (p * values[i] + (1 - p) * values[i + 1]) / std::exp(r * dt);
          }
      }

      return values[0];
  }

  int main() {
      double S0 = 100.0; // Initial stock price
      double K = 100.0;  // Strike price
      double T = 1.0;    // Time to expiration
      double r = 0.05;   // Risk-free rate
      double sigma = 0.2; // Volatility
      int n = 100;       // Number of time steps

      double callPrice = binomialCallPrice(S0, K, T, r, sigma, n);
      std::cout << "Binomial Call Option Price: " << callPrice << std::endl;

      return 0;
  }
  ```

### **5. Risk Management and Hedging**

**Risk Measures:**

Risk management involves quantifying and managing the risks associated with financial positions.

- **Value at Risk (VaR):**
  - **Definition:** The maximum loss over a specified period at a given confidence level.
  - **Calculation:** VaR can be computed using historical simulation, variance-covariance, or Monte Carlo methods.

- **Conditional VaR (CVaR):**
  - **Definition:** The expected loss given that the loss exceeds the VaR threshold.

  **C++ Implementation:**
  ```cpp
  #include <iostream>
  #include <vector>
  #include <algorithm>

  double valueAtRisk(const std::vector<double>& returns, double confidenceLevel) {
      std::vector<double> sortedReturns = returns;
      std::sort(sortedReturns.begin(), sortedReturns.end());
      int index = static_cast<int>((1 - confidenceLevel) * sortedReturns.size());
      return sortedReturns[index];
  }

  int main() {
      std::vector<double> returns = { -0.05, -0.02, 0.01, -0.03, 0.04, -0.01 };
      double confidenceLevel = 0.95;

      double var = valueAtRisk(returns, confidenceLevel);
      std::cout << "Value at Risk: " << var << std::endl;

      return 0;
  }
  ```

**Hedging Strategies:**

Hedging aims to reduce or manage risk associated with financial positions.

- **Delta Hedging:**
  - **Technique:** Adjusting the position in the underlying asset to maintain a delta-neutral portfolio.

- **Portfolio Insurance:**
  - **Method:** Using options and other instruments to protect a portfolio from significant losses.

  **C++ Implementation:**
  ```cpp
  #include <iostream>

  double deltaHedge(double optionDelta, double stockPrice, double positionSize) {
      return -optionDelta * stockPrice * positionSize;
  }

  int main() {
      double optionDelta = 0.5; // Delta of the option
      double stockPrice = 100.0; // Current stock price
      double positionSize = 10.0; // Size of the position

      double hedgeAmount = deltaHedge(optionDelta, stockPrice, positionSize);
      std::cout << "Amount to Hedge: " << hedgeAmount << std::endl;

      return 0;
  }
  ```

### **6. Fixed Income Securities**

**Bond Pricing and Valuation:**

Fixed income securities, such as bonds, provide regular interest payments and return of principal at maturity.

- **Zero-Coupon Bonds:**

  **Pricing Formula:**
  \[ P = \frac{F}{(1 + r)^n} \]
  Where:
  - \( P \) = Price
  - \( F \) = Face value
  - \( r \) = Yield to maturity
  - \( n \) = Number of periods

- **Coupon Bonds:**

  **Pricing Formula:**
  As previously mentioned.

  **Duration and Convexity:**
  - **Duration:** Measures the weighted average time to receive bond cash flows.
  - **Convexity:** Measures the curvature in the bond price-yield relationship.

  **C++ Implementation:**
  ```cpp
  #include <iostream>
  #include <vector>
  #include <cmath>

  double bondDuration(const std::vector<double>& cashFlows, double yield) {
      double duration = 0.0;
      double price = 0.0;
      int n = cashFlows.size();

      for (int t = 0; t < n; ++t) {
         

 price += cashFlows[t] / std::pow(1 + yield, t + 1);
          duration += (t + 1) * cashFlows[t] / std::pow(1 + yield, t + 1);
      }
      return duration / price;
  }

  int main() {
      std::vector<double> cashFlows = { 50.0, 50.0, 50.0, 50.0, 1050.0 }; // Annual coupons and face value
      double yield = 0.05; // Yield to maturity

      double duration = bondDuration(cashFlows, yield);
      std::cout << "Bond Duration: " << duration << std::endl;

      return 0;
  }
  ```

**Interest Rate Models:**

Models such as Vasicek and Cox-Ingersoll-Ross (CIR) describe the evolution of interest rates over time.

- **Vasicek Model:**
  \[ dr = \theta (\mu - r) dt + \sigma \sqrt{r} dW(t) \]

- **Cox-Ingersoll-Ross (CIR) Model:**
  \[ dr = \kappa (\theta - r) dt + \sigma \sqrt{r} dW(t) \]

  **C++ Implementation:**
  ```cpp
  #include <iostream>
  #include <random>

  double vasicekModel(double r0, double mu, double theta, double sigma, double dt) {
      std::random_device rd;
      std::mt19937 gen(rd());
      std::normal_distribution<> d(0, 1);
      return r0 + mu * dt + sigma * std::sqrt(dt) * std::sqrt(r0) * d(gen);
  }

  int main() {
      double r0 = 0.05; // Initial interest rate
      double mu = 0.03; // Long-term mean
      double theta = 0.02; // Speed of reversion
      double sigma = 0.01; // Volatility
      double dt = 1.0;    // Time increment

      double r1 = vasicekModel(r0, mu, theta, sigma, dt);
      std::cout << "Interest Rate after one time step: " << r1 << std::endl;

      return 0;
  }
  ```

### **7. Portfolio Optimization**

**Modern Portfolio Theory (MPT):**

MPT focuses on constructing a portfolio that maximizes return for a given level of risk.

- **Efficient Frontier:**

  **Objective:**
  - Maximize return for a given risk level.
  - Minimize risk for a given return level.

- **Mean-Variance Optimization:**

  **Optimization Problem:**
  - Maximize the Sharpe ratio:
    \[ \text{Sharpe Ratio} = \frac{R_p - R_f}{\sigma_p} \]
    Where:
    - \( R_p \) = Portfolio return
    - \( R_f \) = Risk-free rate
    - \( \sigma_p \) = Portfolio standard deviation

  **C++ Implementation:**
  ```cpp
  #include <iostream>
  #include <vector>
  #include <cmath>

  double portfolioVariance(const std::vector<double>& weights, const std::vector<std::vector<double>>& covarianceMatrix) {
      double variance = 0.0;
      int n = weights.size();

      for (int i = 0; i < n; ++i) {
          for (int j = 0; j < n; ++j) {
              variance += weights[i] * weights[j] * covarianceMatrix[i][j];
          }
      }
      return variance;
  }

  int main() {
      std::vector<double> weights = {0.5, 0.5}; // Portfolio weights
      std::vector<std::vector<double>> covarianceMatrix = {{0.04, 0.01}, {0.01, 0.03}}; // Covariance matrix

      double variance = portfolioVariance(weights, covarianceMatrix);
      std::cout << "Portfolio Variance: " << variance << std::endl;

      return 0;
  }
  ```

**Capital Asset Pricing Model (CAPM):**

CAPM relates the expected return of an asset to its risk as measured by beta.

- **CAPM Formula:**
  \[ R_i = R_f + \beta_i (R_m - R_f) \]
  Where:
  - \( R_i \) = Expected return of asset \( i \)
  - \( R_f \) = Risk-free rate
  - \( \beta_i \) = Beta of asset \( i \)
  - \( R_m \) = Expected market return

  **C++ Implementation:**
  ```cpp
  #include <iostream>

  double capmReturn(double riskFreeRate, double beta, double marketReturn) {
      return riskFreeRate + beta * (marketReturn - riskFreeRate);
  }

  int main() {
      double riskFreeRate = 0.03; // Risk-free rate
      double beta = 1.2;          // Beta of the asset
      double marketReturn = 0.08; // Expected market return

      double expectedReturn = capmReturn(riskFreeRate, beta, marketReturn);
      std::cout << "Expected Return: " << expectedReturn << std::endl;

      return 0;
  }
  ```

### **8. Advanced Topics**

**Machine Learning in Finance:**

Machine learning techniques, such as regression trees, neural networks, and clustering, are increasingly used for predictive modeling and strategy development.

- **Regression Trees:**
  - **Application:** Used for predicting financial outcomes based on historical data.

- **Neural Networks:**
  - **Application:** Employed in algorithmic trading, credit scoring, and market predictions.

  **C++ Implementation:**
  Implementing machine learning models from scratch in C++ is complex and often involves using libraries like TensorFlow or PyTorch. For simpler cases, you might use a basic implementation of regression or classification algorithms. For more advanced models, using specialized libraries or languages like Python is more common.
