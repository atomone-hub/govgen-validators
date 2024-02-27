# 🔗 `govgen-1`

![chain-id](https://img.shields.io/badge/chain%20id-govgen--1-blue?style=for-the-badge)
![version: v1.0.1](https://img.shields.io/badge/version-v1.0.1-green?style=for-the-badge)
![genesis-time](https://img.shields.io/badge/%E2%8F%B0%20genesis%20time-2024--02--27T14%3A00%3A00Z-red?style=for-the-badge)


## Register in the Genesis

To register your validator node in the `genesis.json` you just need to provide a signed `gentx` with an initial delegation of `1000000ugovgen`.

```sh
# Init node
govgend init your-moniker --chain-id govgen-1

# Create keys, be careful with the mnemonic 👀
govgend keys add your-key-name

# Set account necessary balance
govgend add-genesis-account your-key-name 10000000ugovgen
```
*NOTE*: if you are submitting a gentx for a new account, (meaning you had to run the command above because the account did not have balance) be aware that you will be granted some funds (including the 1000000ugovgen required as min self-delegation), enough to pay for fees. The amount above is indicative of the actual amount of funds you will be granted, but the final amount might change.

Then create your own genesis transaction (`gentx`). You will have to choose the following parameters for your validator: `commission-rate`, `commission-max-rate`, `commission-max-change-rate` all set to 0, `min-self-delegation` (>=1), `website` (optional), `details` (optional), `identity` ([keybase](https://keybase.io) key hash, used to get validator logos in block explorers - optional), `security-contact` (email - optional).

The `commission-rate`, `commission-max-rate`, `commission-max-change-rate` are recommended to be set to 0  since rewards and inflations are both set to 0.

```sh
# Create the gentx
govgend gentx your-key-name 1000000ugovgen \
  --node-id $(govgend tendermint show-node-id) \
  --chain-id govgen-1 \
  --commission-rate 0.0 \
  --commission-max-rate 0.0 \
  --commission-max-change-rate 0.0 \
  --min-self-delegation 1 \
  --website "https://foo.network" \
  --details "My validator" \
  --identity "id-from-keybase" \
  --security-contact "security@foo.network"
```

## Operate the node 

### Install the binary

- You can install the binary from github release page

https://github.com/atomone-hub/govgen/releases/tag/v1.0.1

- Build from the source

You need to have [go](https://go.dev/doc/install) installed

```sh
$ git clone https://github.com/atomone-hub/govgen.git
$ cd govgen
$ make install
```

### Genesis file [download link](https://atomone.fra1.digitaloceanspaces.com/govgen/govgen-1/genesis.json)

The final genesis is avalable at [this link](https://atomone.fra1.digitaloceanspaces.com/govgen/govgen-1/genesis.json).
More info on the genesis can be found at https://github.com/atomone-hub/govgen-genesis

```sh
$ wget -O ~/.govgen/config/genesis.json https://atomone.fra1.digitaloceanspaces.com/govgen/govgen-1/genesis.json
$ md5sum ~/.govgen/config/genesis.json
8ff1071744159cb8efce69edb6ca7d46
```

### Recommendations

| minimum-gas-prices | 0.001ugovgen                                         |
|--------------------|------------------------------------------------------|
| seeds              | see [./seeds.txt](./seeds.txt)                       |
| persistent_peers   | see [./persistent_peers.txt](./persistent_peers.txt) |


## Hardware recommendation

GovGen is a relatively simple and vanilla Cosmos SDK chain with minor modifications. The recommended minimum hardware requirements should be enough to comfortably be able to run a validator node.

- 4 Cores
- 8 GB RAM
- 512 GB disk space (could increase over time, will need to monitor disk usage)


