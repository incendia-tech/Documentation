
**Initiate a Ceremony**

Generates initial voting setup parameters for Ganache, Sepolia, or Ethereum.

```
cargo run -- initiate --network [NETWORK]

```

**Vote**

Burns ETH, creates the proof, and submits the vote. If you don’t specify a ceremony ID, it uses the latest generated one. 

```
cargo run -- vote \
  --amount [ETH] \
  --vote [VOTE_VALUE] \
  --revote [REVOTE_FLAG] \
  --private-key [PRIVATE_KEY] \
  --ceremony-id [CEREMONY_ID]

```

**Tally**

Calculates and outputs results after the tally deadline. Defaults to the latest ceremony if ID isn’t provided.

```
cargo run -- tally --ceremony-id [CEREMONY_ID]

```

**Demo (Offline, Fast)**
Runs a full in-memory ceremony (proof generation, verification, Merkle tree handling) without on-chain integration.

```
cargo run -- demo [PRIVATE_KEY]

```

**On-chain Demo**
Deploys smart contracts on-chain, submits a sample proof, and retrieves tally results. 

```
make contracts
cargo run -- onchain-demo [PRIVATE_KEY]

```