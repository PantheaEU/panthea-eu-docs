---
description: A Cosmos SDK-based blockchain designed for on-chain user reviews and rewards.
---

# Lum Network (LUM)

## Snapshot (Max. 4 hours old) <a href="#snapshot" id="snapshot"></a>

**Pruning**: custom/100/0/10 - **Indexer**: null

```bash
sudo systemctl stop lumd

cp $HOME/.lumd/data/priv_validator_state.json $HOME/.lumd/priv_validator_state.json.backup

rm -rf $HOME/.lumd/data

curl -o - -L https://valhalla.panthea.eu/snapshots/lum-snapshot.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.lumd

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

## Persistent Peer

```url
43216584c1e6b1056566a4825b15cdfbfc79d9e8@lum-peer.panthea.eu:33656
```

## Seed Node

{% code fullWidth="false" %}
```url
0df233b1eb62504f96a856ce358014b2fb8ce91b@lum-seed.panthea.eu:43656
```
{% endcode %}

## gRPC Endpoint

lum-grpc.panthea.eu:16770

## RPC Endpoint

[https://lum-rpc.panthea.eu/](https://lum-rpc.panthea.eu/)

## REST/API Endpoint

[https://lum-api.panthea.eu/](https://lum-api.panthea.eu/)
