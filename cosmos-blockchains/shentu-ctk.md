---
description: >-
  Decentralized security solution for audits, insurance, monitoring, and
  decentralized finance, built with the Cosmos SDK.
---

# Shentu (CTK)

## Snapshot (Max. 4 hours old)

**Pruning**: custom/100/0/10 - **Indexer**: null

```bash
sudo systemctl stop shentud

cp $HOME/.shentud/data/priv_validator_state.json $HOME/.shentud/priv_validator_state.json.backup

rm -rf $HOME/.shentud/data

curl -o - -L https://valhalla.panthea.eu/snapshots/shentu-snapshot.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.shentud

mv $HOME/.shentud/priv_validator_state.json.backup $HOME/.shentud/data/priv_validator_state.json

sudo systemctl start shentud
```

## State Sync

```bash
SNAP_RPC="https://shentu-rpc.panthea.eu:443"

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.shentud/config/config.toml

sudo systemctl stop shentud

cp $HOME/.shentud/data/priv_validator_state.json $HOME/.shentud/priv_validator_state.json.backup

shentud tendermint unsafe-reset-all --keep-addr-book --home "$HOME/.shentud"

mv $HOME/.shentud/priv_validator_state.json.backup $HOME/.shentud/data/priv_validator_state.json

sudo systemctl start shentud
```

## Addrbook (Updated 6 times a day)

[https://valhalla.panthea.eu/addrbooks/shentu/addrbook.json](https://valhalla.panthea.eu/addrbooks/shentu/addrbook.json)

```bash
curl -Ls https://valhalla.panthea.eu/addrbooks/shentu/addrbook.json > $HOME/.shentud/config/addrbook.json
```

## Genesis file

[https://valhalla.panthea.eu/genesis/shentu/genesis.json](https://valhalla.panthea.eu/genesis/shentu/genesis.json)

```bash
curl -Ls https://valhalla.panthea.eu/genesis/shentu/genesis.json > $HOME/.shentud/config/genesis.json
```

## Persistent Peer

```url
207c47bed435e4174844064ef3f51ca35b059de2@shentu-peer.panthea.eu:26656
```

## Seed Node

```url
3edd4e16b791218b623f883d04f8aa5c3ff2cca6@shentu-seed.panthea.eu:36656
```

## RPC Endpoint

[https://shentu-rpc.panthea.eu/](https://shentu-rpc.panthea.eu/)

## REST/API Endpoint

[https://shentu-api.panthea.eu/](https://shentu-api.panthea.eu/)
