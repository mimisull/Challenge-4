# Challenge-4
The Directory for this respoitory is:
[Summary](https://github.com/mimisull/Challenge-4/blob/main/README.md)
[Code](https://github.com/mimisull/Challenge-4/blob/main/risk_return_analysis.ipynb)
**Quantitative Analysis for FinTech Investing Platform**
Specifically, I am finding investment opportunities for clients through our investing solution so that they can place their retirement portfolios in inexpensive and high quality funds. Using simple algorithms, I build client portfolios. We are now determining which of four very large investment insitutions that we want to include.

*User Story*:
As a user, I need to determine the fund with the most investment potential based on key risk-management metrics: the daily returns, standard deviations, Sharpe ratios, and betas.

*Acceptance Criteria*:
Given that I’m unable to determine which fund to include by normal overview of strategy, I need to use quantitative analysis to determine the best choice based on the criteria above.


## Usage
The project works by cleaning the data, importing the CSV files, and comparing performance listed by trading day.
Imported the necessary tools with this code:
'''import pandas as pd
from pathlib import Path
import numpy as np
%matplotlib inline'''

Collected the data via this code:
'''whale_nav = pd.read_csv(Path('./Resources/whale_navs.csv'),
                        index_col='date',parse_dates=True, infer_datetime_format=True)'''

Determined percent change with this code:
'''whale_nav_daily_returns = whale_nav.pct_change().dropna()'''

Determined cumulative return with this code:
'''whale_nav_cumulative_return = (1 + whale_nav_daily_returns).cumprod()'''

Found standard deviation, and annual standard deviation with this code:
'''trading_days = 252
annual_standard_deviation = whale_nav_daily_returns.std() * np.sqrt(trading_days)
annual_standard_deviation.sort_values()'''

Found annual average return with this code:
'''annual_average_return = whale_nav_daily_returns.mean() * trading_days
annual_average_return.sort_values()'''

Sharpe ratios:
'''whale_nav_sharpe_ratios = annual_average_return / annual_standard_deviation
whale_nav_sharpe_ratios.sort_values()'''

Variance:
'''market_variance = whale_nav_daily_returns['S&P 500'].rolling(window=60).var()'''

Specific company comparison:
'''berkshire_covariance = whale_nav_daily_returns['BERKSHIRE HATHAWAY INC'].rolling(window=60).cov(whale_nav_daily_returns['S&P 500'])'''
'''berkshire_beta = berkshire_covariance / market_variance'''

And determined that Berkshire Hathaway was the correct company to include in the portfolio.

## Contributors
Michael Sullivan

Cal Berkeley Fintech 

Kevin Lee