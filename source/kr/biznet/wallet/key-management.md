# **키 관리**

이 문서는 BizNet에서 분산된 애플리케이션의 클라이언트 측 키 관리 전략에 대한 가이드입니다.

## **Web3 설정하기**

`web3.js`는 클라이언트 측 애플리케이션이 블록체인과 대화할 수 있도록 하는 자바스크립트 라이브러리입니다.
메타마스크를 통해 통신할 수 있도록 web3를 구성하여야 합니다.

`web3.js` 에 대한 자세한 설명은 [이곳](https://web3js.readthedocs.io/en/v1.2.2/getting-started.html#adding-web3-js) 을 참조해 주십시오.

## **BizNet에 연결하기**

```javascript
    // mainnet 
     const web3 = new Web3('https://mainnet.bosagora.org');
    // testnet
	const web3 = new Web3('https://testnet.bosagora.org');
```

## **계정 설정하기**
web3의 설치 및 인스턴스화에 성공하였다면, 아래 코드는 임의의 계정을 리턴하는 것입니다.
```javascript
    const account = web3.eth.accounts.create();
```

## **계정 복구하기**

계정의 개인 키를 백업한 경우 그 개인키를 사용하여 계정을 복원할 수 있습니다.
```javascript
	const account = web3.eth.accounts.privateKeyToAccount("$private-key")
```

## **전체코드**
```javascript
const Web3 = require('web3');
async function main() {

	const web3 = new Web3('https://mainnet.bosagora.org:443');
    const loader = setupLoader({ provider: web3 }).web3;

    const account = web3.eth.accounts.create();
    console.log(account);
}
```