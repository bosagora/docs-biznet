# **Hardhat 사용하기**

## **Hardhat 이란?**

Hardhat은 스마트 계약을 컴파일, 배포, 테스트 및 디버그하기 위한 개발 환경입니다.

## **요구 사항:**

시작하기 전에 몇 가지 기술 요구 사항이 있습니다. 다음을 설치하십시오: 

- Windows, Linux or Mac OS X
- [Node.js v8.9.4 LTS or later](https://nodejs.org/en/)
- [Git](https://git-scm.com/)


## **설치하기**

먼저 빈 프로젝트를 만들어야 합니다. `npm init --yes`
프로젝트가 준비되면 다음을 실행해야 합니다.
```shell
npm install --save-dev hardhat
```

일부 종속성을 설치합니다

```shell
npm install --save-dev @nomiclabs/hardhat-waffle ethereum-waffle chai @nomiclabs/hardhat-ethers ethers
```
Hardhat를 실행하기 위해서는 npx를 사용하여 실행해야 합니다(예: npx hardhat).

## **프로젝트 만들기**

Hardhat 프로젝트를 생성하려면 프로젝트 폴더에서 `npx hardhat`을 실행하십시오.

```shell
mkdir MegaCoin
cd MegaCoin
```

- 프로젝트 초기화:

```
$ npx hardhat
888    888                      888 888               888
888    888                      888 888               888
888    888                      888 888               888
8888888888  8888b.  888d888 .d88888 88888b.   8888b.  888888
888    888     "88b 888P"  d88" 888 888 "88b     "88b 888
888    888 .d888888 888    888  888 888  888 .d888888 888
888    888 888  888 888    Y88b 888 888  888 888  888 Y88b.
888    888 "Y888888 888     "Y88888 888  888 "Y888888  "Y888

Welcome to Hardhat v2.0.8

? What do you want to do? …
❯ Create a sample project
  Create an empty hardhat.config.js
  Quit
```

이 프로젝트가 초기화되면 이제 다음 항목이 있는 프로젝트 구조가 생깁니다.

* Contracts/: Solidity 컨트랙트 디렉토리
* scripts/: 스크립팅 가능한 배포 파일의 디렉터리
* test/: 애플리케이션 및 계약을 테스트하기 위한 테스트 파일 디렉토리
* hardhat-config.js: Hardhat 구성 파일


### 스마트 컨트랙트 생성

자신의 스마트 계약을 작성하거나 [ERC20 토큰 스마트 컨트랙트 템플릿](../ERC20Token.template)을 다운로드할 수 있습니다 .

### BizNet을 위한 Hardhat 구성하기

- 파일 hardhat.config.js 를 오픈합니다.
- 파일 hardhat.config.js 를 다음과 같이 수정합니다.

```js
require("@nomiclabs/hardhat-waffle");
require('@nomiclabs/hardhat-ethers');
const { mnemonic } = require('./secrets.json');

// This is a sample Hardhat task. To learn how to create your own go to
// https://hardhat.org/guides/create-task.html
task("accounts", "Prints the list of accounts", async () => {
  const accounts = await ethers.getSigners();

  for (const account of accounts) {
    console.log(account.address);
  }
});

// You need to export an object to set up your config
// Go to https://hardhat.org/config/ to learn more

/**
 * @type import('hardhat/config').HardhatUserConfig
 */
module.exports = {
  defaultNetwork: "mainnet",
  networks: {
  	localhost: {
      url: "http://127.0.0.1:8545"
    },
    hardhat: {
    },
    testnet: {
      url: "https://testnet.bosagora.org/",
      chainId: 2019,
      gasPrice: 20000000000,
      accounts: {mnemonic: mnemonic}
    },
    mainnet: {
      url: "https://mainnet.bosagora.org/",
      chainId: 2152,
      gasPrice: 20000000000,
      accounts: {mnemonic: mnemonic}
    }
  },
  solidity: {
  version: "0.5.16",
  settings: {
    optimizer: {
      enabled: true
    }
   }
  },
  paths: {
    sources: "./contracts",
    tests: "./test",
    cache: "./cache",
    artifacts: "./artifacts"
  },
  mocha: {
    timeout: 20000
  }
};

```

**참고**  
제공자에 대해 전달되는 니모닉이 필요합니다. 이는 배포하려는 계정의 시드 구문입니다. 루트 디렉토리에 새 .secret파일을 만들고 시작하려면 12단어 니모닉 시드 구문을 입력하십시오. 메타마스크 지갑에서 시드워드를 얻으려면 메타마스크 설정으로 이동한 다음 메뉴에서 보안 및 개인정보 보호를 선택하면 시드 단어 공개라는 버튼이 표시됩니다.

### 스마트 컨트랙트 컴파일하기

Hardhat 프로젝트를 컴파일하려면 프로젝트가 있는 디렉토리의 루트로 변경한 후 터미널에 다음을 입력하십시오.
```shell
npx hardhat compile
```


## **BizNet에 배포하기**

프로젝트 디렉터리의 루트에서 다음 명령을 실행합니다.
```shell
npx hardhat run --network testnet scripts/deploy.js
```

> 귀하의 주소, transaction_hash 및 기타 제공된 세부 정보가 다를 수 있음을 기억하십시오. 위는 구조에 대한 아이디어를 제공하기 위한 것입니다.

**축하합니다!** ERC20 스마트 계약을 성공적으로 배포했습니다. 이제 스마트 계약과 상호 작용할 수 있습니다.

배포 상태는 다음 URL에서 확인할 수 있습니다.  <https://scan.bosagora.org/> 또는 <https://testnet-scan.bosagora.org/>

