---
description: A Cosmos SDK-based blockchain designed for on-chain user reviews and rewards.
---

# Lum Network (LUM)

## State Sync

```bash
#!/bin/bash

SNAP_RPC="https://lum-rpc.panthea.eu:443"

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.lumd/config/config.toml

service lumd stop
lumd tendermint unsafe-reset-all --keep-addr-book --home "$HOME/.lumd"
service lumd start
```

## Persistent Peer

```url
43216584c1e6b1056566a4825b15cdfbfc79d9e8@lum-peer.panthea.eu:33656
```

## Seed Node

```url
0df233b1eb62504f96a856ce358014b2fb8ce91b@lum-seed.panthea.eu:43656
```
