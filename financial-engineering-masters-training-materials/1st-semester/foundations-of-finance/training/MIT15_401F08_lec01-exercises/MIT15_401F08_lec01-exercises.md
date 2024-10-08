1. Discuss why understanding finance is critical for business decision-making, particularly in asset valuation and management. Create a case study involving a company facing a tough decision on whether to invest in a new technology. Use quantitative analysis to support your answer.

- Why understanding Finance is critical for business decision-making?
  - Efficient resource allocation through fiancial metrics
  - Risk evaluation with investment
  - Assets can evaluated accurately
  - Strategies can be planned more efficiently because of insights

- Case stuy: FinAI Tech Company
  - Midsized Fintech Company, company considers in investing in new AI, total investment of $1 Million,
  - Cash flow over the next five years:
    - 1. $300,000
    - 2. $400,000 
    - 3. $500,000
    - 4. $600,000     
    - 5. $700,000 
  - Discount reate is 10% for its product
 
  - Quantitative analysis

```c++
#include <iostream>
#include <vector>
#include <cmath>

using namespace std;

// Function to calculate Net Present Value (NPV)
double calculateNPV(double initialInvestment, const vector<double>& cashFlows, double discountRate) {
    double npv = 0.0; // Initialize NPV to zero

    // Loop through each year's cash flow
    for (size_t t = 0; t < cashFlows.size(); ++t) {
        // Calculate the present value of the cash flow for year t
        // Cash Flow_t / (1 + r)^t
        double presentValue = cashFlows[t] / pow(1 + discountRate, t + 1);
        npv += presentValue; // Accumulate the present values
    }

    // Subtract the initial investment from the total present value to get NPV
    npv -= initialInvestment;

    return npv; // Return the calculated NPV
}

// Function to calculate the Internal Rate of Return (IRR)
// Here we use the Newton-Raphson method for finding the root of NPV equation
double calculateIRR(double initialInvestment, const vector<double>& cashFlows, double guess = 0.1, int maxIterations = 1000, double tolerance = 0.0001) {
    double rate = guess; // Initial guess for the IRR
    int iteration = 0;

    while (iteration < maxIterations) {
        // Calculate the NPV for the current rate
        double npv = calculateNPV(initialInvestment, cashFlows, rate);

        // Calculate the derivative of NPV with respect to the rate (slope)
        double npvDerivative = 0.0;
        for (size_t t = 0; t < cashFlows.size(); ++t) {
            // Derivative: -Cash Flow_t * t / (1 + r)^(t + 1)
            npvDerivative -= cashFlows[t] * (t + 1) / pow(1 + rate, t + 2);
        }

        // Update the rate using Newton-Raphson formula
        double newRate = rate - (npv / npvDerivative);

        // Check if the result is within the tolerance level
        if (abs(newRate - rate) < tolerance) {
            return newRate; // Return the calculated IRR
        }

        rate = newRate; // Update the rate for the next iteration
        ++iteration; // Increment the iteration counter
    }

    return rate; // Return the last calculated rate if max iterations reached
}

int main() {
    double initialInvestment = 1000000; // Initial investment in dollars
    vector<double> cashFlows = {300000, 400000, 500000, 600000, 700000}; // Cash flows for years 1-5
    double discountRate = 0.10; // Discount rate of 10%

    // Calculate NPV
    double npv = calculateNPV(initialInvestment, cashFlows, discountRate);
    cout << "Net Present Value (NPV): $" << npv << endl;

    // Calculate IRR
    double irr = calculateIRR(initialInvestment, cashFlows);
    cout << "Internal Rate of Return (IRR): " << irr * 100 << "%" << endl;

    return 0;
}
```

----

2. Develop a financial model to illustrate the difference between real and financial assets, using examples from real-world companies. Analyze how each type of asset impacts a company's valuation.

- Real asset: physical or tangible (Real Estate, Machinery and Equipment, Natural Resources)
- Financial asset: Represents claim to ownership or a contractual right to receive cash of another fnancial asset (Stocks, Bonds, Derivatives)

