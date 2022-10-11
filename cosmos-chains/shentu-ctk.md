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
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.certik/config/config.toml

sudo service certik stop
certik unsafe-reset-all
sudo service certik start
```

## Persistent Peer

```url
207c47bed435e4174844064ef3f51ca35b059de2@shentu-peer.panthea.eu:26656
```
