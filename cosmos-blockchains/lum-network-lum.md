# Lum Network (LUM)

## Snapshot (Max. 4 hours old) <a href="#snapshot" id="snapshot"></a>

```bash
sudo systemctl stop lumd

cp $HOME/.lumd/data/priv_validator_state.json $HOME/.lumd/priv_validator_state.json.backup

rm -rf $HOME/.lumd/data

curl -o - -L https://valhalla.panthea.eu/snapshots/lum-snapshot.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.lumd

mv $HOME/.lumd/priv_validator_state.json.backup $HOME/.lumd/data/priv_validator_state.json

sudo systemctl start lumd
```

## State Sync

```bash
SNAP_RPC="https://lum-rpc.panthea.eu:443"

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.lumd/config/config.toml

sudo systemctl stop lumd

cp $HOME/.lumd/data/priv_validator_state.json $HOME/.lumd/priv_validator_state.json.backup

lumd tendermint unsafe-reset-all --keep-addr-book --home "$HOME/.lumd"

mv $HOME/.lumd/priv_validator_state.json.backup $HOME/.lumd/data/priv_validator_state.json

sudo systemctl start lumd
```

## Addrbook (Updated every hour) <a href="#addrbook" id="addrbook"></a>

[https://valhalla.panthea.eu/addrbooks/lum/addrbook.json](https://valhalla.panthea.eu/addrbooks/lum/addrbook.json)

```bash
curl -Ls https://valhalla.panthea.eu/addrbooks/lum/addrbook.json > $HOME/.lumd/config/addrbook.json
```

## Genesis file

[https://valhalla.panthea.eu/genesis/lum/genesis.json](https://valhalla.panthea.eu/genesis/lum/genesis.json)

```bash
curl -Ls https://valhalla.panthea.eu/genesis/lum/genesis.json > $HOME/.lumd/config/genesis.json
```
