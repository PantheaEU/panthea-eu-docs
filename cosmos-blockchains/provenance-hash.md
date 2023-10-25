---
description: >-
  A Tendermint-based blockchain network designed to support financial service
  industry.
---

# Provenance (HASH)

Wasm only (Max. 4 hours old)

[https://valhalla.panthea.eu/snapshots/provenance-wasm.tar.lz4](https://valhalla.panthea.eu/snapshots/provenance-wasm.tar.lz4)

```bash
rm -rf $HOME/.provenanced/data/wasm

curl -o - -L https://valhalla.panthea.eu/snapshots/provenance-wasm.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.provenanced/data/
```

## Addrbook (Updated every hour) <a href="#addrbook" id="addrbook"></a>

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
