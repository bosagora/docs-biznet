# **Geth 업그레이드 방법**

`geth`를 업데이트하기 위해 가장 쉬운 방법은 최신버전을 다운로드하는 것입니다. `geth`의 최신 버전을 다운로드하여 설치하고 geth노드를 종료하고 새 소프트웨어로 다시 시작하기만 하면 됩니다. 
Geth는 자동으로 이전 노드의 데이터를 사용하고 이전 소프트웨어를 종료한 후 채굴된 최신 블록을 동기화합니다.

## **1단계: 새 버전 컴파일**

```bash
git clone https://github.com/bosagora/go-ethereum
# Enter the folder go-ethereum was cloned into
cd go-ethereum
# Comile and install go-ethereum
make geth
```


## **2단계: Geth 중지**

```

$ pid=`ps -ef | grep geth | grep -v grep | awk '{print $2}'`

$ kill  $pid

```


## **3단계: 다시 시작**



```bash
## start a node
geth --config ./config.toml --datadir ./node --syncmode snap
```
