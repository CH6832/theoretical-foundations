# **Programming for Financial Engineering**

## **Course Overview**

This course is designed to equip students with programming skills for solving complex problems in financial engineering using Python and R. Key areas of focus include data analysis, algorithmic trading, financial modeling, and the application of object-oriented programming, data science, and machine learning techniques. Students will gain hands-on experience with real-world financial data and develop the ability to implement and analyze financial models and trading strategies.

## **Topics Covered**

### **Python/R for Finance**

**Data Structures:**

- **Python Data Structures:**

  Python provides various built-in data structures to handle financial data efficiently:

  ```python
  # Lists
  prices = [100, 101, 102, 103]
  
  # Tuples (immutable sequences)
  stock_data = (100, 101, 102, 103)
  
  # Dictionaries (key-value pairs)
  financials = {'AAPL': 150, 'GOOGL': 2800}
  
  # Sets (unique elements)
  unique_assets = {'AAPL', 'GOOGL', 'MSFT'}
  
  # Example using Pandas for financial data
  import pandas as pd
  
  # Creating a DataFrame
  data = {'Date': pd.date_range(start='2022-01-01', periods=5),
          'Price': [100, 101, 102, 103, 104]}
  df = pd.DataFrame(data)
  
  # Displaying DataFrame
  print(df)
  ```

  **R Data Structures:**

  ```r
  # Vectors
  prices <- c(100, 101, 102, 103)
  
  # Matrices
  stock_matrix <- matrix(c(100, 101, 102, 103), nrow=2)
  
  # Data Frames
  dates <- seq(as.Date("2022-01-01"), by="day", length.out=5)
  df <- data.frame(Date=dates, Price=c(100, 101, 102, 103, 104))
  
  # Displaying Data Frame
  print(df)
  ```

**Financial Libraries:**

- **Python Libraries:**

  ```python
  import numpy as np
  import pandas as pd
  from scipy.stats import norm
  
  # Financial calculations
  def black_scholes(S, K, T, r, sigma):
      d1 = (np.log(S / K) + (r + 0.5 * sigma ** 2) * T) / (sigma * np.sqrt(T))
      d2 = d1 - sigma * np.sqrt(T)
      call_price = S * norm.cdf(d1) - K * np.exp(-r * T) * norm.cdf(d2)
      return call_price
  
  # Example calculation
  S = 100  # Stock price
  K = 100  # Strike price
  T = 1    # Time to maturity
  r = 0.05 # Risk-free rate
  sigma = 0.2 # Volatility
  
  print(f"Call Option Price: {black_scholes(S, K, T, r, sigma):.2f}")
  ```

- **R Libraries:**

  ```r
  library(quantmod)
  library(TTR)
  
  # Fetching financial data
  getSymbols("AAPL", src="yahoo", from="2022-01-01")
  stock_data <- Cl(AAPL)
  
  # Calculating moving average
  moving_avg <- SMA(stock_data, n=20)
  plot(index(stock_data), stock_data, type="l", col="blue")
  lines(index(stock_data), moving_avg, col="red")
  ```

### **Object-Oriented Programming**

**Classes and Objects:**

- **Python Example:**

  ```python
  class Bond:
      def __init__(self, face_value, coupon_rate, years_to_maturity):
          self.face_value = face_value
          self.coupon_rate = coupon_rate
          self.years_to_maturity = years_to_maturity
          
      def price(self, discount_rate):
          coupon_payment = self.face_value * self.coupon_rate
          present_value_coupons = sum(coupon_payment / (1 + discount_rate) ** i for i in range(1, self.years_to_maturity + 1))
          present_value_face_value = self.face_value / (1 + discount_rate) ** self.years_to_maturity
          return present_value_coupons + present_value_face_value
  
  # Example usage
  bond = Bond(1000, 0.05, 10)
  print(f"Bond Price: ${bond.price(0.03):.2f}")
  ```

- **C++ Example:**

  ```cpp
  #include <iostream>
  #include <cmath>
  
  class Bond {
  private:
      double face_value;
      double coupon_rate;
      int years_to_maturity;
  
  public:
      Bond(double face_value, double coupon_rate, int years_to_maturity)
          : face_value(face_value), coupon_rate(coupon_rate), years_to_maturity(years_to_maturity) {}
  
      double price(double discount_rate) {
          double coupon_payment = face_value * coupon_rate;
          double present_value_coupons = 0.0;
          for (int i = 1; i <= years_to_maturity; ++i) {
              present_value_coupons += coupon_payment / std::pow(1 + discount_rate, i);
          }
          double present_value_face_value = face_value / std::pow(1 + discount_rate, years_to_maturity);
          return present_value_coupons + present_value_face_value;
      }
  };
  
  int main() {
      Bond bond(1000, 0.05, 10);
      std::cout << "Bond Price: $" << bond.price(0.03) << std::endl;
      return 0;
  }
  ```

