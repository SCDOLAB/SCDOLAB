# SCDOLAB

Open-source software for the **SCDO** blockchain. The only official website is
**[scdoscan.io](https://scdoscan.io)** (explorer, web wallet, downloads). Treat any other
site, app or "pool" that uses the SCDO name as unaffiliated.

SCDO has two parts:

* **Shard 0**: an EVM chain run by a [core-geth](https://github.com/etclabscore/core-geth) fork,
  Ethash proof of work, **chain ID 5680** (`0x1630`). MetaMask and other Ethereum wallets work directly.
* **Shards 1-4**: the original sharded proof-of-work chain ([go-scdo](https://github.com/SCDOLAB/go-scdo),
  ZPoW, cross-shard transactions).

## Networks

| Network | Client | Consensus | Chain ID | Decimals | Endpoints |
|---|---|---|---|---|---|
| **Shard 0** (EVM) | [`scdo-shard0`](https://github.com/SCDOLAB/scdo-shard0) (core-geth v1.12.23 fork) | Ethash PoW, 2 SCDO per block + fees | **5680** (`0x1630`) | **18** | RPC `https://scdoscan.io/rpc/0`, P2P `82.223.19.88:30368` |
| **Shard 1** | [`go-scdo`](https://github.com/SCDOLAB/go-scdo) | ZPoW | n/a | **8** | P2P port **8057** |
| **Shard 2** | `go-scdo` | ZPoW | n/a | **8** | P2P port **8058** |
| **Shard 3** | `go-scdo` | ZPoW | n/a | **8** | P2P port **8059** |
| **Shard 4** | `go-scdo` | ZPoW | n/a | **8** | P2P port **8056** |

Shard 0 genesis: [scdo-shard0-genesis.json](https://scdoscan.io/downloads/shard0/scdo-shard0-genesis.json)
(genesis hash `0xbbb083…70cb12`). Bootnode:
`enode://1d2c370db7c419349e2313f20023f6b379f946990042b9b42df45cb56e4c3487df0d36c52cd81308fcdf312450f758a6213fcac21213e94a71af4a3c9392601f@82.223.19.88:30368`

Shards 1-4: block reward 3 SCDO in the current era, dropping to 2.5 SCDO at height 9,450,000
(`consensus/reward.go`); 1 SCDO = 100,000,000 wen. Public P2P seed hosts (TCP + UDP, one port per
shard as above): `74.208.207.184`, `82.223.19.88`, `74.208.136.152`, `217.160.65.210`.

**Add shard 0 to MetaMask:** RPC URL `https://scdoscan.io/rpc/0`, chain ID `5680`, symbol `SCDO`,
explorer `https://scdoscan.io`.

## Mining

**Shard 0 (GPU, Ethash).** Download the GPU mining package for Windows or Linux (NVIDIA) from
<https://scdoscan.io/downloads/shard0/> (also in [scdo-gpu-miner releases](https://github.com/SCDOLAB/scdo-gpu-miner/releases)).
It runs your own shard 0 node plus the `scdo-stratum` proxy on your PC, so the blocks you find pay
your own address. Any Ethash stratum miner can connect to that local proxy.
Use the package if you want the rewards yourself.

**Shards 1-4 (ZPoW).** Solo mining with your own go-scdo full node (the history is about 25 GB):

```bash
curl -fsSL https://scdoscan.io/mine.sh -o mine.sh && bash mine.sh   # Linux x86_64
```

Guide: <https://scdoscan.io/quickstart.html>.

There is no SCDO cloud-mining service. Mining gives no guaranteed value.

## Links

| | |
|---|---|
| Explorer | <https://scdoscan.io> |
| Web wallet | <https://scdoscan.io/wallet/> |
| Shard 0 downloads (GPU miner, genesis, SHA256SUMS) | <https://scdoscan.io/downloads/shard0/> |
| Shards 1-4 node and client (Linux) | [node](https://scdoscan.io/downloads/scdo-node-linux-amd64), [client](https://scdoscan.io/downloads/scdo-client-linux-amd64), [SHA256SUMS](https://scdoscan.io/downloads/SHA256SUMS) |
| Explorer API | `https://scdoscan.io/api/v1` (e.g. [`/network/summary`](https://scdoscan.io/api/v1/network/summary)) |

## Repositories

| Repository | What it is |
|---|---|
| [scdo-shard0](https://github.com/SCDOLAB/scdo-shard0) | Shard 0 node: core-geth v1.12.23 fork (branch `scdo`) with the `scdo-stratum` proxy, faucet and the chain ID 5680 genesis |
| [scdo-gpu-miner](https://github.com/SCDOLAB/scdo-gpu-miner) | Shard 0 GPU mining package scripts and releases |
| [go-scdo](https://github.com/SCDOLAB/go-scdo) | Client for shards 1-4: node, client, miner, seed configs, `mine.sh` |
| [scdoscan-api](https://github.com/SCDOLAB/scdoscan-api) | Explorer backend (MongoDB indexer and REST API behind scdoscan.io) |

Archived, for reference only: [scdo-shard0-parallel-legacy](https://github.com/SCDOLAB/scdo-shard0-parallel-legacy)
(the retired first shard 0 node), [scdo-eth-rpc-proxy](https://github.com/SCDOLAB/scdo-eth-rpc-proxy) (proof of concept),
and the original SCDO project repositories (scdowallet, scdo.js, contractDeploy, scdoproject.org).

Security issues: please email **admin@apeccapital.org** (do not open public issues).

## Operator and compliance

| | |
|---|---|
| Operator | **9Y9 PTY LTD**, Melbourne, Victoria, Australia |
| ACN / ABN | ACN 600 445 118 · ABN 19 600 445 118 |
| AUSTRAC | Registered Digital Currency Exchange provider, registration **DCE100714503-001** (valid until 14 March 2029). Verify on the [AUSTRAC register](https://online.apps.austrac.gov.au/vaspr) by searching ACN `600445118` |
| Compliance | [scdoscan.io/compliance.html](https://scdoscan.io/compliance.html) |
| External dispute resolution | Member of the [Australian Financial Complaints Authority](https://www.afca.org.au/) (AFCA), member number **124589** |

**Important.** Registration with AUSTRAC is not an endorsement, approval or guarantee by AUSTRAC or
any other government agency of 9Y9 PTY LTD, SCDO or any software here. AUSTRAC does not assess the
merits of digital currencies. Nothing in these repositories is an offer of a financial product.
The software is provided as-is under its open-source licences. Digital assets are highly volatile
and you can lose all of their value. Do your own research.
