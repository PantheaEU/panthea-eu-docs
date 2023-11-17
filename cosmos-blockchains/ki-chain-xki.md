---
description: >-
  Open-source, public blockchain designed to enable decentralized finance, built
  with the Cosmos SDK.
---

# Ki Chain (XKI)

## Snapshot (Max. 4 hours old)

```bash
sudo systemctl stop kid

cp $HOME/.kid/data/priv_validator_state.json $HOME/.kid/priv_validator_state.json.backup

rm -rf $HOME/.kid/data

curl -o - -L https://valhalla.panthea.eu/snapshots/kichain-snapshot.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.kid

mv $HOME/.kid/priv_validator_state.json.backup $HOME/.kid/data/priv_validator_state.json

sudo systemctl start kid
```

## Wasm only (Max. 4 hours old)

[https://valhalla.panthea.eu/snapshots/kichain-wasm.tar.lz4](https://valhalla.panthea.eu/snapshots/kichain-wasm.tar.lz4)

```bash
rm -rf $HOME/.kid/wasm

curl -o - -L https://valhalla.panthea.eu/snapshots/kichain-wasm.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.kid/
```

## State Sync

```bash
SNAP_RPC="https://kichain-rpc.panthea.eu:443"

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.kid/config/config.toml

sudo systemctl stop kid

cp $HOME/.kid/data/priv_validator_state.json $HOME/.kid/priv_validator_state.json.backup

kid tendermint unsafe-reset-all --keep-addr-book --home "$HOME/.kid"

mv $HOME/.kid/priv_validator_state.json.backup $HOME/.kid/data/priv_validator_state.json

sudo systemctl start kid
```

## Addrbook (Updated every hour) <a href="#addrbook" id="addrbook"></a>

[https://valhalla.panthea.eu/addrbooks/kichain/addrbook.json](https://valhalla.panthea.eu/addrbooks/kichain/addrbook.json)

```bash
curl -Ls https://valhalla.panthea.eu/addrbooks/kichain/addrbook.json > $HOME/.kid/config/addrbook.json
```

## Genesis file

[https://valhalla.panthea.eu/genesis/kichain/genesis.json](https://valhalla.panthea.eu/genesis/kichain/genesis.json)

```bash
curl -Ls https://valhalla.panthea.eu/genesis/kichain/genesis.json > $HOME/.kid/config/genesis.json
```

## Persistent Peer

```url
e7bab76ef15493aaee6f91a0652ba098838a0bfb@kichain-peer.panthea.eu:28656
```

## Seed Node

```url
8edd80b2e7e807af9617d643dcbf5125425cab68@kichain-seed.panthea.eu:38656
```

## gRPC Endpoint

kichain-grpc.panthea.eu:16720

## RPC Endpoint

[https://kichain-rpc.panthea.eu](https://kichain-rpc.panthea.eu)

## REST/API Endpoint

[https://kichain-api.panthea.eu](https://kichain-api.panthea.eu)
