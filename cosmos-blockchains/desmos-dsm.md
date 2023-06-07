---
description: >-
  Desmos is a blockchain protocol powered by Forbole designed for user-centric
  social networks.
---

# Desmos (DSM)

## Snapshot (Max. 4 hours old)

**Pruning**: custom/100/0/10 - **Indexer**: null

```bash
sudo systemctl stop desmosd

cp $HOME/.desmos/data/priv_validator_state.json $HOME/.desmos/priv_validator_state.json.backup

rm -rf $HOME/.desmos/data $HOME/.desmos/wasm

curl -o - -L https://valhalla.panthea.eu/snapshots/desmos-snapshot.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.desmos

mv $HOME/.desmos/priv_validator_state.json.backup $HOME/.desmos/data/priv_validator_state.json

sudo systemctl start desmosd
```

## State Sync

Remember to add our peer:\
**7c506d9e32cfc486ea714ee0c0307022398b8c20@desmos-peer.panthea.eu:29656**\
to persistent\_peers in config.toml before doing the State Sync.

```bash
SNAP_RPC="https://desmos-rpc.panthea.eu:443"

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.desmos/config/config.toml

sudo systemctl stop desmosd

cp $HOME/.desmos/data/priv_validator_state.json $HOME/.desmos/priv_validator_state.json.backup

desmos tendermint unsafe-reset-all --keep-addr-book --home "$HOME/.desmos"

mv $HOME/.desmos/priv_validator_state.json.backup $HOME/.desmos/data/priv_validator_state.json

sudo systemctl start desmosd
```

## Wasm only (Max. 4 hours old)

[https://valhalla.panthea.eu/snapshots/desmos-wasm.tar.lz4](https://valhalla.panthea.eu/snapshots/desmos-wasm.tar.lz4)

```bash
rm -rf $HOME/.desmos/wasm

curl -o - -L https://valhalla.panthea.eu/snapshots/desmos-wasm.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.desmos/
```

## Addrbook (Updated every hour)

[https://valhalla.panthea.eu/addrbooks/desmos/addrbook.json](https://valhalla.panthea.eu/addrbooks/desmos/addrbook.json)

```bash
curl -Ls https://valhalla.panthea.eu/addrbooks/desmos/addrbook.json > $HOME/.desmos/config/addrbook.json
```

## Genesis file

[https://valhalla.panthea.eu/genesis/desmos/genesis.json](https://valhalla.panthea.eu/genesis/desmos/genesis.json)

```bash
curl -Ls https://valhalla.panthea.eu/genesis/desmos/genesis.json > $HOME/.desmos/config/genesis.json
```

## Persistent Peer

```url
7c506d9e32cfc486ea714ee0c0307022398b8c20@desmos-peer.panthea.eu:29656
```

## Seed Node

```url
73fc6b8b41aada42306b2f149619cc0ff935a868@desmos-seed.panthea.eu:39656
```

## RPC Endpoint

[https://desmos-rpc.panthea.eu/](https://desmos-rpc.panthea.eu/)

## REST/API Endpoint

[https://desmos-api.panthea.eu/](https://desmos-api.panthea.eu/)
