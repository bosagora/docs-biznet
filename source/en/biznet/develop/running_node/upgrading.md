# How to Upgrade Geth

Updating `geth` is as easy as it gets. You just need to download and install the newer version of `geth`, shutdown your node and restart with the new software. Geth will automatically use the data of your old node and sync the latest blocks that were mined since you shut down the old software.

## Step 1: Compile the New Version

```bash
git clone https://github.com/bosagora/go-ethereum
# Enter the folder go-ethereum was cloned into
cd go-ethereum
# Comile and install go-ethereum
make geth
```


## Step 2: Stop Geth

```

$ pid=`ps -ef | grep geth | grep -v grep | awk '{print $2}'`

$ kill  $pid

```


## Step 3: Restart



```bash
## start a node
geth --config ./config.toml --datadir ./node --syncmode snap
```
