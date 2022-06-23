# Use MetaMask For BizNet

**Tip**  
If you encounter any network configuration issues in MetaMask, please make sure you have the latest version running.

## What is it?

MetaMask was created out of the needs of creating more secure and usable Ethereum-based web sites. In particular, it handles account management and connecting the user to the blockchain.
It’s supported in Chrome, Chrome, and Safari browsers.
## Install

**Example: Install MetaMask in Chrome browser**

* Open Extension Category in Chrome: https://chrome.google.com/webstore/category/extensionsSearch for MetaMask

![img](assets/metamask01.png)

**warning**   
Note: Make sure it’s offered by metamask.io

* Click on "Add to Chrome"

That’s it! You have successfully installed MetaMask extension in Chrome!

![img](assets/metamask02.png)

**Tip**  
The workflow is the same for all browsers

## Create an account in MetaMask for BizNet

1. Click on the "Create a wallet" button

![img](assets/metamask03.png)

2. Create Password of at least 8 characters

![img](assets/metamask04.png)

3. Click on "Create" and then write down your backup phrase.

![img](assets/metamask05.png)

4. Select each phrase in order to make sure it is correct then click "Confirm".

![img](assets/metamask06.png)

Congratulations! you have creat your MetaMask account!

## Connect Your MetaMask With BizNet

1. Go to setting page

![img](assets/metamask07.png)

2. Add a new network

![img](assets/metamask08.png)

* Testnet
  * [RPC URLs](./../../develop/rpc.md)
  * ChainID: 0x7E3 (2019 in decimal)
  * Symbol: BOA
  * [Block Explorer](https://testnet-scan.bosagora.org)

* Mainnet
  * [RPC URLs](./../../develop/rpc.md)
  * ChainID: 0x867 (2151 in decimal)
  * Symbol: BOA
  * [Block Explorer](https://scan.bosagora.org)

3. Claim some testnet token to your account. Click on your address for copy

![img](assets/metamask09.png)

1. Go to faucet page: https://faucet.bosagora.org/request/boa/your-address

**Tip**  
Please note that you can only claim once every minute

After the transfer transaction is sent, you will see an increase of your balance

![img](assets/metamask10.png)

## Transfer BOA to other BizNet address

1. Log in to your MetaMask


2. Click on Send button

![img](assets/metamask11.png)

3. Copy the receiver’s address in the box

![img](assets/metamask12.png)

4. Input the amount

![img](assets/metamask13.png)

5. Confirm your transaction, then click Next

![img](assets/metamask14.png)

6. Click Confirm to send your transaction

![img](assets/metamask15.png)

7. Wait for your transaction to be included in the new block

![img](assets/metamask16.png)

8. Once your transaction is confirmed, check it on block explorer by clicking Details

![img](assets/metamask17.png)

9.  Click on your account to see "Details''

![img](assets/metamask18.png)

10. Verify your transaction in Explorer:

![img](assets/metamask19.png)

## Add ERC20 Tokens
1. Deploy an ERC20 contract at https://remix.ethereum.org/

2. You can create a new file or import a sample contract: <https://gist.github.com/dev-bosagora/5e06fc7357604f900c2d81e0f6f0ad75>

![img](assets/metamask41.png)

![img](assets/metamask42.png)

3. Connect your BizNet Account to Remix

![img](assets/metamask43.png)

4. Select "SampleToken" contract and compile

![img](assets/metamask44.png)

5. Deploy your compiled contract

![img](assets/metamask45.png)

6. Adjust Gas Fee for your contract, then confirm your deployed contract

![img](assets/metamask45.png)

7. You can see that there is a new creat contract transaction in block explorer

![img](assets/metamask19.png)

8. In MetaMask, Click on "Import Tokens"

![img](assets/metamask46.png)

9. Choose "Custom Token" and copy the contract address in the box

![img](assets/metamask47.png)

10.  Click on "Add Custom Tokens"

![img](assets/metamask48.png)

Then you can see change of your balance

![img](assets/metamask49.png)
![img](assets/metamask50.png)

## Create Multiple Accounts

1. To create multiple accounts, you click on Profile icon on MetaMask and then click on Create Account

![img](assets/metamask30.png)

2. You can then add an account name and click on Create.

![img](assets/metamask31.png)

3. Then you can see a new account is created!

![img](assets/metamask32.png)
