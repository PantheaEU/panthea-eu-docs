---
description: A Cosmos SDK-based blockchain designed for on-chain user reviews and rewards.
---

# Lum Network (LUM)

## Snapshot (Max. 6 hours old)

**Pruning**: custom/100/0/10 - **Indexer**: null

```bash
sudo systemctl stop lumd

cp $HOME/.lumd/data/priv_validator_state.json $HOME/.lumd/priv_validator_state.json.backup

rm -rf $HOME/.lumd/data/

curl -o - -L https://www.panthea.eu/snapshots/lum-snapshot.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.lumd

mv $HOME/.lumd/priv_validator_state.json.backup $HOME/.lumd/data/priv_validator_state.json

sudo systemctl start lumd
```

## State Sync

```bash
Not available!
```

## Persistent Peer

```url
43216584c1e6b1056566a4825b15cdfbfc79d9e8@lum-peer.panthea.eu:33656
```

## Seed Node

```url
0df233b1eb62504f96a856ce358014b2fb8ce91b@lum-seed.panthea.eu:43656
```
