# Monte Carlo Simulation: Normal vs Student-t Distribution (SPY)

## Project Overview

This project implements a Monte Carlo simulation to estimate the potential risk (Value at Risk - VaR) of the SPY ETF. It compares two different statistical models for generating random price paths:
1.  **Normal Distribution**: Assuming returns follow a standard Gaussian distribution.
2.  **Student-t Distribution**: Assuming returns follow a Student-t distribution (with heavier tails), which is often more realistic for financial data during volatile periods.

The goal is to visualize and quantify the difference in extreme loss scenarios between the two models.

## Methodology

1.  **Data Sourcing**: Historical daily price data for **SPY** is downloaded using `yfinance` for the period from **2020-01-01 to 2024-01-01**.
2.  **Parameters**:
    *   Daily log returns are calculated.
    *   Mean ($\mu$) and Standard Deviation ($\sigma$) of log returns are estimated.
3.  **Simulation**:
    *   **Number of Simulations**: 10,000 runs.
    *   **Time Horizon**: 252 trading days (1 year).
    *   **Initial Price**: The last available closing price from the dataset.
4.  **Models**:
    *   **Normal Model**: Random shocks are generated using $\mathcal{N}(0, 1)$.
    *   **Student-t Model**: Random shocks are generated using a Student-t distribution with **degrees of freedom (df) = 5**. These shocks are scaled by $\sqrt{\frac{df-2}{df}}$ to match the variance of the normal distribution for a fair comparison of "fat tails" vs "thin tails".

## Dependencies

The analysis requires the following Python libraries:
*   `numpy`
*   `pandas`
*   `yfinance`
*   `scipy`
*   `matplotlib`

## Usage

1.  Install the required dependencies:
    ```bash
    pip install numpy pandas yfinance scipy matplotlib
    ```
2.  Run the Jupyter Notebook `analysis.ipynb` to execute the simulation and view the results.

## Interpretation of Results

The notebook calculates the **0.1 percentile** outcome (a 1-in-1000 worst-case scenario) for both models.

*   **Normal Model**: Provides a worst-case price estimation based on standard market behavior.
*   **Student-t Model**: Provides a worst-case price estimation that accounts for "fat tails" (extreme events), typically resulting in a lower predicted price (higher loss) than the Normal model.