**Inheritance and Polymorphism:**

- **Python Example:**

  ```python
  class FixedRateBond(Bond):
      def __init__(self, face_value, coupon_rate, years_to_maturity):
          super().__init__(face_value, coupon_rate, years_to_maturity)
          
      def yield_to_maturity(self, market_price):
          # Simplified YTM calculation for demonstration
          return (self.face_value * self.coupon_rate + (self.face_value - market_price) / self.years_to_maturity) / ((self.face_value + market_price) / 2)
  
  # Example usage
  fixed_bond = FixedRateBond(1000, 0.05, 10)
  print(f"Yield to Maturity: {fixed_bond.yield_to_maturity(950):.2%}")
  ```

- **C++ Example:**

  ```cpp
  #include <iostream>
  
  class FixedRateBond : public Bond {
  public:
      FixedRateBond(double face_value, double coupon_rate, int years_to_maturity)
          : Bond(face_value, coupon_rate, years_to_maturity) {}
  
      double yield_to_maturity(double market_price) {
          // Simplified YTM calculation for demonstration
          return (face_value * coupon_rate + (face_value - market_price) / years_to_maturity) / ((face_value + market_price) / 2);
      }
  };
  
  int main() {
      FixedRateBond fixed_bond(1000, 0.05, 10);
      std::cout << "Yield to Maturity: " << fixed_bond.yield_to_maturity(950) << std::endl;
      return 0;
  }
  ```

**Design Patterns:**

- **Python Example (Strategy Pattern):**

  ```python
  from abc import ABC, abstractmethod
  
  class TradingStrategy(ABC):
      @abstractmethod
      def execute(self, data):
          pass
  
  class MovingAverageStrategy(TradingStrategy):
      def execute(self, data):
          # Implement moving average trading strategy
          pass
  
  class MomentumStrategy(TradingStrategy):
      def execute(self, data):
          # Implement momentum trading strategy
          pass
  
  # Example usage
  def trading_algorithm(strategy, data):
      strategy.execute(data)
  
  strategy = MovingAverageStrategy()
  trading_algorithm(strategy, data)
  ```

- **C++ Example (Singleton Pattern):**

  ```cpp
  #include <iostream>
  
  class ConfigurationManager {
  private:
      static ConfigurationManager* instance;
      ConfigurationManager() {}
  
  public:
      static ConfigurationManager* getInstance() {
          if (instance == nullptr) {
              instance = new ConfigurationManager();
          }
          return instance;
      }
  
      void printSettings() {
          std::cout << "Configuration Settings" << std::endl;
      }
  };
  
  ConfigurationManager* ConfigurationManager::instance = nullptr;
  
  int main() {
      ConfigurationManager* config = ConfigurationManager::getInstance();
      config->printSettings();
      return 0;
  }
  ```

### **Algorithmic Trading**

**Backtesting Strategies:**

- **Python Example:**

  ```python
  import pandas as pd
  import numpy as np
  import matplotlib.pyplot as plt
  
  # Sample backtesting framework
  def backtest_strategy(prices, strategy):
      signals = strategy(prices)
      returns = signals.shift(1) * prices.pct_change()
      cumulative_returns = (1 + returns).cumprod()
      return cumulative_returns
  
  # Example strategy:

 Moving Average Crossover
  def moving_average_strategy(prices):
      short_ma = prices.rolling(window=50).mean()
      long_ma = prices.rolling(window=200).mean()
      signals = np.where(short_ma > long_ma, 1, 0)
      return pd.Series(signals, index=prices.index)
  
  # Simulate backtest
  data = pd.read_csv('historical_prices.csv', index_col='Date', parse_dates=True)
  prices = data['Close']
  returns = backtest_strategy(prices, moving_average_strategy)
  
  # Plot results
  plt.plot(returns)
  plt.title('Strategy Backtest Performance')
  plt.xlabel('Date')
  plt.ylabel('Cumulative Returns')
  plt.show()
  ```

**Portfolio Optimization:**

