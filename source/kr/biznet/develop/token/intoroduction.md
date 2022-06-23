# ERC20 토큰 소개

ERC20 토큰은 파일 [IERC20.sol](../IERC20.sol)내의 IERC20의 인터페이스 를 구현해야 합니다.
이것은 템플릿 계약 [ERC20Token.template](../ERC20Token.template) 입니다
사용자 는 자신의 요구 사항에 따라 `_name`, `_symbol`, `_decimals`, `_totalSupply` 를 입력하기만 하면 됩니다.
```
  constructor() public {
    _name = {{TOKEN_NAME}};
    _symbol = {{TOKEN_SYMBOL}};
    _decimals = {{DECIMALS}};
    _totalSupply = {{TOTAL_SUPPLY}};
    _balances[msg.sender] = _totalSupply;

    emit Transfer(address(0), msg.sender, _totalSupply);
  }
```
그런 다음 사용자는 [Remix IDE](https://remix.ethereum.org) 및 [Metamask](../../wallet/tutorials/metamask.md) 를 사용하여 ERC20 계약을 컴파일하고 BizNet에 배포할 수 있습니다.

## [Web3](https://www.npmjs.com/package/web3) 및 NodeJS 를 사용하여 Contract와 상호 작용

### BizNet의 공용 RPC 연결

```js
const Web3 = require('web3');
// mainnet
const web3 = new Web3('https://mainnet.bosagora.org');

// testnet
const web3 = new Web3('https://testnet.bosagora.org');
```

### 지갑 만들기

```javascript
web3.eth.accounts.create([entropy]);

```
Output:
```bash
web3.eth.accounts.create();
{
  address: '0x926605D0729a968266f1BB299d8Df0471C4F5367',
  privateKey: '0x6b4618539d95f205f33e916e89404b301dde545c0c4acc181fd0c0b42708bad3',
  signTransaction: [Function: signTransaction],
  sign: [Function: sign],
  encrypt: [Function: encrypt]
}

```

### 지갑 복구

```javascript

const account = web3.eth.accounts.privateKeyToAccount("0xe500f5754d761d74c3eb6c2566f4c568b81379bf5ce9c1ecd475d40efe23c577")

```


### 잔액 확인

```javascript
web3.eth.getBalance(holder).then(console.log);

```

Output:

The balance will be bumped by e18 for BOA.

```
6249621999900000000
```

### 트랜잭션 생성

**파라메타**

* Object - 보낼 트랜잭션 개체:
* from - String|Number: 보내는 계정의 주소입니다. 지정하지 않은 경우 web3.eth.defaultAccount 속성을 사용합니다. 또는 web3.eth.accounts.wallet에 있는 로컬 지갑의 주소 또는 인덱스
* to - String: (선택 사항) 메시지의 대상 주소입니다. 컨트랙트 생성을 위한 트랜잭션에서는 정의하지 않습니다.
* value - Number|String|BN|BigNumber: (선택 사항) 트랜잭션을 통해 전송된 BOA이며 그것의 단위는 10^-18입니다. 계약 생성 트랜잭션인 경우에는 기부금입니다.
* gas - Number: (선택 사항, default: To-Be-Determined) 거래에 사용할 가스의 양(사용하지 않은 가스는 환불됨).
* gasPrice - Number|String|BN|BigNumber: (선택 사항) 이 트랜잭션에 대한 가스 가격이며 그것의 단위는 10^-15입니다., 기본값은 web3.eth.gasPrice입니다.
* data - String: (선택 사항) 계약에 대한 함수 호출 데이터를 포함하는 ABI 바이트 문자열 또는 계약 생성 트랜잭션의 경우 초기화 코드입니다.
* nonce - Number: (선택 사항) nonce의 정수입니다. 이를 통해 동일한 nonce를 사용하는 보류 중인 트랜잭션을 덮어쓸 수 있습니다.

```Javascript

	// // Make a transaction using the promise
	web3.eth.sendTransaction({
	    from: holder,
	    to: '0x0B75fbeB0BC7CC0e9F9880f78a245046eCBDBB0D',
	    value: '1000000000000000000',
	    gas: 5000000,
        gasPrice: 18e9,
	}, function(err, transactionHash) {
      if (err) {
        console.log(err);
        } else {
        console.log(transactionHash);
       }
    });
```


