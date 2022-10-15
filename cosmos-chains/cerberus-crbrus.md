---
description: A community-led three-headed dog meme coin in Cosmos ecosystem.
---

# Cerberus (CRBRUS)

## State Sync

```bash
#!/bin/bash

SNAP_RPC="https://cerberus-rpc.panthea.eu:443"

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.cerberus/config/config.toml

sudo service cerberusd stop
cerberusd tendermint unsafe-reset-all --home "$HOME/.cerberus"
sudo service cerberusd start
```

## Persistent Peer

```url
ab4fe77e992354fb1c384e4eadbc05427446ada7@cerberus-peer.panthea.eu:28656
```

## Seed

```url
d94df4d4a17fa10834bb97853d91b501aa4abc4b@cerberus-seed.panthea.eu:38656
```
