# Anubis Chain subgraph example

Example [The Graph](https://thegraph.com/) subgraph for **Anubis Mainnet**.

Anubis is listed as a supported network: [thegraph.com/docs/en/supported-networks/anubis](https://thegraph.com/docs/en/supported-networks/anubis/).

This repository is **development source**: a clone-and-adapt template. It is not a hosted Graph Node and not The Graph’s docs site.

- Live explorer: [AnubisScan](https://anubisscan.io/)
- Public RPC: `https://rpc.anubispace.org`
- Network id in `subgraph.yaml`: `anubis` (must match The Graph registry)
- Example contract: DAI `0x83fd06F0846d9D90B3016bF670Efe2E0B11cDe14` on chain ID `6714`

A subgraph can only index **public** on-chain data. Shielded / ZK-private payloads are not visible to Indexers.

## Network

| Parameter | Mainnet |
| --- | --- |
| Registry id | `anubis` |
| Chain ID | `6714` (`eip155:6714`) |
| Gas token | `gasDAI` |
| RPC | `https://rpc.anubispace.org` |
| Explorer | `https://anubisscan.io/` |

Studio playground testing is not available for Anubis. Validate locally or publish to The Graph Network.

## Quick start

```sh
npm ci
npm run codegen
npm run build
```

Point `subgraph.yaml` at your contract address, ABI, and **start block** (the deployment block on [AnubisScan](https://anubisscan.io/) — do not scan from genesis on a long chain).

Initialize a new project with Graph CLI if you prefer the wizard (`ethereum` protocol, network identifier `anubis`):

```sh
npm install -g @graphprotocol/graph-cli@latest
graph init
```

## Local Graph Node (optional)

Anubis has no Studio staging, so a local node is the way to dry-run indexing. Point it at the public RPC:

```yaml
environment:
  ethereum: "anubis:https://rpc.anubispace.org"
```

Then:

```sh
graph create --node http://localhost:8020/ anubis-subgraph-example
graph deploy --node http://localhost:8020/ --ipfs http://localhost:5001 anubis-subgraph-example
```

See [graph-node](https://github.com/graphprotocol/graph-node) for the Docker stack.

## Publish

```sh
graph codegen && graph build
graph publish
```

`--protocol-network` is where The Graph protocol contracts live (Arbitrum One), not Anubis. Add curation signal so Indexers pick the subgraph up. Query URLs and API keys come from [Graph Explorer](https://thegraph.com/explorer/) and [Studio](https://thegraph.com/studio/).

## Layout

| Path | Purpose |
| --- | --- |
| `subgraph.yaml` | Manifest (`network: anubis`) |
| `schema.graphql` | Query entities |
| `src/mapping.ts` | Event handlers |
| `abis/` | Contract ABIs |

## License

MIT. Safe/upstream ABIs you swap in keep their original licenses.
