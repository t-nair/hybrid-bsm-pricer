# black-scholes-model
Attempting to build a Black-Scholes option pricer.
## needed context
* Call options: give the right (but not obligation) to buy an asset 
* Put options: give the right to sell the asset
* European options (represented by lowercase c for call and lowercase p for put): can only be exercised at the expiration date
* American options (represented by uppercase C for call and uppercase P for put): can be exercised at any time before/on the expiration date
* The values of call/put options differ depending on whether they're American or European -- American options provide more freedom, and are therefore at least equal to (often higher than) the value of their European counterpart 
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
