# BitCanna (BCNA)

Bitcanna is a blockchain platform tailored for the cannabis industry, offering secure payment processing, supply chain transparency, and decentralized identity management. Its native cryptocurrency, $BCNA, enables transactions in regions where traditional banking services are limited due to cannabis regulations. The platform ensures traceability from seed to sale, enhancing consumer trust and regulatory compliance. Bitcanna also features a reputation system for product and business reviews, aiming to standardize and streamline operations within the global cannabis market.

## State Sync

```bash
SNAP_RPC="https://bitcanna-rpc.panthea.eu:443"

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.bcna/config/config.toml

sudo systemctl stop bcnad

cp $HOME/.bcna/data/priv_validator_state.json $HOME/.bcna/priv_validator_state.json.backup

bcnad tendermint unsafe-reset-all --keep-addr-book --home "$HOME/.bcna"

mv $HOME/.bcna/priv_validator_state.json.backup $HOME/.bcna/data/priv_validator_state.json

sudo systemctl start bcnad
```
