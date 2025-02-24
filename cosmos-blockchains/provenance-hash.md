# Provenance (HASH)

Provenance is a blockchain platform designed for financial services, enabling secure and transparent transactions, asset tokenization, and streamlined processes. It offers a decentralized ledger that enhances the efficiency and transparency of financial operations, such as loan origination, trading, and asset servicing. By utilizing smart contracts, Provenance reduces costs and operational risks while ensuring compliance and data integrity. The platform supports the creation and management of digital assets, facilitating instant settlement and immutable record-keeping, making it a powerful tool for financial institutions looking to modernize their infrastructure.

## State Sync

```bash
SNAP_RPC="https://provenance-rpc.panthea.eu:443"

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.provenanced/config/config.toml

sudo systemctl stop provenanced

cp $HOME/.provenanced/data/priv_validator_state.json $HOME/.provenanced/priv_validator_state.json.backup

provenanced tendermint unsafe-reset-all --keep-addr-book --home "$HOME/.provenanced"

mv $HOME/.provenanced/priv_validator_state.json.backup $HOME/.provenanced/data/priv_validator_state.json

curl -o - -L https://valhalla.panthea.eu/snapshots/provenance-wasm.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.provenanced/data/

sudo systemctl start provenanced
```

## Wasm Only

[https://valhalla.panthea.eu/snapshots/provenance-wasm.tar.lz4](https://valhalla.panthea.eu/snapshots/provenance-wasm.tar.lz4)

```bash
curl -o - -L https://valhalla.panthea.eu/snapshots/provenance-wasm.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.provenanced/data/
```

## Addrbook (Updated every 8 hours) <a href="#addrbook" id="addrbook"></a>

[https://valhalla.panthea.eu/addrbooks/provenance/addrbook.json](https://valhalla.panthea.eu/addrbooks/provenance/addrbook.json)

```bash
curl -Ls https://valhalla.panthea.eu/addrbooks/provenance/addrbook.json > $HOME/.provenanced/config/addrbook.json
```

## Genesis file

[https://valhalla.panthea.eu/genesis/provenance/genesis.json](https://valhalla.panthea.eu/genesis/provenance/genesis.json)

```bash
curl -Ls https://valhalla.panthea.eu/genesis/provenance/genesis.json > $HOME/.provenanced/config/genesis.json
```

## Persistent Peer

```uri
aa808927715ad82be258605060c21fc5afc1cd00@provenance-peer.panthea.eu:34656
```

## Seed Node

```url
ad3386812bb9f2fee4e9da6d9f37547afc948977@provenance-seed.panthea.eu:42656
```

## gRPC Endpoint

provenance-grpc.panthea.eu:16780

## RPC Endpoint

[https://provenance-rpc.panthea.eu/](https://provenance-rpc.panthea.eu/)

## REST/API Endpoint

[https://provenance-api.panthea.eu/](https://provenance-api.panthea.eu/)
