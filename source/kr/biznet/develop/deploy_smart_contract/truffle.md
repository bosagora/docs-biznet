# **Truffle 사용하기**

## **개발 환경 설정**

### 요구 사항

시작하기 전에 몇 가지 기술 요구 사항이 있습니다. 다음을 설치하십시오: 

- Windows, Linux or Mac OS X
- [Node.js v8.9.4 LTS or later](https://nodejs.org/en/)
- [Git](https://git-scm.com/)

#### Windows에 대한 권장 사항
Windows에서 Truffle을 실행하는 경우 Truffle이 제대로 실행되지 않도록 하는 몇 가지 이름 충돌이 발생할 수 있습니다. 솔루션에 대한 이름 충돌 해결에 대한 섹션을 참조하십시오.

### Truffle 설치하기

다음 명령어를 실행하면 됩니다.
```shell
npm install -g truffle
```

Truffle이 제대로 설치되었는지 확인하려면 **truffle version** 터미널에 입력하십시오. 오류가 표시되면 npm 모듈이 경로에 추가되었는지 확인하십시오.

## **프로젝트 생성, 컴파일 및 구성**

첫 번째 단계는 Truffle 프로젝트를 만드는 것입니다. 계정 간에 전송할 수 있는 토큰을 생성하는 **MegaCoin** 을 예로 사용하겠습니다.

### Truffle 프로젝트를 위한 새 디렉토리 생성

```shell
mkdir MegaCoin
cd MegaCoin
```

### 프로젝트 초기화

프로젝트를 초기화하려면 다음 명령을 사용하십시오.

```shell
truffle init
```

이 작업이 완료되면 이제 다음 항목이 포함된 프로젝트 구조가 생성됩니다.

* Contracts/: Solidity 컨트랙트 디렉토리
* 마이그레이션/: 스크립팅 가능한 배포 파일의 디렉터리
* test/: 애플리케이션 및 계약을 테스트하기 위한 테스트 파일 디렉토리
* truffle-config.js: 트러플 구성 파일

### 스마트 컨트랙트 생성하기

자신의 스마트 계약을 작성하거나 ERC20 토큰 스마트 컨트랙트 템플릿을 다운로드할 수 있습니다.

### 스마트 컨트랙트 컴파일하기

Truffle 프로젝트를 컴파일하려면 프로젝트가 있는 디렉토리의 루트로 변경한 후 터미널에 다음을 입력하십시오.

```shell
truffle compile
```


### BizNet용 Truffle 구성

- truffle-config.js 파일을 오픈합니다.
- truffle-config.js 파일의 다음과 같이 수정합니다.

```js
const HDWalletProvider = require('@truffle/hdwallet-provider');
const fs = require('fs');
const mnemonic = fs.readFileSync(".secret").toString().trim();

module.exports = {
  networks: {
    development: {
      host: "127.0.0.1",     // Localhost (default: none)
      port: 8545,            // Standard RPC port (default: none)
      network_id: "*",       // Any network (default: none)
    },
    testnet: {
      provider: () => new HDWalletProvider(mnemonic, `https://testnet.bosagora.org`),
      network_id: 2019,
      confirmations: 10,
      timeoutBlocks: 200,
      skipDryRun: true
    },
    mainnet: {
      provider: () => new HDWalletProvider(mnemonic, `https://mainnet.bosagora.org/`),
      network_id: 2151,
      confirmations: 10,
      timeoutBlocks: 200,
      skipDryRun: true
    },
  },

  // Set default mocha options here, use special reporters etc.
  mocha: {
    // timeout: 100000
  },

  // Configure your compilers
  compilers: {
    solc: {
      version: "^0.6.12", // A version or constraint - Ex. "^0.5.0"
    }
  }
}
```

참고로 제공자에 대해 니모닉을 전달해야 하며 이는 배포하려는 계정의 시드 구문입니다. 루트 디렉터리에 새 .secret 파일을 만들고 시작하려면 12단어 니모닉 시드 구문을 입력하세요. 메타마스크 지갑에서 시드워드를 얻으려면 메타마스크 설정으로 이동한 다음 메뉴에서 보안 및 개인정보 보호를 선택하면 시드 단어 공개라는 버튼이 표시됩니다.

## **BizNet에 배포하기**

프로젝트 디렉터리의 루트에서 다음 명령을 실행합니다.
```jsshell
truffle migrate --network testnet
```

스마트컨트랙트는 BizNet Testnet에 배포되며 다음과 같습니다.

```
1_initial_migration.js
======================

   Deploying 'Migrations'
   ----------------------
   > transaction hash:    0xaf4502198400bde2148eb4274b08d727a17080b685cd2dcd4aee13d8eb954adc
   > Blocks: 3            Seconds: 9
   > contract address:    0x81eCD10b61978D9160428943a0c0Fb31a5460466
   > block number:        3223948
   > block timestamp:     1604049862
   > account:             0x623ac9f6E62A8134bBD5Dc96D9B8b29b4B60e45F
   > balance:             6.24574114
   > gas used:            191943 (0x2edc7)
   > gas price:           20 gwei
   > value sent:          0 ETH
   > total cost:          0.00383886 ETH

   Pausing for 5 confirmations...
   ------------------------------
   > confirmation number: 2 (block: 3223952)
   > confirmation number: 3 (block: 3223953)
   > confirmation number: 4 (block: 3223954)
   > confirmation number: 6 (block: 3223956)

   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:          0.00383886 ETH


Summary
=======
> Total deployments:   1
> Final cost:          0.00383886 ETH
```

> 귀하의 주소, transaction_hash 및 기타 제공된 세부 정보가 다를 수 있음을 기억하십시오. 위는 구조에 대한 아이디어를 제공하기 위한 것입니다.

**축하합니다!** ERC20 스마트 계약을 성공적으로 배포했습니다. 이제 스마트 계약과 상호 작용할 수 있습니다.

배포 상태는 다음 URL에서 확인할 수 있습니다.  <https://scan.bosagora.org/> 또는 <https://testnet-scan.bosagora.org/>

