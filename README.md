# SCDOLAB

Open-source software for the **SCDO** blockchain: the shard 0 EVM node, the go-scdo
proof-of-work client for shards 1-4, the [scdoscan.io](https://scdoscan.io) explorer
backend, and wallet tooling.

SCDO started as a sharded proof-of-work chain (go-scdo: four shards, ZPoW CPU mining,
cross-shard transactions). **Shard 0** is a newer EVM-compatible chain that standard
Ethereum wallets such as MetaMask can use directly.

## Networks

| Network | Client | Consensus | Chain ID | Decimals | Block reward | Endpoints |
|---|---|---|---|---|---|---|
| **Shard 0** (EVM) | [`scdo-shard0`](https://github.com/SCDOLAB/scdo-shard0) (`parallel-node`) | Single producer node, 2 s blocks | **568** (`0x238`) | **18** | none (fees only) | RPC `https://scdoscan.io/rpc/0` |
| **Shard 1** | [`go-scdo`](https://github.com/SCDOLAB/go-scdo) | ZPoW (CPU) | n/a | **8** | 3 SCDO* | P2P port **8057** |
| **Shard 2** | `go-scdo` | ZPoW (CPU) | n/a | **8** | 3 SCDO* | P2P port **8058** |
| **Shard 3** | `go-scdo` | ZPoW (CPU) | n/a | **8** | 3 SCDO* | P2P port **8059** |
| **Shard 4** | `go-scdo` | ZPoW (CPU) | n/a | **8** | 3 SCDO* | P2P port **8056** |

\* go-scdo's current reward era (block heights 6,300,000-9,449,999). The reward drops to
2.5 SCDO per block at height 9,450,000 (`consensus/reward.go`). go-scdo amounts use
8 decimals: 1 SCDO = 100,000,000 wen (`common.ScdoToWen`).

Public P2P seed hosts for shards 1-4 (TCP + UDP, one port per shard as above):
`74.208.207.184`, `82.223.19.88`, `74.208.136.152`.

**Add shard 0 to MetaMask:** RPC URL `https://scdoscan.io/rpc/0`, chain ID `568`,
symbol `SCDO`, explorer `https://scdoscan.io`.

## Mining: there is no pool

**There is no SCDO mining pool or stratum server.** Shards 1-4 are mined solo: you run
your own go-scdo full node for your shard, it syncs the full history (about 25 GB), and
every block it finds pays the reward directly to your address. Shard 0 is not mined by
the public.

```bash
curl -fsSL https://scdoscan.io/mine.sh -o mine.sh && bash mine.sh   # Linux x86_64
```

Guide: <https://scdoscan.io/quickstart.html>. Treat any website or app that offers
"SCDO pool mining" or "cloud mining" as unaffiliated.

## Links

| | |
|---|---|
| Explorer | <https://scdoscan.io> |
| Web wallet | <https://scdoscan.io/wallet/> |
| Downloads (Linux node and client, SHA256SUMS) | <https://scdoscan.io/downloads/> ([node](https://scdoscan.io/downloads/scdo-node-linux-amd64), [client](https://scdoscan.io/downloads/scdo-client-linux-amd64), [SHA256SUMS](https://scdoscan.io/downloads/SHA256SUMS)) |
| Mining quick start | <https://scdoscan.io/quickstart.html> |
| Explorer API | `https://api.scdoscan.io/api/v1` |

## Repositories

| Repository | What it is |
|---|---|
| [scdo-shard0](https://github.com/SCDOLAB/scdo-shard0) | Shard 0 EVM node (`parallel-node`): JSON-RPC, signed-tx validation, 2 s blocks, faucet |
| [go-scdo](https://github.com/SCDOLAB/go-scdo) | Go client for the PoW shards 1-4: node, client, miner, seed configs, `mine.sh` |
| [scdoscan-api](https://github.com/SCDOLAB/scdoscan-api) | Explorer backend: MongoDB indexer and REST API behind scdoscan.io |
| [scdo-wallet-mobile](https://github.com/SCDOLAB/scdo-wallet-mobile) | Mobile wallet |
| [scdo-eth-rpc-proxy](https://github.com/SCDOLAB/scdo-eth-rpc-proxy) | Translates Ethereum `eth_*` JSON-RPC to go-scdo `scdo_*` calls |
| [scdo-evm-bridge](https://github.com/SCDOLAB/scdo-evm-bridge) | Proof of concept: SCDO to EVM bridge and tooling |
| [eip-toolkit](https://github.com/SCDOLAB/eip-toolkit) | EIP-1559 base fee, Merkle allowlist and log-filter experiments |

Security issues: please email **admin@apeccapital.org** (do not open public issues).

## Operator and compliance

| | |
|---|---|
| Operator | **9Y9 PTY LTD**, Melbourne, Victoria, Australia |
| ACN / ABN | ACN 600 445 118 · ABN 19 600 445 118 |
| AUSTRAC | Registered Digital Currency Exchange provider, registration **DCE100714503-001** (valid until 14 March 2029). Verify on the [AUSTRAC register](https://online.apps.austrac.gov.au/vaspr) by searching ACN `600445118` |
| Compliance | [scdoscan.io/compliance.html](https://scdoscan.io/compliance.html) |
| External dispute resolution | Member of the [Australian Financial Complaints Authority](https://www.afca.org.au/) (AFCA), member number **124589** |

**Important.** Registration with AUSTRAC is not an endorsement, approval or guarantee by
AUSTRAC or any other government agency of 9Y9 PTY LTD, SCDO or any software here. AUSTRAC
does not assess the merits of digital currencies. 9Y9 PTY LTD does not currently hold a
remittance registration or an Australian Credit Licence, and nothing in these repositories
is an offer of a financial product, credit or remittance service. The software is provided as-is under its open-source licences. Digital assets are
highly volatile and you can lose all of their value. Do your own research.
