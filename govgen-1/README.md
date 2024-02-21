# 🔗 `govgen-1`

![chain-id](https://img.shields.io/badge/chain%20id-govgen--1-blue?style=for-the-badge)

## Register in the Genesis

To register your validator node in the `genesis.json` you just need to provide a signed `gentx` with an initial delegation of `10000000000ugovgen`.

```sh
# Init node
govgend init your-moniker --chain-id govgen-1

# Create keys, be careful with the mnemonic 👀
govgend keys add your-key-name

# Set account necessary balance
govgend add-genesis-account your-key-name 10000000ugovgen
```

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
