
# Architecture

The system architecture has two major components:

Smart Contracts: manage ceremony creation, vote submission, and tallying.

Burn Circuits: Circom circuits enforcing the validity of burn addresses, nullifiers, and Merkle proofs.


## Smart Contract Architecture

### VotingFactory

location: `contracts/src/VotingFactory.sol`

Factory contract is responsible for deploying new voting ceremonies contracts with following parameters:

- **Verifier Address**: Deployed Groth16 verifier (BN254)

- **Voting Deadline**: UNIX timestamp to lock voting

- **Tally Deadline**: UNIX timestamp, after this anyone can call tallyVotes() function

- **Merkle Root**: Allow-list root for eligible voters ids

- **State Root**: Ethereum state root at voting end (for verifying burn balances)

- **Ceremony ID**: Unique voting identifier

- **Salt**: Unique salt for deterministic contract address generation


### Voting Contract

location: `contracts/src/Voting.sol`

Each deployed voting contract instance implements the core voting logic:

Key functions:
- `submitVote(proofA, proofB, proofC, [nullifier, voteValue, revoteFlag, stateRoot, merkleProof, ceremonyId])`: Submits a vote with a zero-knowledge proof
- `submitRevote(...)`: Overwrites a previous vote if the nullifier matches
- `tallyVotes()`: Computes and publishes the final outcome after the tally deadline

The factory pattern allows for:
- Deterministic contract addresses based on salt
- Multiple concurrent voting instances
- Gas-efficient deployment of new voting contracts
- Easy tracking of all deployed voting instances

## Circom Circuits

Under `circuits/`:

- **`Vote.circom`**:  
  - Computes burn address: `address == H(secret ∥ ceremonyID ∥ vote ∥ blindingFactor)`.  
  - Computes nullifier: `address == H(secret ∥ ceremonyID ∥ blindingFactor)`.  
  - Verifies Merkle Patricia inclusion (`stateRoot`, `accountRLP`, `accountProof`).  
- **`rlp.circom`**: Supporting subcircuits.
