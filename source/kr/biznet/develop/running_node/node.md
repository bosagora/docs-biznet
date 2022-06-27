# **노드를 운영하는 방법**

## **노드의 기능들**

* 전체 블록체인 기록을 디스크에 저장하고 네트워크의 데이터 요청에 응답할 수 있습니다.
* 새 블록 및 트랜잭션을 수신하고 유효성을 검사합니다.
* 모든 계정의 상태를 확인합니다.

## **지원되는 플랫폼**

`Mac OS X`와 `Linux`에서 노드 실행을 지원합니다.

## **시스템 사양**
- 최신 버전의 Mac OS X 또는 Linux를 실행하는 VPS.
- **중요** 2T GB의 여유 디스크 공간, 솔리드 스테이트 드라이브(SSD), gp3, 8k IOPS, 250MB/S 처리량, 읽기 지연 시간 <1ms. (스냅/빠른 동기화로 시작하는 경우 NVMe SSD가 필요합니다)
- 16코어 CPU와 64GB 메모리(RAM).
- AWS에서는 m5zn.3xlarge 인스턴스 유형, Google 클라우드에서는 c2-standard-16을 제안합니다.
- 업로드/다운로드 속도가 초당 5MB인 광대역 인터넷 연결

## **노드의 설정**

### 연결과 관련된 일반적인 문제

가끔 동기화가 안될 때가 있습니다. 가장 일반적인 이유는 다음과 같습니다.

- `geth` 를 검색 프로토콜 없이 시작 했으며 `--nodiscover` 매개변수를 `False` 로 설정할 수 있습니다. 고정 노드로 전체 노드를 실행하는 경우에만 이것을 사용하십시요.

- `BootstrapNodes`를 업데이트

```
BootstrapNodes = ["enode://b072533c8d72501816f1bc07e12f4703778697abfef305800c3ee178b63439e537c4570b5b4b491582e901cb176616826ed071539cbbf26fe46ee8571992293a@13.228.4.203:30303","enode://4c76a1996466b69bd6dc6dd9566aff175cb8aadc846241d100378bdb1d9a4ea47196d9f660d308954ed8a2c725c4f6f4616e9cf108abb5efd766ad9bc7c9af35@3.39.127.36:30303"]
```

- `Static nodes`를 추가

Geth는 또한 항상 연결하고 싶은 특정 피어가 있는 경우 정적 노드라는 기능을 지원합니다. 고정 노드는 연결이 끊길 때 다시 연결됩니다. 
다음과 같은 내용을 파일에 `<datadir>/geth/static-nodes.json` 아래 내용을 넣어 영구 정적 노드를 구성할 수 있습니다
```
[
    "enode://pubkey@ip:port",
    "enode://b072533c8d72501816f1bc07e12f4703778697abfef305800c3ee178b63439e537c4570b5b4b491582e901cb176616826ed071539cbbf26fe46ee8571992293a@13.228.4.203:30303",
    "enode://844a0cbe8a98fbfc2d80c20539148c4c0862fa06e3e9580bd53ce05c7f26ac4a5cb78369adcb7ac146062273cb437a6e4dd1022cf5a42e31409e279741494a11@54.255.235.26:30303",
    "enode://5ef7a9487b4944f0eaca0ffbd36839de9cf36d871104d4ebc788d75ccf5418e3103bb73791cfc8942b80dba33aad7daa6aed709ba4ee1efa26564f7af523f9c5@54.169.187.148:30303",
    "enode://ce91817b76993736a1c01ab419597528a4084ab57928c60e43741d13d78f941396895d33a3b8ab9286cd403f8520a873af0c692151905b51b7ea7370d832d3bc@18.136.209.89:30303",
    "enode://a578d5c7c87dc293d3fa9f9176f27049dc6e5e259914202b52a15ad52b2529fd375b62e055097ff520a7f93a876d1fcbca5ef0b32dab273e474db907f33d97b3@13.215.191.60:30303",
    "enode://4c76a1996466b69bd6dc6dd9566aff175cb8aadc846241d100378bdb1d9a4ea47196d9f660d308954ed8a2c725c4f6f4616e9cf108abb5efd766ad9bc7c9af35@3.39.127.36:30303",
    "enode://9b086682cfd01ac2223700676d718eb5a7945c6200ca113d0555c4aebec3ee19a6161a88fbee50662254976d9a97c4c5b7e50f55bfbf7ed598cd8c5c078dbd7d@54.180.121.94:30303",
    "enode://b39fd722a26cf48c6b055b0eed5b49c98d420d546d3419ff6a2499ddd190aa5a4e7371343d63a0150e7695bb42387b3d6837f99a49db8f05d78fc775689e2210@15.164.170.19:30303",
    "enode://c08fdd44bc3e09267321a99c6057ec870d5bcb1e3b5ecf7ef48158881abc99d1cca2174328e80917003c1ee27908792badc148a80dc3bdee365c748fcd046723@54.180.93.83:30303"
]
```

`admin.addPeer()`를 사용하여 js 콘솔을 통해 런타임에 정적 노드를 추가할 수도 있습니다.

```
admin.addPeer( "enode://b072533c8d72501816f1bc07e12f4703778697abfef305800c3ee178b63439e537c4570b5b4b491582e901cb176616826ed071539cbbf26fe46ee8571992293a@13.228.4.203:30303"
)
```

- `Trusted nodes`를 추가

