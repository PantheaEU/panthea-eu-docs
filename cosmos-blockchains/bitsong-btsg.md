# BitSong (BTSG)

Bitsong is a blockchain platform designed for the music industry, aiming to empower artists and creators by providing decentralized tools for content distribution, royalty management, and fan engagement. It allows artists to tokenize their work, ensuring transparent and fair royalty payments through smart contracts. Bitsong also offers direct interaction between artists and fans, bypassing traditional intermediaries, and enabling a more equitable revenue distribution. The platform's native token, $BTSG, facilitates transactions within the ecosystem, supporting a decentralized music economy that prioritizes artists' rights and earnings.

## Snapshot (Max. 4 hours old) <a href="#snapshot" id="snapshot"></a>

```bash
sudo systemctl stop bitsongd

cp $HOME/.bitsongd/data/priv_validator_state.json $HOME/.bitsongd/priv_validator_state.json.backup

rm -rf $HOME/.bitsongd/data

curl -o - -L https://valhalla.panthea.eu/snapshots/bitsong-snapshot.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.bitsongd

mv $HOME/.bitsongd/priv_validator_state.json.backup $HOME/.bitsongd/data/priv_validator_state.json

sudo systemctl start bitsongd
```

## State Sync

```bash
SNAP_RPC="https://bitsong-rpc.panthea.eu:443"

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.bitsongd/config/config.toml

sudo systemctl stop bitsongd

cp $HOME/.bitsongd/data/priv_validator_state.json $HOME/.bitsongd/priv_validator_state.json.backup

bitsongd tendermint unsafe-reset-all --keep-addr-book --home "$HOME/.bitsongd"

mv $HOME/.bitsongd/priv_validator_state.json.backup $HOME/.bitsongd/data/priv_validator_state.json

sudo systemctl start bitsongd
```

## Addrbook (Updated every 8 hours) <a href="#addrbook" id="addrbook"></a>

[https://valhalla.panthea.eu/addrbooks/bitsong/addrbook.json](https://valhalla.panthea.eu/addrbooks/bitsong/addrbook.json)

```bash
curl -Ls https://valhalla.panthea.eu/addrbooks/bitsong/addrbook.json > $HOME/.bitsongd/config/addrbook.json
```

## Genesis file

[https://valhalla.panthea.eu/genesis/bitsong/genesis.json](https://valhalla.panthea.eu/genesis/bitsong/genesis.json)

```bash
curl -Ls https://valhalla.panthea.eu/genesis/bitsong/genesis.json > $HOME/.bitsongd/config/genesis.json
```

## Persistent Peer

```url
2cd6bb75fc9279c62c0ef3af82fbe08632743472@bitsong-peer.panthea.eu:31656
```

## Seed Node

```url
8defec7d0eec97f507411e02fd2634e3efc997a2@bitsong-seed.panthea.eu:41656
```

## gRPC Endpoint

bitsong-grpc.panthea.eu:16750

## RPC Endpoint

[https://bitsong-rpc.panthea.eu/](https://bitsong-rpc.panthea.eu/)

## REST/API Endpoint

[https://bitsong-api.panthea.eu/](https://bitsong-api.panthea.eu/)
