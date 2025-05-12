# black-scholes-model
Attempting to build a Black-Scholes option pricer.
## needed context
* call options: financial contracts that give the buyer the right (but not obligation) to buy an asset at a specified price in a specific period
  * contract between a buyer/seller
  * buyer has a right to buy the underlying asset at the strike price
  * there is an expiration date on/before which the option must be exercised
  * the buyer pays a premium to the seller for this right
## notes on model and implementation
* People had been trading stock options for a while, but no mathematical way to value an option
* No analytical framework, but general feeling of values

* s_0 = stock price
* x = exercise price
* r = risk-free interest rate
* T = time to expiration
* σ = standard deviation of log returns (volatility)
  *   Here, S2 is more volatile (will have a higher σ) than S1 - looking at how dispersed the returns are away from their mean
      ![image](https://github.com/user-attachments/assets/28580b97-d5e1-4593-ac74-3cc43550bbb2)
  * Would drive the value of an option up

* For a European call option:
  ![image](https://github.com/user-attachments/assets/7bd24f7a-8340-4644-8b4d-6eb1d42f3d54)
