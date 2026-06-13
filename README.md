[![CI Status](https://github.com/stellarspend/stellarspend-contracts/actions/workflows/contract-ci.yml/badge.svg)](https://github.com/stellarspend/stellarspend-contracts/actions/workflows/contract-ci.yml)
# stellarspend-contracts
Soroban smart contracts for automated budgets, savings goals, and spending limits on Stellar
Smart contracts powering StellarSpend financial logic on the Stellar blockchain using Soroban.

---

## Overview

**StellarSpend Contracts** are a collection of **Soroban smart contracts written in Rust** that power the core financial logic of the StellarSpend ecosystem. These contracts enable secure, transparent, and low-cost financial interactions for users, including budgeting, savings, and on-chain data verification.

They are designed to support **financial inclusion**, **self-sovereign identity**, and **trustless execution** for unbanked and underbanked users globally.

---

## Key Feature

- **On-Chain Budget Logic** — Enforces spending limits and budget rules
- **Savings Vaults** — Smart-contract–based savings and goal tracking
- **Self-Custody** — Users retain full control of their assets
- **Low Fees & Fast Execution** — Powered by Stellar + Soroban
- **Composable Contracts** — Designed to integrate with backend & frontend
- **Deterministic & Secure** — Written in Rust with predictable execution
- **Network Agnostic** — Works on Testnet & Mainnet
- **Open & Auditable** — Fully transparent smart contract logic

---
## Product / Website
StellarSpend is the smart-contract layer for automated budgets, savings goals, and spending limit features on Stellar. If a public website or product documentation exists, add the reference here so contributors know where to learn more.

---
## Contributing
We welcome contributions!

1. Fork the repository
2. Create a branch: `git checkout -b feature/short-description`
3. Implement changes and add tests where applicable
4. Run linters and tests locally
5. Open a clear Pull Request describing the changes
6. Look for issues and link them in your PR

## Quick Start

### Prerequisites

- Rust (stable)
- `rustup`
- Soroban CLI

Install Soroban CLI:

```bash
cargo install --locked soroban-cli
```

Add the WASM build target (needed for Soroban contracts):

```bash
rustup target add wasm32-unknown-unknown
```

### Build

Build a single contract to WASM:

```bash
cargo build -p batch-conversion --target wasm32-unknown-unknown --release
```

### Test

Run tests for a single contract:

```bash
cargo test -p batch-conversion
```

Run all workspace tests:

```bash
cargo test --workspace
```

## Contributing

We welcome contributions.

1. Fork the repository
2. Create a branch: `git checkout -b feature/short-description`
3. Implement changes and add/update tests where applicable
4. Run tests locally
5. Open a Pull Request with a clear description


---

## ZK Private Spending Proof (Stellar Hacks Submission)

We added zero-knowledge proof verification to the spending limits contract. Users can now prove their payment is within their spending limit **without revealing the actual payment amount**.

### How It Works

1. User generates a ZK proof off-chain using the Noir circuit in `circuits/spending_proof/`
2. Proof is submitted to the `zk-verifier` Soroban contract on Stellar
3. Contract verifies the proof on-chain
4. Payment approved or rejected — amount stays completely private

### Why This Matters

StellarSpend handles real payments on Stellar. Adding ZK means:
- Payment amounts are never revealed on-chain
- Spending limits are still enforced cryptographically
- No trust required — math proves it

### ZK Circuit

Located in `circuits/spending_proof/src/main.nr`

### Test the Circuit

```bash
cd circuits/spending_proof && nargo check
```
