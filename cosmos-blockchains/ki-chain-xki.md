---
description: >-
  Open-source, public blockchain designed to enable decentralized finance, built
  with the Cosmos SDK.
---

# Ki Chain (XKI)

## Snapshot (Max. 6 hours old)

**Pruning**: custom/100/0/10 - **Indexer**: null

```bash
sudo systemctl stop kid

cp $HOME/.kid/data/priv_validator_state.json $HOME/.kid/priv_validator_state.json.backup

rm -rf $HOME/.kid/data/

curl -o - -L https://valhalla.panthea.eu/snapshots/kichain-snapshot.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.kid

mv $HOME/.kid/priv_validator_state.json.backup $HOME/.kid/data/priv_validator_state.json

sudo systemctl start kid
```

## Addrbook

[https://valhalla.panthea.eu/addrbooks/kichain/addrbook.json](https://valhalla.panthea.eu/addrbooks/kichain/addrbook.json)

## State Sync

```
Not available!
```

## Persistent Peer

```url
e7bab76ef15493aaee6f91a0652ba098838a0bfb@kichain-peer.panthea.eu:28656
```

## Seed Node

```url
8edd80b2e7e807af9617d643dcbf5125425cab68@kichain-seed.panthea.eu:38656
```