| Feature                        | Real Assets                                     | Financial Assets                               |
|--------------------------------|------------------------------------------------|------------------------------------------------|
| **Nature**                     | Physical, tangible assets                       | Intangible, contractual claims                  |
| **Value Determinants**        | Market demand, condition, location              | Market rates, company performance, creditworthiness |
| **Usage**                      | Used in production or as resources              | Used for investment or liquidity                |
| **Depreciation/Amortization** | Subject to depreciation over time               | Generally do not depreciate, but can fluctuate in value |
| **Liquidity**                  | Generally less liquid, harder to sell quickly  | Usually more liquid, easily tradable           |

```python
import numpy as np


def main() -> None:
    """Driving code."""
    # Company A: Real Asset-Focused Company (Manufacturing)
    # Assets
    real_estate = 5000000 # Real estate value in dollars
    machinery = 2000000 # Machinery value in dollars
    total_assets_A = real_estate + machinery  # Total assets for Company A
    
    # Liabilities
    liabilities_A = 1500000 # Total liabilities in dollars
    
    # Revenue and Expenses
    revenue_A = 4000000 # Revenue for Company A
    expenses_A = 2500000 # Expenses for Company A (including depreciation)
    
    # Calculate NAV for Company A
    nav_A = calculate_nav(total_assets_A, liabilities_A)
    print(f"Company A - Net Asset Value (NAV): ${nav_A:,.2f}")

    # Calculate EBIT for Company A
    ebit_A = calculate_ebit(revenue_A, expenses_A)
    print(f"Company A - Earnings Before Interest and Taxes (EBIT): ${ebit_A:,.2f}")

    # Assuming an EV/EBIT multiple of 10 for Company A
    valuation_multiple_A = 10
    valuation_A = calculate_valuation(ebit_A, valuation_multiple_A)
    print(f"Company A - Valuation: ${valuation_A:,.2f}\n")
    
    # Company B: Financial Asset-Focused Company (Technology)
    # Assets
    cash_and_equivalents = 10000000 # Cash value in dollars
    marketable_securities = 5000000 # Marketable securities value in dollars
    total_assets_B = cash_and_equivalents + marketable_securities  # Total assets for Company B
    
    # Liabilities
    liabilities_B = 3000000 # Total liabilities in dollars
    
    # Revenue and Expenses
    revenue_B = 6000000 # Revenue for Company B
    expenses_B = 3500000 # Expenses for Company B
    
    # Calculate NAV for Company B
    nav_B = calculate_nav(total_assets_B, liabilities_B)
    print(f"Company B - Net Asset Value (NAV): ${nav_B:,.2f}")

    # Calculate EBIT for Company B
    ebit_B = calculate_ebit(revenue_B, expenses_B)
    print(f"Company B - Earnings Before Interest and Taxes (EBIT): ${ebit_B:,.2f}")

    # Assuming an EV/EBIT multiple of 12 for Company B
    valuation_multiple_B = 12
    valuation_B = calculate_valuation(ebit_B, valuation_multiple_B)
    print(f"Company B - Valuation: ${valuation_B:,.2f}")

    return None


# Function to calculate Net Asset Value (NAV)
def calculate_nav(total_assets, total_liabilities):
    """Calculate the Net Asset Value (NAV) of a company.
    
    NAV = Total Assets - Total Liabilities
    """

    return total_assets - total_liabilities


def calculate_ebit(revenue, expenses):
    """Calculate Earnings Before Interest and Taxes (EBIT).
    
    EBIT = Revenue - Expenses
    """

    return revenue - expenses


def calculate_valuation(ebit, multiple):
    """Calculate the valuation of a company based on the EV/EBIT multiple.
    
    Valuation = EBIT * Valuation Multiple
    """

    return ebit * multiple


if __name__ == "__main__":
    main()
```

----

3. Choose a non-financial corporation and evaluate how it raises capital. Identify the financial intermediaries involved and discuss the role of capital markets in this process.

