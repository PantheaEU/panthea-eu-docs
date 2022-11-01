---
description: >-
  A Cosmos SDK-based decentralized interchain NFT marketplace and social
  network.
---

# Stargaze (STARS)

## State Sync

```bash
#!/bin/bash

SNAP_RPC="https://stargaze-rpc.panthea.eu:443"

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.starsd/config/config.toml

sudo service starsd stop
starsd tendermint unsafe-reset-all --home "$HOME/.starsd"
sudo service starsd start
```

## Persistent Peer

```url
350dfe5fa979d4b1ee07cab2a22b130a4238105f@stargaze-peer.panthea.eu:32656
```

## Seed Node

```url
01f3e27f915811797cf0e29d593925f59328d1c7@stargaze-seed.panthea.eu:42656
```
