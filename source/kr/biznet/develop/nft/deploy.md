# **BizNet에 NFT 배포**

> 이 문서는 [이 블로그](https://forum.openzeppelin.com/t/draft-create-an-nft-and-deploy-to-a-public-testnet-using-truffle/2961)를 참고하여 작성되었습니다.

이 튜토리얼에서는 NFT(Non-Fungible Token)를 생성하고 공개 테스트넷에 배포할 것입니다.

ERC721은 부동산이나 수집품과 같이 각 토큰이 고유한 [대체 불가능한 토큰](https://docs.openzeppelin.com/contracts/3.x/tokens#different-kinds-of-tokens) 의 소유권을 나타내는 표준입니다 .

[OpenZeppelin](https://docs.openzeppelin.com/contracts/3.x/) 계약에서 [Presets](https://docs.openzeppelin.com/contracts/3.x/api/presets)을 사용 하여 ERC721을 만들고 Truffle을 사용하여 배포합니다.

## **환경 설정**

우리는 새로운 프로젝트를 만드는 것으로 시작합니다.

```
$ mkdir mynft && cd mynft
$ npm init -y
```

그런 다음 ERC721 이 구현된 [OpenZeppelin Contracts](https://docs.openzeppelin.com/contracts)를 설치합니다.

```
$ npm i --save-dev @openzeppelin/contracts
```

다음으로 배포용 개발 도구를 설치합니다. 이 자습서에서는 [Truffle](https://www.trufflesuite.com/) 하용하지만 Remix 또는 [OpenZeppelin CLI](https://docs.openzeppelin.com/cli) 와 같은 다른 도구를 사용할 수도 있습니다 .

```
$ npm i truffle
```

## **스마트 컨트랙트 Artifacts 가져오기**

명령어 `truffle init` 이것을 사용하여 프로젝트를 구성할 것입니다.

```
$ npx truffle init
Starting init...
================

> Copying project files to

Init successful, sweet!
```

우리는 Preset [`ERC721PresetMinterPauserAutoId`](https://docs.openzeppelin.com/contracts/3.x/api/presets#ERC721PresetMinterPauserAutoId)를 사용할 것입니다.
이것은 발행, 일시 중지, 소각기능이 포함되어있는 ERC721입니다.
`Preset` 계약은 이미 컴파일되었으므로 아티팩트만 build/contracts 디렉터리에 복사하면 됩니다.

```
$ mkdir -p build/contracts/
$ cp node_modules/@openzeppelin/contracts/build/contracts/* build/contracts/
```

`migrations` 폴더안에 편집기를 사용 하여 다음 내용으로 파일 `2_deploy.js`를 생성합니다.

```
// migrations/2_deploy.js
// SPDX-License-Identifier: MIT
const ERC721PresetMinterPauserAutoId = artifacts.require("ERC721PresetMinterPauserAutoId");

module.exports = function(deployer) {
  deployer.deploy(ERC721PresetMinterPauserAutoId, "My NFT","NFT", "http://my-json-server.typicode.com/huangsuyu/nft/tokens");
};
```

## **로컬 블록체인에 컨트랙트 배포**

개발을 위해 [`truffle develop`](https://www.trufflesuite.com/docs/truffle/reference/truffle-commands#develop)를 사용합니다.

- 다음을 사용하여 테스트넷 BOA를 요청하세요 https://faucet.bosagora.org/request/boa/:your-address


```
$ npx truffle develop
Truffle Develop started at http://127.0.0.1:9545/

Accounts:
(0) 0xc7e4bbc4269fdc62f879834e363173aee7895f45

Private Keys:
(0) ef424b4dc91a9c9d6c1fc4ae0a50ce80668f3a955a7e982584b45577e2c70e27

Mnemonic: mechanic cannon setup general indicate people notable frown poet friend credit true

⚠️  Important ⚠️  : This mnemonic was created for you by Truffle. It is not secure.
Ensure you do not use it on production blockchains, or else you risk losing funds.

truffle(develop)> migrate

Compiling your contracts...
===========================
> Compiling ./contracts/Migrations.sol
> Artifacts written to /Users/Documents/work/mynft/build/contracts
> Compiled successfully using:
   - solc: 0.5.16+commit.9c3226ce.Emscripten.clang

Starting migrations...
======================
> Network name:    'develop'
> Network id:      5777
> Block gas limit: 6721975 (0x6691b7)

1_initial_migration.js
======================

   Deploying 'Migrations'
   ----------------------
   > transaction hash:    0x9a17a50e6efd52ba3e55245c76c52b065d20587add45aee732c233987033e567
   > Blocks: 0            Seconds: 0
   > contract address:    0x77409B688eA5461078a31450F3138EA8324F72C9
   > block number:        1
   > block timestamp:     1604387655
   > account:             0xc7e4bBc4269fdC62F879834E363173aeE7895F45
   > balance:             99.99616114
   > gas used:            191943 (0x2edc7)
   > gas price:           20 gwei
   > value sent:          0 ETH
   > total cost:          0.00383886 ETH


   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:          0.00383886 ETH


2_deploy.js
===========

   Deploying 'ERC721PresetMinterPauserAutoId'
   ------------------------------------------
   > transaction hash:    0xc1a3994c2ad2ba706ac49934b4f480c7b3d9b94241f526afa2dfe91545145a4e
   > Blocks: 0            Seconds: 0
   > contract address:    0xEaB17D581552123695f03F12b09e378EE9463b44
   > block number:        3
   > block timestamp:     1604387655
   > account:             0xc7e4bBc4269fdC62F879834E363173aeE7895F45
   > balance:             99.92142266
   > gas used:            3694586 (0x385ffa)
   > gas price:           20 gwei
   > value sent:          0 ETH
   > total cost:          0.07389172 ETH


   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:          0.07389172 ETH


Summary
=======
> Total deployments:   2
> Final cost:          0.07773058 ETH

truffle(develop)>
```

마이그레이션을 사용하여 새로운 NFT를 개발 블록체인에 배포할 수 있습니다.

```
truffle(develop)> migrate

Compiling your contracts...
===========================
> Everything is up to date, there is nothing to compile.



Starting migrations...
======================
> Network name:    'develop'
> Network id:      5777
> Block gas limit: 6721975 (0x6691b7)


1_initial_migration.js
======================

   Replacing 'Migrations'
   ----------------------
   > transaction hash:    0x5d71b0a45a0fe20e2ca645393bb44b83fbd47351c009c48be0b8b84b610fb3b7
   > Blocks: 0            Seconds: 0
   > contract address:    0x3797c825cAC4a1FA765F6D8cd7787fB195849555
   > block number:        1
   > block timestamp:     1590736865
   > account:             0x0445c33BdCe670D57189158b88c0034B579f37cE
   > balance:             99.99671674
   > gas used:            164163 (0x28143)
   > gas price:           20 gwei
   > value sent:          0 ETH
   > total cost:          0.00328326 ETH


   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:          0.00328326 ETH


2_deploy.js
===========

   Replacing 'ERC721PresetMinterPauserAutoId'
   ------------------------------------------
   > transaction hash:    0x166d7b28f4afb949585b5a0e5b4151daa54acbcb70566b202fd62ab380a6650c
   > Blocks: 0            Seconds: 0
   > contract address:    0xDEE9411430c7Dd9b67fC6DA723DE729AdAB50AD7
   > block number:        3
   > block timestamp:     1590736866
   > account:             0x0445c33BdCe670D57189158b88c0034B579f37cE
   > balance:             99.92191642
   > gas used:            3697675 (0x386c0b)
   > gas price:           20 gwei
   > value sent:          0 ETH
   > total cost:          0.0739535 ETH


   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:           0.0739535 ETH


Summary
=======
> Total deployments:   2
> Final cost:          0.07723676 ETH
```

그런 다음 배포된 계약을 사용할 수 있습니다.

```
truffle(develop)> nft = await ERC721PresetMinterPauserAutoId.deployed()
undefined
```

## **토큰과 상호 작용**

`truffle develop`를 시작할 때 사용할 수 있는 계정이 표시되었습니다 

### 토큰 메타데이터

`name`, `symbol`, `baseURI` 와 같은 토큰 메타데이터를 읽기 위해 계약을 호출할 수 있습니다

```
truffle(develop)> await nft.name()
'My NFT'
truffle(develop)> await nft.symbol()
'NFT'
truffle(develop)> await nft.baseURI()
```

### 민트

발행자 역할이 있는 계정에서 지정된 계정으로 토큰을 발행하는 트랜잭션을 보낼 수 있습니다. 우리의 경우 발행자 역할이 부여된 토큰을 배포한 계정에서 발행합니다.

토큰 ID가 0인 NFT 1개를 발행합니다.

```
truffle(develop)> await nft.mint("0x0445c33bdce670d57189158b88c0034b579f37ce")
{ tx:
   '0xd301a60dbb8ac187687f6639f200d4e6f2cfa065923092b3940330e35a26421d',
  receipt:
   { transactionHash:
      '0xd301a60dbb8ac187687f6639f200d4e6f2cfa065923092b3940330e35a26421d',
     transactionIndex: 0,
     blockHash:
      '0x3ad3cfcb26da0c969e9d5a5414a5e90a91a3a862c9e9082afc38a0ec0f1a5d00',
     blockNumber: 5,
     from: '0x0445c33bdce670d57189158b88c0034b579f37ce',
     to: '0xdee9411430c7dd9b67fc6da723de729adab50ad7',
     gasUsed: 156470,
...
```

토큰의 소유자와 메타데이터에 대한 토큰 URI를 확인할 수 있습니다.

```
truffle(develop)> await nft.ownerOf(1)
'0x0445c33BdCe670D57189158b88c0034B579f37cE'
truffle(develop)> await nft.tokenURI(1)
```

## **메타데이터**

[EIP-721 2](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-721.md)
에는 가 포함된 선택적 메타데이터 확장 이 포함되어 있으며 name, symbol각 tokenID에 대해 a는 가 포함 tokenURI된 JSON 파일을 가리킬 수 있으며 , name주어진 토큰 ID에 대해서는 가 있습니다.descriptionimage

includes an optional **metadata extension** with a `name`, `symbol` and for each tokenID a `tokenURI` with can point to a JSON file with `name`, `description` and `image` for the given token ID.

이 메타데이터를 만들고 호스팅하는 방법은 사용자에게 달려 있습니다. 
필요에 따라 이동할 수 있도록 데이터를 호스팅하는 위치를 가리키도록 제어하는 도메인을 사용하는 것이 좋습니다.

이 자습서에서는 가짜 JSON 서버를 통해 액세스할 수 있는 GitHub 리포지토리에 단일 JSON 파일을 저장할 수 있는 [My JSON Server](https://my-json-server.typicode.com/) 를 사용합니다.

**경고** 프로덕션을 위해 토큰 수명 동안 존재할 수 있는 영구 위치에 메타데이터를 저장해야 합니다.

A sample JSON for tokenID 1 is:
[http://my-json-server.typicode.com/huangsuyu/nft/tokens/1](http://my-json-server.typicode.com/huangsuyu/nft/tokens/1)

## **테스넷에 배포하기**

다음으로 우리는 BizNet testnet에 배포할 것입니다.
배포하기 위해 Truffle을 사용하여 [공개 테스트 네트워크에 연결하기 위한 지침](https://forum.openzeppelin.com/t/connecting-to-public-test-networks-with-truffle/2960)을 사용합니다.

다음이 필요합니다.

- 테스트넷의 RPC URL
- `@truffle/hdwallet-provider` installed
- `truffle-config.js`를 테스트넷용으로 설정하기
- 자금 지원 테스트넷 계정 및 니모닉
- `secrets.json` 또는 다른 비밀 관리 솔루션입니다. **이것을 GitHub에 커밋하지 않았는지 확인하십시오!**

`truffle-config.js`는 다음과 같습니다.

```
     testnet: {
      provider: () => new HDWalletProvider(mnemonic, `https://testnet.bosagora.org`),
      network_id: 2019,
      confirmations: 10,
      timeoutBlocks: 200,
      skipDryRun: true
    },
    mainnet: {
      provider: () => new HDWalletProvider(mnemonic, `https://mainnet.bosagora.org`),
      network_id: 2151,
      confirmations: 10,
      timeoutBlocks: 200,
      skipDryRun: true
    },
```

### BizNet 테스트넷에 배포

```
$ npx truffle migrate --network testnet

Compiling your contracts...
===========================
> Everything is up to date, there is nothing to compile.

Starting migrations...
======================
> Network name:    'develop'
> Network id:      5777
> Block gas limit: 6721975 (0x6691b7)


1_initial_migration.js
======================

   Deploying 'Migrations'
   ----------------------
   > transaction hash:    0x9a17a50e6efd52ba3e55245c76c52b065d20587add45aee732c233987033e567
   > Blocks: 0            Seconds: 0
   > contract address:    0x77409B688eA5461078a31450F3138EA8324F72C9
   > block number:        1
   > block timestamp:     1604387655
   > account:             0xc7e4bBc4269fdC62F879834E363173aeE7895F45
   > balance:             99.99616114
   > gas used:            191943 (0x2edc7)
   > gas price:           20 gwei
   > value sent:          0 ETH
   > total cost:          0.00383886 ETH


   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:          0.00383886 ETH


2_deploy.js
===========

   Deploying 'ERC721PresetMinterPauserAutoId'
   ------------------------------------------
   > transaction hash:    0xc1a3994c2ad2ba706ac49934b4f480c7b3d9b94241f526afa2dfe91545145a4e
   > Blocks: 0            Seconds: 0
   > contract address:    0xEaB17D581552123695f03F12b09e378EE9463b44
   > block number:        3
   > block timestamp:     1604387655
   > account:             0xc7e4bBc4269fdC62F879834E363173aeE7895F45
   > balance:             99.92142266
   > gas used:            3694586 (0x385ffa)
   > gas price:           20 gwei
   > value sent:          0 ETH
   > total cost:          0.07389172 ETH


   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:          0.07389172 ETH


Summary
=======
> Total deployments:   2
> Final cost:          0.07773058 ETH
```

### 민트

발행자 역할이 있는 계정에서 지정된 계정으로 토큰을 발행하는 트랜잭션을 보낼 수 있습니다.

```
truffle(develop)> nft = await ERC721PresetMinterPauserAutoId.deployed()
undefined
```

우리의 경우 발행자 역할이 부여된 토큰을 배포한 계정에서 발행합니다.
구성된 계정을 보려면 명령 `accounts` 을 실행하십시오

```
truffle(rinkeby)> accounts
[ '0x133d144f52705ceb3f5801b63b9ebccf4102f5ed',
```

토큰 ID가 1인 NFT 1개를 발행합니다. 토큰 보유자가 될 주소를 지정합니다 ("0xc7e4bBc4269fdC62F879834E363173aeE7895F45")내 테스트 계정 중 하나임.
```
truffle(rinkeby)> await nft.mint("0x133d144f52705ceb3f5801b63b9ebccf4102f5ed")
{ tx:
   '0x0d90d4a2a4ac3f33d5220deb11e8f65adf14a6669afd18abd4cce8ca7ab58e04',
  receipt:
   { blockHash: '0x724ba66bc1d799820c05a93ae67991b21bb769fd1e9dddd5db9f725f5f633331',
     blockNumber: 3333746,
     contractAddress: null,
     cumulativeGasUsed: 164785,
     from: '0x77737a65c296012c67f8c7f656d1df81827c9541',
     gasUsed: 164785,
...
```
