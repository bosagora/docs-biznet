# Issue ERC20 Tokens

## **Compile and Deploy ERC20 Contract**

1. Open Remix IDE: [https://remix.ethereum.org](https://remix.ethereum.org/)
   ![img](issue_erc20_1.png)

2. Select solidity language
   ![img](issue_erc20_2.png)

3. Create new contract ERC20Token.sol and copy contract code from the ERC20 token template [here](../ERC20Token.template)

4. Modify “name”, “symbol”, “decimals” and “totalSupply” according to your requirements.
   ![img](issue_erc20_3.png)

5. Compile the ERC20 token contract   
   a. Step1: Click button to switch to compile page  
   b. Step2: Select “ERC20Token” contract  
   c. Step3: Enable “Auto compile” and “optimization”  
   d. Step4: Click “ABI” to copy the contract abi and save it.  
   ![img](issue_erc20_4.png)

6. Deploy the contract to BizNet  
   a. Step1: Click button to switch to compile button.  
   b. Step2: Select “Injected Web3”  
   c. Step3: Select “ERC20Token”  
   d. Step4: Client “Deploy” button and Metamask will pop up  
   ![img](issue_erc20_5.png)
   e. Client “confirm” button to sign and broadcast transaction to BizNet.
   ![img](issue_erc20_6.png)
