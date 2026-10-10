# eth-inspect

A fast Rust toolbox for measuring Ethereum blocks and transactions: type, position in the block, tip, builder, and whether a transaction came through the public mempool or a private route.

Status: early development.

## What it measures

| Measure | Definition |
|---|---|
| Type | swap, arbitrage candidate, liquidation, token or native transfer, deployment, other |
| Position | gas used before the transaction / block gas used |
| Tip | effective gas price minus base fee |
| Builder | relay-reported builder, with extraData as a fallback |
| Route | public if seen in the mempool before the block, private otherwise |
| Wait (planned) | time from first seen to inclusion |

Results are aggregated by type, block region, builder and route, and written as Markdown and Parquet.

## Data

Built on [Xatu](https://github.com/ethpandaops/xatu) public data (execution and mempool), with MEV-Boost relay APIs for builder identity. No archive node needed.

## Usage

```
eth-inspect fetch --date 2026-07-01 --out data/
eth-inspect day   --date 2026-07-01 --data data/ --report reports/
```

Each run checks its input schema and stops on implausible output, such as all-zero tips or undecoded builder names.

## Acknowledgements

Classifiers and labels draw on [Brontes](https://github.com/SorellaLabs/brontes) and [mev-inspect-py](https://github.com/flashbots/mev-inspect-py); the mempool-arrival method on [ZeroMEV](https://zeromev.org).

## Licence

Apache-2.0
