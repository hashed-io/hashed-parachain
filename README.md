## Hashed Network

### [Open Hashed Network on polkadot.js.org](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fn1.hashed.systems#/explorer)

## Features
### Standard Pallets
#### [Identity](https://wiki.polkadot.network/docs/learn-identity)
Hashed Chain provides a naming system that allows participants to add information, such as social media accounts, web domains, email addresses, etc. to their on-chain account and subsequently ask for verification of this information by registrars.

#### [Indices](https://wiki.polkadot.network/docs/learn-accounts#indices)
An index is a short and easy-to-remember version of an address. Claiming an index requires a deposit that is released when the index is cleared.

#### [Social Recovery]()
The Recovery pallet is an M-of-N social recovery tool for users to gain access to their accounts if the private key or other authentication mechanism is lost. Through this pallet, a user is able to make calls on-behalf-of another account which they have recovered. The recovery process is protected by trusted "friends" whom the original account owner chooses. A threshold (M) out of N friends are needed to give another account access to the recoverable account.

#### [Uniques (NFTs)](https://github.com/paritytech/substrate/tree/master/frame/uniques)
A simple, secure module for dealing with non-fungible assets.

#### [Treasury](https://wiki.polkadot.network/docs/learn-treasury)
The Treasury pallet provides a "pot" of funds that can be managed by stakeholders in the system and a structure for making spending proposals from this pot.

> Roadmap: Integrate support for native multisig BTC in the treasury via PSBT and output descriptors

#### [Society](https://wiki.polkadot.network/docs/maintain-guides-society-kusama)
The Society module is an economic game which incentivizes users to participate and maintain a membership society.

#### [Bounties](https://wiki.polkadot.network/docs/learn-treasury#bounties-spending) 
Bounties Spending proposals aim to delegate the curation activity of spending proposals to experts called Curators: They can be defined as addresses with agency over a portion of the Treasury with the goal of fixing a bug or vulnerability, developing a strategy, or monitoring a set of tasks related to a specific topic: all for the benefit of the whole ecosystem.

## Custom Pallets
#### [Fruniques (FRactional UNIQUES)](https://github.com/hashed-io/hashed-substrate/tree/main/pallets/fruniques)
A Frunique is a type of Non-Fungible Token (NFT). Fruniques allow token holders to lock any set of fungible and/or non-fungible tokens into a new NFT backed by the tokens. The source/parent asset(s) can be unlocked if and only if all of its child fruniques are held by the same account. Any Frunique may be transformed to become 1..n new Fruniques or a fungible token.

Fruniques are compatible with the `Uniques` pallet referenced above.

