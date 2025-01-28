# Fetch.ai (FET)

Fetch.ai is an open-source blockchain platform that combines artificial intelligence (AI) and distributed ledger technology (DLT) to enable decentralized, automated, and intelligent decision-making. It is designed to power autonomous agents—digital entities that act on behalf of individuals, businesses, or devices—facilitating seamless interactions and transactions in complex, decentralized ecosystems.

Fetch.ai employs a proof-of-stake consensus mechanism for security and scalability. It also features a unique smart contract framework, enabling advanced functionalities like AI-powered automation. The platform is built to support applications in a variety of sectors, such as supply chain optimization, decentralized finance (DeFi), energy grid management, transportation, and IoT device coordination.

One key innovation is its use of "multi-agent systems," where autonomous agents collaborate or compete to complete tasks efficiently. For example, in transportation, agents could optimize routes or allocate resources in real-time. Fetch.ai also provides a machine-learning-based framework that enhances decision-making by analyzing vast amounts of data in a decentralized manner.

The platform’s native cryptocurrency, FET, is used for transactions, staking, and incentivizing network participants. Fetch.ai aims to create a smarter, more efficient decentralized ecosystem where AI and blockchain converge to automate and optimize real-world processes.

## State Sync

```bash
SNAP_RPC="https://fetch-rpc.panthea.eu:443"

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.fetchd/config/config.toml

sudo systemctl stop fetchd

cp $HOME/.fetchd/data/priv_validator_state.json $HOME/.fetchd/priv_validator_state.json.backup

fetchd tendermint unsafe-reset-all --keep-addr-book --home "$HOME/.fetchd"

mv $HOME/.fetchd/priv_validator_state.json.backup $HOME/.fetchd/data/priv_validator_state.json

sudo systemctl start fetchd
```

## Addrbook (Updated every 8 hours)

[https://valhalla.panthea.eu/addrbooks/fetch/addrbook.json](https://valhalla.panthea.eu/addrbooks/fetch/addrbook.json)

```bash
curl -Ls https://valhalla.panthea.eu/addrbooks/fetch/addrbook.json > $HOME/.fetchd/config/addrbook.json
```

## Genesis file

[https://valhalla.panthea.eu/genesis/fetch/genesis.json](https://valhalla.panthea.eu/genesis/fetch/genesis.json)

```bash
curl -Ls https://valhalla.panthea.eu/genesis/fetch/genesis.json > $HOME/.fetchd/config/genesis.json
```

## Persistent Peer

```url
327d55fae801a04ec963345ccaf6baa7233d6df1@fetch-peer.panthea.eu:27656
```

## Seed Node

```url
b66ec99a4d4142ca98308389cafd75156079777c@fetch-seed.panthea.eu:37656
```

## gRPC Endpoint

fetch-grpc.panthea.eu:16710

## RPC Endpoint

[https://fetch-rpc.panthea.eu/](https://fetch-rpc.panthea.eu/)

## REST/API Endpoint

[https://fetch-api.panthea.eu/](https://fetch-api.panthea.eu/)
