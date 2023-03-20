---
description: >-
  Desmos is a blockchain protocol powered by Forbole designed for user-centric
  social networks.
---

# Desmos (DSM)

## Snapshot (Max. 6 hours old)

**Pruning**: custom/100/0/10 - **Indexer**: null

```bash
sudo systemctl stop desmosd

cp $HOME/.desmos/data/priv_validator_state.json $HOME/.desmos/priv_validator_state.json.backup

rm -rf $HOME/.desmos/data $HOME/.desmos/wasm

curl -o - -L https://valhalla.panthea.eu/snapshots/desmos-snapshot.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.desmos

mv $HOME/.desmos/priv_validator_state.json.backup $HOME/.desmos/data/priv_validator_state.json

sudo systemctl start desmosd
```

## Wasm only (Max. 6 hours old)

[https://valhalla.panthea.eu/snapshots/desmos-wasm.tar.lz4](https://valhalla.panthea.eu/snapshots/desmos-wasm.tar.lz4)

## Addrbook

[https://valhalla.panthea.eu/addrbooks/desmos/addrbook.json](https://valhalla.panthea.eu/addrbooks/desmos/addrbook.json)

## Genesis file

[https://valhalla.panthea.eu/genesis/desmos/genesis.json](https://valhalla.panthea.eu/genesis/desmos/genesis.json)

## Persistent Peer

```url
7c506d9e32cfc486ea714ee0c0307022398b8c20@desmos-peer.panthea.eu:29656
```

## Seed Node

```url
73fc6b8b41aada42306b2f149619cc0ff935a868@desmos-seed.panthea.eu:39656
```
