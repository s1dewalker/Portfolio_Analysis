![](screenshots/PRA.png)

Inspired by many **specialized ETFs** (An investment vehicle that pools a group of securities into a fund. It can be traded like an individual stock on an exchange). Creating a basket of stocks with weights for **specific investment strategies or weighting criteria beyond traditional market-capitalization indexes and treating them all as a unit.**
<br/>

A portfolio, if selected properly, is less vulnerable to extreme highs and lows, and provides the benefits of diversification.
<br/>
### [View Portfolio Analysis of US stocks with Python](https://github.com/s1dewalker/Portfolio_Analysis/blob/main/Portfolio_Analysis.ipynb) <br/>
### [Meet Min Volatility and Max Sharpe Ratio on the EfficientFrontier of NSE stocks](https://github.com/s1dewalker/Portfolio_Analysis/blob/main/ETFs.ipynb)
### [View Risk Analysis in Python](https://github.com/s1dewalker/Portfolio_Analysis/blob/main/py_files/RiskAnalysis.ipynb)
<br/> 

# 1. Data Extraction and Portfolio Construction <br/>
Utilized `yfinance` for data retrieval of NSE stocks, obtaining historical price data for a specified date range. <br/>
<br/>
'df' is the DataFrame that contains daily prices of stocks. <br/>
'weights' is the array that contains portfolio weights. <br/>
- `returns = df.pct_change()` <br/>
  `returns.dropna(inplace = True)`

Portfolio construction w/ stock returns
- `returns_pf = returns.dot(weights)`

Portfolio construction w/ stock values
- `pf_AUM = df.dot(weights)`
<br/>

# 2. Risk Analysis - Some Basic Portfolio Risk Metrics <br/>

## Annualized return <br/>

#### Q. Why annualize returns? <br/>
- To account for compounding effect
- To compare portfolios with different time periods
- Average return can be deceiving (example: if portfolio loses all its value in the end the average may be > 0%, but final return is 0%)
<br/>

Annualizing returns:
- `total_return = (pf_AUM[-1] - pf_AUM[0]) / pf_AUM[0]`
- `annualized_return = ((1 + total_return) * * (12 / months)) - 1`

## Annualized Volatility <br/>
- `pf_returns = pf_AUM.pct_change()`
- `pf_vol = pf_returns.std()`
- `pf_vol = pf_vol * np.sqrt(250)`

#### Q. Why multiply with sqrt(250)
250: trading days in a year (annual)
sqrt: variance annualized = 250 * variance daily. <br/>
Therefore, standard deviation annualized = sqrt(250) * standard deviation daily.
<br/>

## Risk-adjusted return | Sharpe Ratio | Efficiency of risk taking <br/>

- `sharpe_ratio = ((annualized_return - rfr) / pf_vol)`

## Portfolio Variance and Volatility <br/>

- `cov_matrix = (returns.cov())*250 ` 
- `port_variance = np.dot(weights.T, np.dot(cov_matrix, weights))`
- `port_standard_dev = np.sqrt(port_variance)`

[View Portfolio Variance derivation](https://github.com/s1dewalker/Portfolio_Analysis/blob/main/Portfolio_variance.pdf) <br/>

#### Q. Why annualizing covariance?
so that we calculate the annualized volatility later. <br/>

#### Q. Why portfolio variance formula instead of standard deviation?
**Precision**: As stocks are **correlated** to each other, we need to account for **correlations** b/w stocks. This gives more **precision** in measuring volatility. <br/>
It can be forward looking if covariance matrix is estimated or forecasted. <br/>

#### Q. Benefits of historical method?
Historical data method can include rebalancing. <br/>

## Skewness
Skewness measures the asymmetry of the distribution of data around its mean. <br/>
- `pf_returns.skew()`

Risk management: Investors should seek positive skew as in the long run: <br/>
few positive bets should create a positive expectancy <br/>

## Kurtosis
Kurtosis measures the "tailedness" of the data distribution, indicating the presence of outliers. <br/>
- `pf_returns.kurtosis()`
 
k>3: FAT (leptokurtic) | high risk-high reward

<br/> 

# 3. Risk Analysis - Value at Risk (VaR) <br/>

 Finding var95 and cvar95:<br/>
- `var = np.percentile(returns_pf, 5)`
- `cvar = returns_pf [returns_pf <= var].mean()`

<img src="screenshots/var2.JPG" alt="Description" width="500">


Monte Carlo Simulation:<br/>
<img src="screenshots/mcsim.JPG" alt="Description" width="500">

Monte Carlo VaR:<br/>
<img src="screenshots/mcvar.JPG" alt="Description" width="500">


### [View Complete Risk Analysis](https://github.com/s1dewalker/Portfolio_Analysis/blob/main/py_files/RiskAnalysis.ipynb) with 15 Portfolio Risk metrics including 5 VaR metrics
<br/> 

# 4. Factor Investing
**The Fama-French 3 factor model** tells us **what drives portfolio returns** and **quantifies their contributions**.
Risk management: 
- Identifies exposure to specific factors (size, value)
- Optimize portfolio by adjusting exposures
- Evaluate performance

### [View Factor Analysis of NSE stocks in Python](https://github.com/s1dewalker/Portfolio_Analysis/blob/main/py_files/Factor_Analysis.ipynb)
### [View Multi Factor Analysis of NYSE stocks in Python](https://github.com/s1dewalker/Portfolio_Analysis/blob/main/py_files/Multi_Factor_Analysis.ipynb)
<br/> 

# 5. Portfolio Optimization | Efficient Frontier

## Optimal weights <br/>

<img src="screenshots/op_wts.JPG" alt="Description" width="600">

## Efficient Frontier <br/>

<img src="screenshots/eff_front3.JPG" alt="Description" width="600">

**The efficient frontier is the set of portfolios that achieve the highest return for a given risk or the lowest risk for a given return, representing optimal diversification.** <br/>
[View Portfolio Optimization maths](https://github.com/s1dewalker/Portfolio_Analysis/blob/main/Portfolio_Optimization.pdf) <br/>
<br/>

### [View Complete Portfolio Optimization](https://github.com/s1dewalker/Portfolio_Analysis/blob/main/ETFs.ipynb) of NSE stocks

##### Python libraries: 
##### `pandas, numpy, yfinance, matplotlib, PyPortfolioOpt, EfficientFrontier` 
<br/>

*hope you find it helpful, and encourage you to forward any suggestions for improvements* <br/>
##### [LinkedIn](https://www.linkedin.com/in/sujay-bhaumik-d12/)