- OpenAI: Technological Research Organization and Technological Company
  - Equity Financing: Equity investments from Venture Capital Firms
  - Partnership: In cooperation with large Tech companies.
  - Grants and Donations: From Philanthropists and other Organizations 
- Financial Intermediaries: Venture Capital Firms, Investment Banks, Tech Partners, Philanthropic Organizations
- Role of Capital Markets: Access to funding, Liquiditiy and platform for price discovery, Investors protection

----

4. Create a flow diagram representing the circulation of money between households, non-financial corporations, financial intermediaries, and capital markets. Apply this to a real-world economy, explaining the interaction between these entities.

- Households
  - Member sof a household provide labour and earn wages. They deposit money in the bank as for savings or buy stocks, bonds, invest in Fonds as well.
- Financial Coporations
  - Banks act as intermediaries between households ad none financial cooperations. They invest in capital and loan money to the household.
- Capital Makets
  - NYSE, where etc. Amazon or Google issue stocks and bonds. 

----

5. Compare the valuation of tangible and intangible assets in a chosen company. Discuss how these valuations affect its financial management strategies.

- Tangible asstes are for examples Smartphones, MacBooks or even Corporate Buildings. These asstes have acertain value and depreciate over time according to a fixed schedule.
- Intangible assets are non-physical asstes and provide long-term value to a company. The value of such an asset is hard to measure. Examples for such assets are Intellectual Property, Brand Value, Software and Ecosystem, etc. 

----

6. Analyze the market for a company's stock and discuss the price discovery process. Consider how market value is determined by external factors, irrespective of the company's internal objectives.

- Stock Market - Tesla Inc.:
  - Listed on the NASDAQ
  - Ticker symbol: TSLA
  - Key characteristics: High volatility, Retail Investor INterest, Institutionalholdings, Options market Influence
  - Price discovery process:
    - Market Sentiment: Investor optimism or pessimism can drive Tesla’s stock price up or down.
    - Information Flow: Stock prices reflect new information quickly.
    - Liquidity and Trading Volume: With Tesla being one of the most traded stocks globally, high liquidity allows investors to buy and sell easily, leading to efficient price discovery. 
    - Bid-Ask Spread: In any stock market, the difference between the highest price buyers are willing to pay (bid) and the lowest price sellers are willing to accept (ask) helps in determining the final trading price.

----

7. Create a hypothetical scenario where a corporation has to decide between two investment options. Evaluate these options using discounted cash flow analysis, taking into account the time value of money and associated risks.

8. Compare the accounting practices of two companies from different industries. Focus on their balance sheets and income statements to evaluate financial health. Discuss how accounting principles influence financial analysis.

9. Using real-world financial statements, distinguish between stock and flow variables. Explain the importance of each in financial decision-making.

10. Develop a case study of a corporation raising cash through both equity and debt. Explain the impact on the balance sheet and income statement, and analyze which financing method is more effective for the company's growth.

11. Construct an example of a company’s cash flow cycle, including cash raised, invested, generated, reinvested, and returned to investors. Examine the financial health of a company with an unbalanced cash flow cycle.

12. Identify a company that recently went through a major investment decision. Analyze the impact of this decision on its real and financial assets, as well as on its shareholder value.

13. Research a company that has experienced financial difficulties. Use accounting analysis to assess what went wrong, focusing on its balance sheet and income statement.

14. Create a financial plan for a company that needs to raise $10 million to expand its operations. Compare the potential sources of financing and suggest the most suitable option.

15. Explore the role of risk management in corporate finance by assessing a company’s recent financial statements. Identify the risks the company faces and discuss how they manage these risks.

16. Create a case study on how time and risk influence a company's financial decision-making process. Focus on an investment decision made by a multinational corporation.

17. Analyze a company’s dividend policy over the past decade. Discuss how its payout decisions reflect its overall financial strategy and shareholder value creation.

18. Compare and contrast the financial management strategies of two companies operating in different sectors. Focus on their investment, financing, and payout decisions.

19. Develop a model that forecasts a company’s stock price based on its financial statements. Use fundamental analysis to explain the relationships between variables.

