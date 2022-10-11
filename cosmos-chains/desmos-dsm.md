---
description: >-
  Desmos is a blockchain protocol powered by Forbole designed for user-centric
  social networks.
---

# Desmos (DSM)

## State Sync

```bash
#!/bin/bash

SNAP_RPC="https://desmos-rpc.panthea.eu:443"

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.desmos/config/config.toml

sudo service desmosd stop
desmos unsafe-reset-all
sudo service desmosd start
```

## Persistent Peer

```url
7c506d9e32cfc486ea714ee0c0307022398b8c20@161.97.125.111:29656
```
