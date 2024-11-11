# ETF Portfolio and Risk Analysis
## [Portfolio Analysis with Python](https://github.com/s1dewalker/Portfolio_Analysis/blob/main/Portfolio_Analysis.ipynb) <br/>
## [Portfolio Analysis & EfficientFrontier ETFs of NSE stocks](https://github.com/s1dewalker/Portfolio_Analysis/blob/main/ETFs.ipynb)
<br/> 

## Value at risk | Historical (VaR) | Expected Shortfall (CVaR) <br/>
'df' is the DataFrame that contains daily prices of stocks. <br/>
'weights' is the array that contains portfolio weights. <br/>
 Finding var95 and cvar95 (4 steps):<br/>
> ### 1) returns = df.pct_change()
> returns.dropna(inplace = True)
> ### 2) returns_pf = returns.dot(weights)
> ### 3) var = np.percentile(returns_pf, 5)
> ### 4) cvar = returns_pf [returns_pf <= var].mean()
