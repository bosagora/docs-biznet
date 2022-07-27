# Swap Guide

Token swapping in BOASwap is a simple way to exchange one ERC-20 token with another.

The user selects an input token and an output token.
This specifies the input amount and the protocol calculates the amount of output tokens they will receive.
Then, run the swap with one click and immediately receive the output token in your wallet.

BOASwap does not use orders to indicate liquidity or determine prices.
BOASwap uses an automated market maker mechanism to provide instant feedback on exchange rates and Sleepy.
Each pair of BOASwap is actually supported by a pool of liquidity.
A liquidity pool is a smart contract that holds the balance of two unique tokens and enforces the rules associated with depositing and withdrawing them.

### BOASwap DEX Protocol Overview
- Our BOASwap DEX Protocol basically follows Uniswap V2. BOASwap Protocol is a binary smart contract system.
  BOASwap Interfaces allow you to interact with the BOASwap DEX Protocol directly with smart contracts without relying on intermediaries or requiring permissions.

#### Fees
- The token exchange fees is 1.5%. This fees is split to the liquidity providers in proportion to their contributions to the liquidity reserve.
  The exchange fees is immediately deposited to the liquidity reserve, which increases the value of the liquidity token and is used as a payment to all liquidity providers proportional to their share of the pool.
  The liquidity provider fees are collected by burning liquidity tokens and eliminating a proportional share of the underlying reserve.
  A protocol fees of 0.5% per transaction is applied to the liquidity providers. This is 1/3 of the token exchange fee.
  This fees does not affect the fees paid by traders, but it does affect the amount received by the liquidity providers.
  The protocol fees is calculated when liquidity is added or removed instead of calculating swap costs that can significantly increase gas costs for all users.