# BitCanna (BCNA)

Bitcanna is a blockchain platform tailored for the cannabis industry, offering secure payment processing, supply chain transparency, and decentralized identity management. Its native cryptocurrency, $BCNA, enables transactions in regions where traditional banking services are limited due to cannabis regulations. The platform ensures traceability from seed to sale, enhancing consumer trust and regulatory compliance. Bitcanna also features a reputation system for product and business reviews, aiming to standardize and streamline operations within the global cannabis market.

## Snapshot (Max. 4 hours old) <a href="#snapshot" id="snapshot"></a>

```bash
sudo systemctl stop bcnad

cp $HOME/.bcna/data/priv_validator_state.json $HOME/.bcna/priv_validator_state.json.backup

rm -rf $HOME/.bcna/data

curl -o - -L https://valhalla.panthea.eu/snapshots/bitcanna-snapshot.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.bcna

mv $HOME/.bcna/priv_validator_state.json.backup $HOME/.bcna/data/priv_validator_state.json

sudo systemctl start bcnad
```

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

## Addrbook (Updated every hour) <a href="#addrbook" id="addrbook"></a>

[https://valhalla.panthea.eu/addrbooks/bitcanna/addrbook.json](https://valhalla.panthea.eu/addrbooks/bitcanna/addrbook.json)&#x20;

```bash
curl -Ls https://valhalla.panthea.eu/addrbooks/bitcanna/addrbook.json > $HOME/.bcna/config/addrbook.json
```

## Genesis file

[https://valhalla.panthea.eu/genesis/bitcanna/genesis.json](https://valhalla.panthea.eu/genesis/bitcanna/genesis.json)

```bash
curl -Ls https://valhalla.panthea.eu/genesis/bitcanna/genesis.json > $HOME/.bcna/config/genesis.json
```

## Persistent Peer

```url
0a658df9d9fab096983a12e6f878e87281a15ce6@bitcanna-peer.panthea.eu:27656
```

## Seed Node

```url
f0e6c86d769bf5c52f78e01864091690e731643f@bitcanna-seed.panthea.eu:37656
```

## gRPC Endpoint

bitcanna-grpc.panthea.eu:16710

## RPC Endpoint

[https://bitcanna-rpc.panthea.eu/](https://bitcanna-rpc.panthea.eu/)

## REST/API Endpoint

[https://bitcanna-api.panthea.eu/](https://bitcanna-api.panthea.eu/)