Geth는 피어 제한에 도달한 경우에도 항상 다시 연결할 수 있는 신뢰할 수 있는 노드를 지원합니다. 
구성 파일을 통해 영구적으로 추가하거나 RPC 호출을 통해 임시로 추가할 수 있습니다.
구성파일은 다음과 같습니다. <datadir>/geth/trusted-nodes.json


### 동기화 모드

* 빠른 동기화

기본 동기화 모드입니다 . 전체 상태 데이터베이스를 다운로드하고 헤더를 먼저 요청하고 나중에 블록 본문과 영수증을 작성하여 빠른 동기화를 수행하는 노드를 동기화합니다. 
빠른 동기화가 BizNet 네트워크의 최상의 블록에 도달하면 전체 동기화 모드로 전환됩니다.

* 전체 동기화

제네시스에서 시작하여 모든 블록을 확인하고 모든 트랜잭션을 실행하는 노드를 동기화합니다. 이 모드는 빠른 동기화 모드보다 약간 느리지만 보안이 강화되었습니다.

## **단계별로 노드를 실행하기**

### 스냅샷에서 동기화

준비 중입니다.


### 제네시스 블록에서 동기화

1.소스 코드로 빌드

[Go 1.18+](https://golang.org/doc/install)를 설치하고, `PATH`에 `GOPATH`를 추가했는지 확인하십시오

```bash
git clone https://github.com/bosagora/go-ethereum
# Enter the folder go-ethereum was cloned into
cd go-ethereum
# Compile and install go-ethereum
make geth
```

또는 [릴리스 페이지](https://github.com/bosagora/go-ethereum/releases/latest) 에서 이미 빌드된 바이너리를 다운로드 하거나 아래 지침을 따를 수 있습니다.
```bash
# Linux
wget   $(curl -s https://api.github.com/repos/bosagora/go-ethereum/releases/latest |grep browser_ |grep linux |cut -d\" -f4)
unzip linux.zip
# MacOS
wget   $(curl -s https://api.github.com/repos/bosagora/go-ethereum/releases/latest |grep browser_ |grep mac |cut -d\" -f4)
unzip mac.zip
```

2.구성 파일 다운로드

다운로드 `genesis.json` 및 `config.toml`:

```bash

## mainet
wget   $(curl -s https://api.github.com/repos/bosagora/go-ethereum/releases/latest |grep browser_ |grep mainnet |cut -d\" -f4)  
unzip mainnet.zip

## testnet
wget   $(curl -s https://api.github.com/repos/bosagora/go-ethereum/releases/latest |grep browser_ |grep testnet |cut -d\" -f4)
unzip testnet.zip
```

3.로컬에서 제네시스 상태 생성하기

```bash
geth --datadir node init genesis.json
```

다음 출력을 볼 수 있습니다.

```
INFO [05-19|14:53:17.468] Allocated cache and file handles         database=/Users/michael/Downloads/go-ethereum/node/geth/chaindata cache=16.00MiB handles=16
INFO [05-19|14:53:17.498] Writing custom genesis block
INFO [05-19|14:53:17.501] Persisted trie from memory database      nodes=21 size=56.84KiB time=357.915µs gcnodes=0 gcsize=0.00B gctime=0s livenodes=1 livesize=-574.00B
INFO [05-19|14:53:17.502] Successfully wrote genesis state         database=chaindata hash=7d79cc…fb0d1e
INFO [05-19|14:53:17.503] Allocated cache and file handles         database=/Users/michael/Downloads/go-ethereum/node/geth/lightchaindata cache=16.00MiB handles=16
INFO [05-19|14:53:17.524] Writing custom genesis block
INFO [05-19|14:53:17.525] Persisted trie from memory database      nodes=21 size=56.84KiB time=638.396µs gcnodes=0 gcsize=0.00B gctime=0s livenodes=1 livesize=-574.00B
INFO [05-19|14:53:17.528] Successfully wrote genesis state         database=lightchaindata hash=7d79cc…fb0d1e
```

4.노드 시작

```bash
## start a node
geth --config ./config.toml --datadir ./node
```

## **노드의 유지 관리**
 
### 바이너리
모든 클라이언트는 최신 릴리스로 업그레이드하는 것이 좋습니다. [최신 버전](https://github.com/bosagora/go-ethereum/releases/latest)은 더 안정적이고 더 나은 성능을 제공합니다.

### 스토리지
테스트에 따르면 스토리지 크기가 1.5T를 초과하면 노드의 성능이 저하됩니다. 노드는 항상 스토리지를 정리하여 가벼운 스토리지를 유지하는 것이 좋습니다.

스토리지 정리 방법:

1. 노드를 중지합니다.  
2. 실행 `nohup geth snapshot prune-state --datadir {the data dir of your node} &`.   
   이 실행이 완료하는 데 3-5시간이 걸립니다.  
3. 완료되면 노드를 시작하십시오.  

유지 관리자는 항상 몇 개의 백업 노드를 가지고 있어야 합니다.

하드웨어도 중요 하므로 SSD가 2T GB의 여유 디스크 공간, 솔리드 스테이트 드라이브(SSD), gp3, 8k IOPS, 250MB/S 처리량, 읽기 지연 시간 <1ms를 충족하는지 확인하십시오 .

## **Geth 업그레이드**

이 [가이드](./upgrading.md) 를 읽으십시오