20. Design a framework to evaluate how a company’s financial decisions are influenced by its corporate objectives. Apply this to a real-world scenario where corporate goals conflict with market valuation.

21. Investigate the role of financial intermediaries in a recent major merger or acquisition. Analyze the functions of banks and other institutions in facilitating the deal.

22. Analyze a company’s risk management strategy by focusing on its use of derivatives or other financial instruments. Explain how these instruments are used to hedge against potential risks.

23. Assess the financial health of a company by calculating key financial ratios (e.g., liquidity, profitability, solvency). Discuss how these ratios inform business decisions.

24. Examine a recent IPO and analyze how the company raised capital through equity markets. Discuss the implications of this decision for both the company and investors.

25. Analyze how a corporation allocates its cash flow between reinvestment and payout to investors. Use financial statements to assess the impact on its growth prospects.

26. Develop a financial strategy for a company planning to expand internationally. Consider the risks involved and propose a strategy for managing currency risk and other financial challenges.

27. Create a valuation model for a company’s real assets, including both tangible and intangible assets. Discuss the challenges in valuing intangible assets like intellectual property.

28. Investigate how financial markets influence a company’s cost of capital. Develop a case study showing how market conditions impact a corporation’s financing decisions.

29. Research a company’s recent acquisition and analyze how it financed the deal. Discuss the financial impact of the acquisition on the company’s balance sheet.

30. Compare the debt and equity structure of two companies. Explain how their capital structures affect their financial risk and shareholder value.

31. Create a financial model to predict how changes in interest rates will affect a company’s profitability. Use historical data to support your predictions.

32. Analyze a company’s earnings report and discuss how management decisions regarding asset allocation and reinvestment have influenced its financial performance.

33. Compare and contrast the investment strategies of two companies from different industries. Analyze how their approaches to asset valuation and management affect their long-term financial health.

34. Research a case where a company has faced liquidity issues. Use its financial statements to assess the causes and suggest strategies for improving liquidity.

35. Develop a cash flow model for a start-up company. Analyze how it manages its limited resources and the implications of its cash flow decisions on future growth.

36. Assess how a company’s use of financial intermediaries affects its ability to manage risk. Develop a case study where financial intermediaries played a key role in stabilizing the company’s financial health.

37. Create a financial analysis report on a company’s recent decision to invest in a new product line. Discuss the valuation process for the new assets and how this investment aligns with the company’s overall strategy.

38. Develop a scenario where a company must choose between issuing bonds or stocks to raise capital. Analyze the trade-offs and recommend the best option based on current market conditions.

39. Investigate a company’s capital allocation strategy. Analyze how its decisions regarding asset acquisition and divestiture affect its financial performance.

40. Create a financial model that shows the impact of inflation on a company’s profitability. Use historical data to predict future trends.

41. Analyze how corporate governance structures influence financial management decisions. Focus on the relationship between shareholders and management in a public company.

42. Create a financial plan for a company that needs to manage both short-term and long-term debt. Discuss the strategies for balancing these obligations while maintaining liquidity.

43. Research a company that has recently changed its dividend policy. Analyze how this change reflects its financial strategy and shareholder expectations.

44. Investigate how a company uses financial data to make strategic decisions. Develop a case study showing how accounting and financial analysis drive business growth.

45. Analyze a company’s capital expenditure decisions over the past five years. Discuss how these decisions reflect its overall financial strategy and risk tolerance.

46. Develop a model that shows how a company’s financial performance is influenced by external economic factors, such as interest rates, inflation, and exchange rates.

47. Create a scenario where a company must decide whether to acquire another firm or invest in organic growth. Use financial analysis to support your recommendation.

48. Investigate the role of financial regulations in shaping a company’s financial management strategies. Analyze how compliance with regulations impacts its decision-making process.

49. Research a company that has undergone significant restructuring. Analyze the financial impact of this restructuring on its balance sheet and income statement.

50. Develop a financial risk assessment for a company considering expansion into a new market. Consider factors such as currency risk, political risk, and market volatility.
