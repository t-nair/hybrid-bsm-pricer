# hybrid-bsm-pricer
Attempting to build an augmented Black-Scholes option pricer that:
 1. Learns and corrects for residual pricing errors using real market data.
 2. Replaces the constant volatility term with a fused, dynamic volatility estimate: using both GARCH and a RNN.
 3. Identifies and compensates for sudden discontinuities in price dynamics with a jump detection module.
## formula
[hybrid-bsm-math.ipynb](https://github.com/t-nair/hybrid-bsm-pricer/blob/main/hybrid_bsm_math.ipynb)
## components
* BSM engine implemented in Python: modular to swap volatility term
* Fused volatility estimator
 * Inputs: past returns, volatility index, technical indicators, macro signals
 * Outputs: volatility from GARCH, volatility from RNN
* Fusion layer combines outputs into one volatility metric - linear regressor with weights for GARCH vs. RNN outputs based on recent market conditions
* Residual correction module using MLP to predict error
* Jump detection module
 * When jump detected: adds a small correction term to the price
# notes
## basic info
* Stock: (a.k.a. equity) security that represents the ownership of a fraction of the issuing corporation
 * Units of stock are called shares: they entitle the owner to a portion of the corporation's profits equal to the number of shares owned
 * Bough and sold predominantly on public exchanges
* Shareholder: person/company/institution that owns at least one share of a company's stock
* Options: contract that gives an investor a right to buy/sell a stock/ETF at an agreed-upon strike price for a specific period of time
 * Financial derivatives: derive their value from the underlying security/stock
 * Have a cost associated with them (premium) and an expiration date
* Call options: give the right (but not obligation) to buy an asset
 * Profitable when the strike price is below the stock's market price, since the trader can buy the stock at a lower price
* Put options: give the right to sell the asset
 * Profitable when the strike price is higher than the stock's 
* European options (represented by lowercase c for call and lowercase p for put): can only be exercised at the expiration date
* American options (represented by uppercase C for call and uppercase P for put): can be exercised at any time before/on the expiration date
* The values of call/put options differ depending on whether they're American or European -- American options provide more freedom, and are therefore at least equal to (often higher than) the value of their European counterpart 
### black-scholes model and implementation
* People had been trading stock options for a while, but no mathematical way to value an option
* No analytical framework, but general feeling of values
### assumptions
* Assumes option prices exhibit Brownian motion
* Assumes risk-free rates are constant, when in reality, they're dynamic and fluctuate with supply and demand
* Assumes stock returns resemble a log-normal distribution
* Assumes we have a frictionless market and there are no transaction costs (not the case in the real world)
* Neglects dividend payouts throughout the option period
### formula
* Equation is a parabolic PDE
* Describes price V(S, t) of an option, where S is price of underlying asset and t is time
![image](https://github.com/user-attachments/assets/e078b874-112b-4390-8f6b-a038d4a5cca7)
* Key financial insight: one can perfectly hedge the option by buying/selling underlying asset and bank account asset to "eliminate risk", implying there's a unique price for the option given by the Black-Scholes formula
* Where K is the strike price of the option, S is the price of the underlying asset at time t, σ is the standard deviation of the stock's returns (volatility), T is the time of option expiration, t is a time in years (with t = 0 generally representing the present year), r is the annualized risk-free interest rate (continuously compounded, a.k.a. force of interest), and N is the standard normal cumulative distribution function:
![image](https://github.com/user-attachments/assets/be7ed181-1365-4dbc-8baa-b1990a638c99)
* For a European call option C(S, t):
![image](https://github.com/user-attachments/assets/096b0ff5-d827-447a-9a1f-41fbe77bf75e)
* For a European put option P(S, t):
![image](https://github.com/user-attachments/assets/04e00ea3-2da0-4ae6-b187-0af7a559310a)
### in practice
* Not all assumptions of the model are empirically valid
* Useful approximation IF you understand the risks
* Most significant limitations include:
  * Underestimation of extreme moves, which yields tail risk (can be hedged with out-of-the-money options)
  * Assumption of instant, cost-less trading, which yields liquidity risk (difficult to hedge)
  * Assumption of a stationary process, which yields volatility risk (can be hedged with volatility hedging)
  * Assumption of continuous time/trading, which yields gap risk (can be hedged with Gamma hedging)
  * Model tends to underprice deep out-of-the-money options and overprice deep in-the-money options 



