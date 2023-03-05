---
description: >-
  A blockchain hub that provides a trust-less marketplace for the music
  industry.
---

# BitSong (BTSG)

## Snapshot (Max. 6 hours old)

```bash
sudo systemctl stop bitsongd

cp $HOME/.bitsongd/data/priv_validator_state.json $HOME/.bitsongd/priv_validator_state.json.backup

rm -rf $HOME/.bitsongd/data/

curl -o - -L https://www.panthea.eu/snapshots/bitsong-snapshot.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.bitsongd

mv $HOME/.bitsongd/priv_validator_state.json.backup $HOME/.bitsongd/data/priv_validator_state.json

sudo systemctl start bitsongd
```

## State Sync

```bash
Not available!
```

## Persistent Peer

```url
2cd6bb75fc9279c62c0ef3af82fbe08632743472@bitsong-peer.panthea.eu:31656
```

## Seed Node

```url
8defec7d0eec97f507411e02fd2634e3efc997a2@bitsong-seed.panthea.eu:41656
```
