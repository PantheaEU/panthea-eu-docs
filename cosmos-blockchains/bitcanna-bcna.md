---
description: Decentralized payment network and supply chain for legal cannabis industry.
---

# BitCanna (BCNA)

## State Sync

```bash
#!/bin/bash

SNAP_RPC="https://bitcanna-rpc.panthea.eu:443"

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.bcna/config/config.toml

sudo service bcnad stop
bcnad tendermint unsafe-reset-all --home "$HOME/.bcna"
sudo service bcnad start
```

## Persistent Peer

```url
0a658df9d9fab096983a12e6f878e87281a15ce6@bitcanna-peer.panthea.eu:27656
```

## Seed Node

```url
f0e6c86d769bf5c52f78e01864091690e731643f@bitcanna-seed.panthea.eu:37656
```
