---
description: Decentralized payment network and supply chain for legal cannabis industry.
---

# BitCanna (BCNA)

## Snapshot (Max. 6 hours old)

**Pruning**: custom/100/0/10 - **Indexer**: null

```bash
sudo systemctl stop bcnad

cp $HOME/.bcna/data/priv_validator_state.json $HOME/.bcna/priv_validator_state.json.backup

rm -rf $HOME/.bcna/data

curl -o - -L https://valhalla.panthea.eu/snapshots/bitcanna-snapshot.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.bcna

mv $HOME/.bcna/priv_validator_state.json.backup $HOME/.bcna/data/priv_validator_state.json

sudo systemctl start bcnad
```

## Addrbook

[https://valhalla.panthea.eu/addrbooks/bitcanna/addrbook.json](https://valhalla.panthea.eu/addrbooks/bitcanna/addrbook.json)&#x20;

## Genesis file

[https://valhalla.panthea.eu/genesis/bitcanna/genesis.json](https://valhalla.panthea.eu/genesis/bitcanna/genesis.json)

## Persistent Peer

```url
0a658df9d9fab096983a12e6f878e87281a15ce6@bitcanna-peer.panthea.eu:27656
```

## Seed Node

```url
f0e6c86d769bf5c52f78e01864091690e731643f@bitcanna-seed.panthea.eu:37656
```
