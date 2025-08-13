
**Prerequisites**

Node.js (≥16.0.0)

Rust (Cargo)

Circom

Homebrew (macOS)

**1-Setup**

This sets up all required dependencies including Circomlib, snarkjs, ganache-cli, and Rapidsnark.


```
git clone git@github.com:zero-savvy/burn-to-vote.git
cd burn-to-vote
npm run install-deps
```


**2-Run a local blockchain**

Start development and testing on a local Ethereum network.

```
ganache-cli
export PRIVATE_KEY=[YOUR_PRIVATE_KEY]
```