- **Python Example:**

  ```python
  import numpy as np
  import pandas as pd
  from scipy.optimize import minimize
  
  # Example data
  returns = pd.read_csv('portfolio_returns.csv', index_col='Date', parse_dates=True)
  
  def portfolio_variance(weights, cov_matrix):
      return np.dot(weights.T, np.dot(cov_matrix, weights))
  
  def optimize_portfolio(returns):
      cov_matrix = returns.cov()
      num_assets = len(returns.columns)
      initial_weights = np.ones(num_assets) / num_assets
      bounds = [(0, 1) for _ in range(num_assets)]
      constraints = ({'type': 'eq', 'fun': lambda w: np.sum(w) - 1})
      result = minimize(portfolio_variance, initial_weights, args=(cov_matrix,), method='SLSQP', bounds=bounds, constraints=constraints)
      return result.x
  
  optimal_weights = optimize_portfolio(returns)
  print(f"Optimal Weights: {optimal_weights}")
  ```

**Execution Algorithms:**

- **Python Example:**

  ```python
  def vwap_execution(prices, volumes):
      cum_volume = volumes.cumsum()
      cum_price_volume = (prices * volumes).cumsum()
      vwap = cum_price_volume / cum_volume
      return vwap
  
  # Example data
  prices = pd.Series([100, 101, 102, 103, 104])
  volumes = pd.Series([1000, 1500, 1200, 1300, 1100])
  vwap = vwap_execution(prices, volumes)
  print(vwap)
  ```

### **Data Science Techniques**

**Machine Learning in Finance:**

- **Python Example (Predictive Modeling):**

  ```python
  from sklearn.model_selection import train_test_split
  from sklearn.linear_model import LinearRegression
  from sklearn.metrics import mean_squared_error
  
  # Load dataset
  data = pd.read_csv('stock_data.csv')
  X = data[['Feature1', 'Feature2']]
  y = data['Target']
  
  # Split data
  X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
  
  # Train model
  model = LinearRegression()
  model.fit(X_train, y_train)
  
  # Predictions
  predictions = model.predict(X_test)
  mse = mean_squared_error(y_test, predictions)
  print(f"Mean Squared Error: {mse:.2f}")
  ```

**Big Data Analytics:**

- **Python Example (Using PySpark):**

  ```python
  from pyspark.sql import SparkSession
  from pyspark.sql.functions import col
  
  # Initialize SparkSession
  spark = SparkSession.builder.appName('FinancialDataAnalysis').getOrCreate()
  
  # Load data
  data = spark.read.csv('big_data_financials.csv', header=True, inferSchema=True)
  
  # Process data
  data = data.withColumn('Price', col('Price').cast('double'))
  data.show()
  
  # Aggregation example
  average_price = data.groupBy('Date').avg('Price')
  average_price.show()
  ```

**Neural Networks:**

- **Python Example (Deep Learning):**

  ```python
  import numpy as np
  import pandas as pd
  from sklearn.preprocessing import StandardScaler
  from tensorflow.keras.models import Sequential
  from tensorflow.keras.layers import Dense
  
  # Load and preprocess data
  data = pd.read_csv('stock_prices.csv')
  X = data[['Feature1', 'Feature2']]
  y = data['Target']
  
  scaler = StandardScaler()
  X_scaled = scaler.fit_transform(X)
  
  # Build neural network model
  model = Sequential([
      Dense(64, activation='relu', input_shape=(X_scaled.shape[1],)),
      Dense(32, activation='relu'),
      Dense(1)
  ])
  
  model.compile(optimizer='adam', loss='mean_squared_error')
  
  # Train model
  model.fit(X_scaled, y, epochs=10, batch_size=32, validation_split=0.2)
  
  # Predictions
  predictions = model.predict(X_scaled)
  ```

## **Assessment Methods**

- **Problem Sets:** Regular assignments focusing on the application of Python and R for financial data analysis, modeling, and algorithm development. Examples may include writing functions for financial calculations or implementing trading strategies.
- **Midterm Exam:** An assessment covering data structures, financial libraries, and object-oriented programming concepts. Questions may include code-writing tasks and theoretical questions.
- **Final Exam:** A comprehensive exam that includes topics such as algorithmic trading, portfolio optimization, and data science techniques. It may involve analyzing case studies or solving complex problems using programming.
- **Programming Projects:** Hands-on projects where students will develop financial applications, backtest trading strategies, or implement machine learning models. Projects should include well-documented code and a detailed report on the results and findings.

## **Recommended Textbooks**

- **"Python for Finance" by Yves Hilpisch:**
  - This book provides a comprehensive guide to using Python for financial data analysis and modeling, covering both the basics and advanced topics.
- **"Financial Modelling in Python" by Shayne Fletcher and Christopher Gardner:**
  - Offers practical insights into financial modeling using Python, including real-world examples and applications.
