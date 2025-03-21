# Shentu (CTK)

Shentu, formerly known as CertiK Chain, is a blockchain focused on security and reliability. It provides a secure infrastructure for decentralized applications (dApps) and smart contracts by incorporating built-in security features and formal verification methods. Shentu allows developers to create and audit smart contracts with enhanced security measures, ensuring that vulnerabilities are minimized. The platform's native token, $CTK, is used for staking, governance, and accessing various security services within the ecosystem. Shentu's goal is to create a trustless and secure blockchain environment, prioritizing the safety and integrity of decentralized systems.

## Snapshot (Max. 4 hours old) <a href="#snapshot" id="snapshot"></a>

```bash
sudo systemctl stop shentud

cp $HOME/.shentud/data/priv_validator_state.json $HOME/.shentud/priv_validator_state.json.backup

rm -rf $HOME/.shentud/data

curl -o - -L https://valhalla.panthea.eu/snapshots/shentu-snapshot.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.shentud

mv $HOME/.shentud/priv_validator_state.json.backup $HOME/.shentud/data/priv_validator_state.json

sudo systemctl start shentud
```

## State Sync

```bash
SNAP_RPC="https://shentu-rpc.panthea.eu:443"

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.shentud/config/config.toml

sudo systemctl stop shentud

cp $HOME/.shentud/data/priv_validator_state.json $HOME/.shentud/priv_validator_state.json.backup

shentud tendermint unsafe-reset-all --keep-addr-book --home "$HOME/.shentud"

mv $HOME/.shentud/priv_validator_state.json.backup $HOME/.shentud/data/priv_validator_state.json

sudo systemctl start shentud
```

## Addrbook (Updated every 8 hours)

[https://valhalla.panthea.eu/addrbooks/shentu/addrbook.json](https://valhalla.panthea.eu/addrbooks/shentu/addrbook.json)

```bash
curl -Ls https://valhalla.panthea.eu/addrbooks/shentu/addrbook.json > $HOME/.shentud/config/addrbook.json
```

## Genesis file

[https://valhalla.panthea.eu/genesis/shentu/genesis.json](https://valhalla.panthea.eu/genesis/shentu/genesis.json)

```bash
curl -Ls https://valhalla.panthea.eu/genesis/shentu/genesis.json > $HOME/.shentud/config/genesis.json
```

## Persistent Peer

```url
207c47bed435e4174844064ef3f51ca35b059de2@shentu-peer.panthea.eu:26656
```

## Seed Node

```url
3edd4e16b791218b623f883d04f8aa5c3ff2cca6@shentu-seed.panthea.eu:36656
```

## gRPC Endpoint

shentu-grpc.panthea.eu:16700

## RPC Endpoint

[https://shentu-rpc.panthea.eu/](https://shentu-rpc.panthea.eu/)

## REST/API Endpoint

[https://shentu-api.panthea.eu/](https://shentu-api.panthea.eu/)
