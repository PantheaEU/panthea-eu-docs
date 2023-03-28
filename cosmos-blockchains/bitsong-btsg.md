---
description: >-
  A blockchain hub that provides a trust-less marketplace for the music
  industry.
---

# BitSong (BTSG)

## Snapshot (Max. 6 hours old)

**Pruning**: custom/100/0/10 - **Indexer**: null

```bash
sudo systemctl stop bitsongd

cp $HOME/.bitsongd/data/priv_validator_state.json $HOME/.bitsongd/priv_validator_state.json.backup

rm -rf $HOME/.bitsongd/data

curl -o - -L https://valhalla.panthea.eu/snapshots/bitsong-snapshot.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.bitsongd

mv $HOME/.bitsongd/priv_validator_state.json.backup $HOME/.bitsongd/data/priv_validator_state.json

sudo systemctl start bitsongd
```

## Wasm only (Max. 6 hours old)

[https://valhalla.panthea.eu/snapshots/bitsong-wasm.tar.lz4](https://valhalla.panthea.eu/snapshots/bitsong-wasm.tar.lz4)

## Addrbook (Updated 4 times a day)

[https://valhalla.panthea.eu/addrbooks/bitsong/addrbook.json](https://valhalla.panthea.eu/addrbooks/bitsong/addrbook.json)

## Genesis file

[https://valhalla.panthea.eu/genesis/bitsong/genesis.json](https://valhalla.panthea.eu/genesis/bitsong/genesis.json)

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
