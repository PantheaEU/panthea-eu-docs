---
description: >-
  Passage is building a virtual 3D world/metaverse that is mainly powered by
  Unreal Engine 5, Akash, and IBC.
---

# Passage (PASG)

## State Sync

```bash
#!/bin/bash

SNAP_RPC="https://passage-rpc.panthea.eu:443"

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.passage/config/config.toml

sudo service passage stop
passage tendermint unsafe-reset-all --keep-addr-book --home "$HOME/.passage"
sudo service passage start
```

## Persistent Peer

```url
054b90a8dc7b392e4b1d0e3b6d09bcb2c38251cb@passage-peer.panthea.eu:30656
```

## Seed Node

```url
ecfd6a2ab8dc2b196080ff6506cd0d1c68f6f8b5@passage-seed.panthea.eu:40656
```
