# Pool

- The BOASwap Pool is a liquidity pool for the BOASwap DEX Protocol.
  Each BOASwap Liquidity Pool is a trading place for a pair of ERC20 tokens.
  For Pool to facilitate transactions, someone must supply the pool with an initial deposit of each token. This sets the initial price of the pool.
  Pool is a smart contract operated by a user invoking a function and invokes the function 'deposit' when providing liquidity.

- When other liquidity providers add to an existing pool, they must deposit pair tokens in proportion to the current price.
  Otherwise, the added liquidity also risks arbitrage. If you decide that the current price is not correct, you can make a profitable profit and add liquidity to that price.

  ![img](assets/pool-0.png)
