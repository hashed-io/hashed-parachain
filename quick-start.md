# Launch the Relay Chain
```bash
# Clone
cd ~/github.com/paritytech

git clone https://github.com/paritytech/polkadot
cd polkadot

# Compile Polkadot with the real overseer feature
cargo build --release

# Generate a raw chain spec
./target/release/polkadot build-spec --chain rococo-local --disable-default-bootnode --raw > ~/github.com/paritytech/polkadot/rococo-custom-2-raw.json \
e.json

# Alice
./target/release/polkadot --chain ~/github.com/paritytech/polkadot/rococo-custom-2-raw.json --alice --tmp

# Bob (In a separate terminal)
./target/release/polkadot --chain ~/github.com/paritytech/polkadot/rococo-custom-2-raw.json --bob --tmp --port 30334
```
# Reserve the Para ID 
Go to https://polkadot.js.org/apps/?rpc=ws%3A%2F%2F127.0.0.1%3A9944#/parachains/parathreads

and Click `+ParaID`

# Launch the Parachain

```bash

cd ~/github.com/hashed-io

# Clone
git clone https://github.com/hashed-io/hashed-parachain
cd hashed-parachain

# Compile
cargo build --release

# Assumes that `rococo-local` is in `node/chan_spec.rs` as the relay you registered with
./target/release/hashed-parachain-node build-spec --disable-default-bootnode > rococo-local-parachain-plain.json
```

# Add the ParaID
Update `rococo-local-parachain-plain.json` and change the parachain ID to 2000 in two places.

```json
// --snip--
  "para_id": 2000, // <--- your already registered ID
  // --snip--
      "parachainInfo": {
        "parachainId": 2000 // <--- your already registered ID
      },
  // --snip--
```
# Build the Raw Spec File
```bash
# build raw spec 
./target/release/hashed-parachain-node build-spec --chain rococo-local-parachain-plain.json --raw --disable-default-bootnode > rococo-local-parachain-2000-raw.json
```

# Building genesis state and wasm files
```bash
./target/release/hashed-parachain-node export-genesis-state --chain rococo-local-parachain-2000-raw.json > para-2000-genesis

./target/release/hashed-parachain-node export-genesis-wasm --chain rococo-local-parachain-2000-raw.json > para-2000-wasm
```

# Start Collator 
```bash
./target/release/hashed-parachain-node \
    --alice \
    --collator \
    --force-authoring \
    --chain rococo-local-parachain-2000-raw.json \
    --base-path /tmp/parachain/alice \
    --port 40333 \
    --ws-port 8844 \
    -- \
    --execution wasm \
    --chain ~/github.com/paritytech/polkadot/rococo-custom-2-raw.json \
    --port 30343 \
    --ws-port 9977

```

## Sudo Register the parachain
![image](https://user-images.githubusercontent.com/2915325/99548884-1be13580-2987-11eb-9a8b-20be658d34f9.png)


### Purging the Chains
```bash
# Purge a chain
./target/release/hashed-parachain-node \
    purge-chain \
    --base-path /tmp/parachain/alice \
    --chain ~/github.com/hashed-io/hashed-parachain/hashed-parachain-2000-raw.json

# Purge relay chain
./target/release/polkadot purge-chain --base-path /tmp/relay/alice --chain ~/github.com/paritytech/polkadot/rococo-custom-2-raw.json 

```
