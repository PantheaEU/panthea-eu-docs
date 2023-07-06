---
description: >-
  A blockchain hub that provides a trust-less marketplace for the music
  industry.
---

# BitSong (BTSG)

## Snapshot (Max. 4 hours old) <a href="#snapshot" id="snapshot"></a>

**Pruning**: custom/100/0/10 - **Indexer**: null

```bash
sudo systemctl stop bitsongd

cp $HOME/.bitsongd/data/priv_validator_state.json $HOME/.bitsongd/priv_validator_state.json.backup

rm -rf $HOME/.bitsongd/data

curl -o - -L https://valhalla.panthea.eu/snapshots/bitsong-snapshot.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.bitsongd

mv $HOME/.bitsongd/priv_validator_state.json.backup $HOME/.bitsongd/data/priv_validator_state.json

sudo systemctl start bitsongd
```

## State Sync

```bash
SNAP_RPC="https://bitsong-rpc.panthea.eu:443"

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.bitsongd/config/config.toml

sudo systemctl stop bitsongd

cp $HOME/.bitsongd/data/priv_validator_state.json $HOME/.bitsongd/priv_validator_state.json.backup

bitsongd tendermint unsafe-reset-all --keep-addr-book --home "$HOME/.bitsongd"

mv $HOME/.bitsongd/priv_validator_state.json.backup $HOME/.bitsongd/data/priv_validator_state.json

curl -o - -L https://valhalla.panthea.eu/snapshots/bitsong-wasm.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.bitsongd/data/

sudo systemctl start bitsongd
```

## Wasm only (Max. 4 hours old) <a href="#wasm-only" id="wasm-only"></a>

[https://valhalla.panthea.eu/snapshots/bitsong-wasm.tar.lz4](https://valhalla.panthea.eu/snapshots/bitsong-wasm.tar.lz4)

```bash
rm -rf $HOME/.bitsongd/data/wasm

curl -o - -L https://valhalla.panthea.eu/snapshots/bitsong-wasm.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.bitsongd/data/
```

## Addrbook (Updated every hour) <a href="#addrbook" id="addrbook"></a>

[https://valhalla.panthea.eu/addrbooks/bitsong/addrbook.json](https://valhalla.panthea.eu/addrbooks/bitsong/addrbook.json)

```bash
curl -Ls https://valhalla.panthea.eu/addrbooks/bitsong/addrbook.json > $HOME/.bitsongd/config/addrbook.json
```

## Genesis file

[https://valhalla.panthea.eu/genesis/bitsong/genesis.json](https://valhalla.panthea.eu/genesis/bitsong/genesis.json)

```bash
curl -Ls https://valhalla.panthea.eu/genesis/bitsong/genesis.json > $HOME/.bitsongd/config/genesis.json
```

## Persistent Peer

```url
2cd6bb75fc9279c62c0ef3af82fbe08632743472@bitsong-peer.panthea.eu:31656
```

## Seed Node

```url
8defec7d0eec97f507411e02fd2634e3efc997a2@bitsong-seed.panthea.eu:41656
```

## RPC Endpoint

[https://bitsong-rpc.panthea.eu/](https://bitsong-rpc.panthea.eu/)

## REST/API Endpoint

[https://bitsong-api.panthea.eu/](https://bitsong-api.panthea.eu/)
