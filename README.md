# README.md

## Bitcoin + MATT Docker Container

This repository contains a Dockerfile to build and run a custom version of Bitcoin, based on the branch `matt` from the repository https://github.com/Merkleize/bitcoin.

It contains the same opcodes as the [bitcoin-inquisition](https://github.com/bitcoin-inquisition/bitcoin) repo, plus the following opcodes on taproot:

- `OP_CHECKCONTRACTVERIFY`
- `OP_CAT`
- `OP_CHECKSIGFROMSTACK`
- `OP_INTERNALKEY`

See [merkle.fun](https://merkle.fun) for more information.

### Features

- Lightweight image based on Ubuntu 20.04.
- Compiled with wallet support (no legacy wallet), and no GUI
- Exposes ports 18443 and 18444.
- Uses a custom `bitcoin.conf` file.

### Build the Docker Image

```bash
docker build -t bitcoin_matt .
```

### Pull from Docker hub

```bash
docker pull bigspider/bitcoin_matt
```


### Run the Docker Container

```bash
docker run -d -p 18443:18443 bigspider/bitcoin_matt
```

Exposing port 18443 allows interacting with it using `bitcoin-cli -regtest` as normal, as long as a recent version of `bitcoin-cli` is in the path.

Alternatively, once the container is running, one can access a terminal in it with:

```bash
docker exec -it <container_id> /bin/bash
```

or run a command directly, for example:

```bash
docker exec <container_id> bitcoin-cli -regtest getblockcount

```

### Configuration

A custom `bitcoin.conf` is copied to `/root/.bitcoin/bitcoin.conf` within the container.

The rpc user/pass are `rpcuser` and `rpcpass`, and some settings to enable mining transactions with zero fee are added for simplicity.

### Contributions

If you'd like to contribute or make changes to this Docker image, feel free to open a pull request or raise an issue in this repository.

### Disclaimer

Only use on regtest!
