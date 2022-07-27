# Introduction of BOASwap

## What is BOASwap ?

The areas provided by BOASwap can be divided into My Assets, Swap, Pool, and Bridge.

First, let’s explain the names used in the BOASwap.

- BizNet : It is a reliable BOASAGORA blockchain network composed of multiple nodes that achieve consensus with the POA consensus algorithm. Smart contracts can be executed with BizNet’s Ethereum Virtual Machine (EVM) support, so compatible DApps running on Ethereum can also be contracted on BizNet.

- BOASwap DEX Protocol : A continuous, non-upgradable smart contract that creates an automated market maker  facilitating the formation and exchange of the P2P market for ERC-20 tokens on Agora BizNet.

- BOASwap Bridge Protocol : An atomic swap smart contract that allows reliable swaps between Ethereum Mainnet and Agora BizNet. Coins can be swapped while fixing the supply of BOA coins through pegging and de-pegging.

- BOASwap Bridge relay node : It operates as a bridge relay node connected to each network of Ethereum Mainnet and Agora BizNet. It supports atomic swap of bridge protocols to run on each network.

- BOASwap Interfaces: Web interface that allows easy interaction with BOASwap DEX Protocol and Bridge Protocol. The interface is one of many ways to interact with BOASwap protocols.


## BOASwap

### My Assets
The assets shown here show the coins and tokens that you have on the network that you are currently connected to.
Tokens and points that can be displayed are tokens with the ERC-20 token standard and they can be trusted if they are managed in a separate list.
In order for My Assets to display the tokens you have, your Metamask wallet must be connected to the Agora BizNet network. You must also have a trusted connection with BOASwap.

### Swap
Token swapping in BOASwap is a simple way to exchange one ERC-20 token with another.
The user selects an input token and an output token. This specifies the input amount and the protocol calculates the amount of output tokens they will receive.
You can then run the swap with a single click and receive the output token in your wallet immediately.

### Pool
The BOASwap Pool is a liquidity pool for the BOASwap DEX Protocol.
Each BOASwap Liquidity Pool is a trading place for a pair of ERC20 tokens.
For Pool to facilitate transactions, someone must supply the pool with an initial deposit of each token. This sets the initial price of the pool.

### Bridge
It connects Ethereum Mainnet and BizNet blockchain and allows an intermediary transaction.
Currently, BOA tokens are supported for coin transfer from Ethereum Mainnet to BizNet, and this transaction is possible for two-way transactions (two-way pegging).

### BOA
* Ethereum MainNet ERC20 BOA : [0x746DdA2ea243400D5a63e0700F190aB79f06489e](https://etherscan.io/token/0x746dda2ea243400d5a63e0700f190ab79f06489e) It is an ERC20 smart contract token on the Ethereum network and is currently listed on the Coin Exchange.
* BOSAGORA BizNet BOA : It is the default currency for BizNet networks and is used for value exchange and network gas fee.
* Ethereum MainNet ERC20 BOA and BizNet BOA exchange rate is 1BOA = 1BOA
