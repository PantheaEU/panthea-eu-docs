---
description: >-
  A blockchain hub that provides a trust-less marketplace for the music
  industry.
---

# BitSong (BTSG)

## State Sync

```bash
#!/bin/bash

SNAP_RPC="https://bitsong-rpc.panthea.eu:443"

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.bitsongd/config/config.toml

sudo service bitsongd stop
bitsongd tendermint unsafe-reset-all --home "$HOME/.bitsongd"
sudo service bitsongd start
```

## Persistent Peer

```url
2cd6bb75fc9279c62c0ef3af82fbe08632743472@bitsong-peer.panthea.eu:31656
```

## Seed Node

```url
8defec7d0eec97f507411e02fd2634e3efc997a2@bitsong-seed.panthea.eu:41656
```
