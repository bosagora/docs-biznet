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

#### Fee
- The token exchange fee is 1.5%. This fee is split to the liquidity provider in proportion to its contribution to the liquidity reserve.
  The exchange fee is immediately deposited as a liquidity reserve, which increases the value of the liquidity token and is used as a payment to all liquidity providers proportional to the pool's share.
  Fees are collected by incinerating liquidity tokens and eliminating a proportional share of reserves.
  A protocol fee of 0.5% per transaction is applied. This is 1/3 of the token exchange fee.
  This fee does not affect the fees paid by the trader, but it does affect the amount received by the liquidity provider.
  Cost is calculated when liquidity is added or removed instead of calculating swap costs that significantly increase gas costs for all users.
