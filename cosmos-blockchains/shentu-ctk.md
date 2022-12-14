---
description: >-
  Decentralized security solution for audits, insurance, monitoring, and
  decentralized finance, built with the Cosmos SDK.
---

# Shentu (CTK)

## State Sync

```bash
#!/bin/bash

SNAP_RPC="https://shentu-rpc.panthea.eu:443"

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.shentud/config/config.toml

sudo service shentud stop
shentud tendermint unsafe-reset-all
sudo service shentud start
```

## Persistent Peer

```url
207c47bed435e4174844064ef3f51ca35b059de2@shentu-peer.panthea.eu:26656
```

## Seed Node

```url
3edd4e16b791218b623f883d04f8aa5c3ff2cca6@shentu-seed.panthea.eu:36656
```
