# BOASwap을 소개 합니다.

## BOASwap 이란?

BOASwap 에서 제공되는 영역은 My Assets, Swap, Pool, Bridge 로 크게 구분 할 수 있습니다.

먼저 BOASwap 영역에서 사용 되는 명칭을 설명 합니다.

- BizNet : POA 합의 알고리즘으로 합의를 이루는 다중 노드로 구성된 신뢰 할 수 있는 BOASAGORA의 블록체인 네트워크 입니다. EVM(Ethereum Virtual Machine)을 지원 하여 스마트컨트랙트를 실행 할 수 있으므로 이더리움에서 구동중인 호환 DApp을 BizNet 에서도 계약을 실행 할 수 있습니다.

- BOASwap DEX Protocol : Agora BizNet 에서 ERC-20 토큰의 P2P 시장 형성 및 교환을 용이하게 하는 프로토콜인 자동화된 마켓 메이커를 함께 생성하는 지속적이고 업그레이드 되지 않는 스마트 계약 입니다.

- BOASwap Bridge Protocol : 이더리움 메인넷 과 Agora BizNet 간의 서로 다른 네트워크에서 신뢰할 수 있는 스왑을 페깅과 디페깅을 통해 BOA 코인의 공급량을 고정 하면서 가치 를 이전할 수 있는 아토믹 스왑 스마트 계약 입니다.

- BOASwap Bridge relay node : 이더리움 메인넷 과 Agora BizNet 각각의 네트워크에 연결되어있는 브릿지 중계 노드 로 동작 되며 브릿지 프로토콜의 아토믹 스왑을 각각의 네트워크에서 실행 되도록 지원 합니다.

- BOASwap Interfaces : BOASwap DEX Protocol, Bridge Protocol 과 쉽게 상호 작용할 수 있는 웹 인터페이스 입니다. 인터페이스는 BOASwap 프로토콜들 과 상호작용 할 수 있는 많은 방법 중에 하나 입니다.

## BOASwap

### My Assets
여기에 표시되는 자산은 현재 연결된 네트워크에서 사용자가 보유하고 있는 코인 과 토큰들 을 표시 합니다.
표시 될 수 있는 토큰 및 포인트는 ERC-20 토큰 규격으로 별도의 리스트 에서 관리되고 있으면 이는 우리가 신뢰 할 수 있는 토큰들 이라고 할 수 있습니다.
My Assets에 자신이 보유한 토큰이 표시 되기위해서는 메타마스크 지갑이 Agora BizNet 네트워크에 연결 되어 있어야 합니다. 또한 BOASwap과 신뢰된 연결이 되어 있어야 합니다.

### Swap
BOASwap의 토큰 스왑은 하나의 ERC-20 토큰을 다른 토큰과 교환하는 간단한 방법입니다.
사용자는 입력 토큰과 출력 토큰을 선택합니다. 이것은 입력 금액을 지정하고 프로토콜은 그들이 받을 출력 토큰의 양을 계산합니다.
그런 다음 한 번의 클릭으로 스왑을 실행하고 즉시 지갑에 출력 토큰을 받을 수 있습니다.

### Pool
BOASwap Pool은 BOASwap DEX Protocol을 위한 유동성 풀 입니다.
각 BOASwap 유동성 Pool은 한쌍의 ERC20 토큰을 위한 거래 장소입니다.
Pool이 거래를 촉진 하려면 누군가가 각 토큰의 초기 보증금으로 풀에 공급 해야 합니다. 이것은 풀의 초기 가격을 설정 하게 됩니다.

### Bridge
이더리움 메인넷 과 BizNet의 각각의 블록체인 사이에서 이를 연결 하고 거래를 중개합니다. 
현재 BOA 토큰을 이더리움 메인넷 에서 BizNet으로 코인 전송을 지원하고 있으며 이 거래는 양방향 거래(투웨이 페깅)가 가능 합니다.

### BOA
* Ethereum MainNet ERC20 BOA : [0x746DdA2ea243400D5a63e0700F190aB79f06489e](https://etherscan.io/token/0x746dda2ea243400d5a63e0700f190ab79f06489e) Ethereum 네트워크의 ERC20 스마트컨트랙트 토큰 이며 현재 코인거래소에 상장 되어 있습니다.
* BOSAGORA BizNet BOA : BizNet 네트워크의 기본통화 이며 가치교환 및 네트워크 가스비로 사용 됩니다.
* Ethereum MainNet ERC20 BOA 와 BizNet BOA 환율은 1BOA ≈ 1BOA 입니다.