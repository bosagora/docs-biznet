# How to Run A Node on BizNet

## Nodes Functions

* Stores the full blockchain history on disk and can answer the data request from the network.
* Receives and validates the new blocks and transactions.
* Verifies the states of every accounts.

## Supported Platforms

We support running a node on `Mac OS X`and `Linux`.

## Suggested Requirements

### Node
- VPS running recent versions of Mac OS X or Linux.
- **IMPORTANT** 2T GB of free disk space, solid-state drive(SSD), gp3, 8k IOPS, 250MB/S throughput, read latency <1ms. (if start with snap/fast sync, it will need NVMe SSD)
- 16 cores of CPU and 64 gigabytes of memory (RAM).
- Suggest m5zn.3xlarge instance type on AWS, c2-standard-16 on Google cloud.
- A broadband Internet connection with upload/download speeds of 5 megabyte per second

## Settings

### Common Problems With Connectivity

Sometimes you just can’t get synced. The most common reasons are as follows:

* You have started `geth` without the discovery protocol, you can set the `--nodiscover` parameter to `False`. You only want this if you are running node with fixed nodes.

- Update `BootstrapNodes`

```
BootstrapNodes = ["enode://b072533c8d72501816f1bc07e12f4703778697abfef305800c3ee178b63439e537c4570b5b4b491582e901cb176616826ed071539cbbf26fe46ee8571992293a@13.228.4.203:30303","enode://4c76a1996466b69bd6dc6dd9566aff175cb8aadc846241d100378bdb1d9a4ea47196d9f660d308954ed8a2c725c4f6f4616e9cf108abb5efd766ad9bc7c9af35@3.39.127.36:30303"]
```

- Add `Static nodes`

Geth also supports a feature called static nodes if you have certain peers you always want to connect to. 
Static nodes are re-connected on disconnects. You can configure permanent static nodes by putting something like the following into `<datadir>/geth/static-nodes.json`:

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

You can also add static nodes at runtime via the js console using admin.addPeer():

```
admin.addPeer( "enode://b072533c8d72501816f1bc07e12f4703778697abfef305800c3ee178b63439e537c4570b5b4b491582e901cb176616826ed071539cbbf26fe46ee8571992293a@13.228.4.203:30303"
)
```

- Add `Trusted nodes`

Geth supports trusted nodes that are always allowed to reconnect, even if the peer limit is reached. They can be added permanently via a config file `<datadir>/geth/trusted-nodes.json` or temporary via RPC call.


### Sync Mode

* Fast Sync

The **default** sync mode. Synchronizes a node doing a fast synchronization by downloading the entire state database, requesting the headers first, and filling in block bodies and receipts afterward. Once the fast sync reaches the best block of the BNB Smart Chain network, it switches to full sync mode.

* Full Sync

Synchronizes a node starting at genesis, verifying all blocks and executing all transactions. This mode is a bit slower than the fast sync mode but comes with increased security.


## Steps to Run a Node

### Sync From Snapshot

This is being prepared.


### Sync From Genesis Block

1.Build from source code

Make sure that you have installed [Go 1.13+](https://golang.org/doc/install) and have added `GOPATH` to `PATH` environment variable

```bash
git clone https://github.com/bosagora/go-ethereum
# Enter the folder go-ethereum was cloned into
cd go-ethereum
# Compile and install go-ethereum
make geth
```

or you can download the pre-build binaries from [release page](https://github.com/bosagora/go-ethereum/releases/latest) or follow the instructions below:

```bash
# Linux
wget   $(curl -s https://api.github.com/repos/bosagora/go-ethereum/releases/latest |grep browser_ |grep geth_linux |cut -d\" -f4)
# MacOS
wget   $(curl -s https://api.github.com/repos/bosagora/go-ethereum/releases/latest |grep browser_ |grep geth_mac |cut -d\" -f4)
```

2.Download the config files

Download `genesis.json` and `config.toml` by:

```bash

## mainet
wget   $(curl -s https://api.github.com/repos/bosagora/go-ethereum/releases/latest |grep browser_ |grep mainnet |cut -d\" -f4)
unzip mainnet.zip

## testnet
wget   $(curl -s https://api.github.com/repos/bosagora/go-ethereum/releases/latest |grep browser_ |grep testnet |cut -d\" -f4)
unzip testnet.zip
```

3.Write genesis state locally

```bash
geth --datadir node init genesis.json
```

You could see the following output:

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

4.Start your node


!!! Note
BREAKING CHANGE: Non-EIP155 transactions (i.e. transactions which are not replay-protected) are now rejected by the RPC API. You can disable this restriction using the --rpc.allow-unprotected-txs command-line flag.

```bash
## start a node
geth --config ./config.toml --datadir ./node  --cache 8000 --rpc.allow-unprotected-txs --txlookuplimit 0
```

## Node Maintainence

### Peer Discovery
The bootstrap nodes will be enhanced in the short future. So far, a discovery http service will provide some stable public p2p peers for syncing. Please visit https://api.binance.org/v1/discovery/peers to get dynamic peer info. You can append the peer info to the `StaticNodes` in the config.toml to enhance the networking of the nodes. To avoid crowded networking, the discovery service will change the peer info from time to time, try fetch new ones if the connected peers of node are too few.

### Binary
All the clients are suggested to upgrade to the latest release. The [latest version](https://github.com/bosagora/go-ethereum/releases/latest) is supposed to be more stable and get better performance.

### Storage
According to the test, the performance of a node will degrade when the storage size exceeds 1.5T. We suggest the node always keep light storage by pruning the storage.

How to prune:

1. Stop the node.
2. Run `nohup geth snapshot prune-state --datadir {the data dir of your node} &`. It will take 3-5 hours to finish.
3. Start the node once it is done.

The maintainers should always have a few backup nodes.

The hardware is also important, **make sure the SSD meets: 2T GB of free disk space, solid-state drive(SSD), gp3, 8k IOPS, 250MB/S throughput, read latency <1ms**.

### Light Storage
When the node crashes or been force killed, the node will sync from a block that was a few minutes or a few hours ago. This is because the state in memory is not persisted into the database in real time, and the node needs to replay blocks from the last checkpoint once it start. The replaying time dependents on the configuration `TrieTimeout` in the config.toml.  We suggest you raise it if you can tolerate with long replaying time, so the node can keep light storage.

## Upgrade Geth

Please read [this guide](./upgrading.md)

