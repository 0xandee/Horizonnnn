# Aztec Protocol: Comprehensive Overview

*Source: [Aztec Handbook by Wonderland](https://aztec.handbook.wonderland.xyz/)*

**Important Disclaimer**: This handbook contains internal onboarding material created by Wonderland for working with partners. It's not official documentation and may not reflect the latest updates.

---

## What is Aztec?

Aztec is a **privacy-first Layer 2 rollup on Ethereum** where developers and users get to decide what stays private and what becomes public. It enables developers to build smart contracts with selectable privacy levels—some functions execute privately on users' devices, while others run transparently like standard Ethereum contracts.

### Core Value Proposition

Aztec addresses a fundamental gap in blockchain adoption: **mainstream users need financial privacy comparable to traditional banking**. Currently, most blockchains expose all transaction data publicly, which conflicts with mass adoption. Aztec aims to enable everyday users to participate in decentralized finance with privacy protection.

### Key Differentiator

Unlike privacy solutions added retroactively to existing blockchains, **Aztec built privacy from the ground up**, making it a foundational architectural principle rather than an add-on feature.

---

## Privacy Mechanism

The system operates through **zero-knowledge proofs**:

- Users' devices generate cryptographic proofs demonstrating transaction validity and sufficient funds
- These proofs are validated **without revealing transaction amounts or source information**
- The network validates these proofs and updates state accordingly
- Privacy is maintained while ensuring cryptographic verifiability

---

## Core Concepts

### 1. Notes

**Definition**: A note is a cryptographically committed, privately owned data object representing a discrete unit of value or state. It functions as the internal representation of a UTXO and serves as the atomic unit of private state within Aztec.

#### Six Essential Properties

1. **Append Only**: Notes cannot be modified and remain linked to specific contracts

2. **Cryptographically Committed**: Rather than storing raw notes on-chain, a cryptographic hash of the note (the `note_commitment`) is computed and stored

3. **Encrypted and Privately Owned**: Notes are encrypted using recipients' public keys, ensuring only rightful owners with secret viewing keys can decrypt them

4. **Atomic State Units**: Each note represents an indivisible unit of value; state changes involve consuming old notes and creating new ones

5. **Spendable via Nullifiers**: Owners generate unique, irreversible identifiers called nullifiers to prevent double-spending. Once published, a nullifier permanently marks a note as consumed

6. **No Location-Based Relationship**: Ownership is embedded within note data itself, not implied by storage location, enhancing privacy

#### Note Structure

In Aztec.nr (Aztec's smart contract language), the `#[note]` attribute automates implementation of necessary cryptographic functions. A basic note struct includes:
- Data fields
- Owner address
- Auto-generated commitment and nullifier calculations

#### The Note Hash Tree

Instead of storing complete notes on-chain, only their commitments populate a specialized Merkle tree called the **note hash tree**, enabling efficient inclusion proofs without revealing sensitive details.

#### Note Lifecycle

**1. Creation**
- Private functions emit newly created notes
- Contents are encrypted to recipients' public keys

**2. Commitment & Insertion**
- Computed commitments are inserted into the global note hash tree on-chain

**3. Discovery**
- Recipients use "note tagging"—unique tags derived from shared secrets between sender and recipient
- This enables efficient note identification without trial-decryption

**4. Spending/Nullification**
- When spending a note, owners provide its preimage and private spending key within a zero-knowledge circuit
- The computed nullifier is published on-chain and inserted into the nullifier tree
- This permanently marks the note as spent

#### Private Payment Example

Alice's 100 DAI payment to Bob:
1. Alice nullifies her 100 DAI note
2. Creates two new notes:
   - 25 DAI (encrypted to Bob)
   - 75 DAI change (encrypted to Alice)
3. Bob's PXE discovers the tagged 25 DAI note and decrypts it
4. When Bob spends it later, he generates its nullifier, preventing double-spending

---

### 2. Nullifiers

**Purpose**: Nullifiers serve as unique cryptographic fingerprints derived from a spent note that enable the protocol to prevent double-spending while preserving privacy. They function as non-linkable yet verifiable evidence of note consumption.

#### Key Properties

- **Non-reversible**: Cannot be reverse-engineered to expose the original note or spender identity
- **Unlinkable**: Do not connect to newly created notes in the same transaction
- **Deterministic**: Prevent note reuse within specific contexts
- **Non-malleable**: Cannot be modified without invalidating accompanying cryptographic proofs

#### Technical Implementation

The canonical computation follows this structure:

```
nullifier = H(note_secret_data, secret_key, constant)
```

**Components**:
- The note's value, randomness, and asset type
- The owner's secret key
- A circuit-specific constant for domain separation

**Hash Function**: The system employs `poseidon2_hash_with_separator` as its collision-resistant hash function.

#### Role in Privacy Architecture

- Nullifiers are inserted into a **nullifier tree**
- Siloed by contract address to ensure uniqueness across contracts
- This prevents reuse while maintaining the separation of concerns across different smart contracts

#### Verification Mechanism

Before transaction acceptance, the system verifies that generated nullifiers don't already exist in the tree, using proofs like `prove_nullifier_non_inclusion` for validation purposes.

---

## Architecture & Stack

### Core State Structure

Aztec's architecture employs a **multi-tree approach** rather than traditional single key-value stores. The system maintains "a cryptographically authenticated set of data structures that encode the persistent status of the network."

### Key Components

#### Private State Trees

1. **Note Hash Tree**
   - Append-only structure
   - Stores encrypted note commitments
   - Enables efficient inclusion proofs

2. **Nullifier Tree**
   - Indexed Merkle tree
   - Prevents double-spends by tracking spent notes
   - Siloed by contract for isolation

#### Public State

**Public Data Tree**
- Indexed key-value store
- Supports membership and non-membership proofs
- Functions like traditional smart contract state

#### Supporting Trees

- **L1→L2 Message Tree**: For cross-chain messaging with Ethereum
- **Archive Tree**: Preserves historic block headers

### Design Principle: Read = Write

A distinctive architectural feature: reading private notes requires **"nullifying the note after every read and immediately re-creating it"** with a fresh nonce.

**Benefits**:
- Ensures users always access current values while maintaining privacy
- The sequencer performs non-membership checks at the chain head
- Users don't need to prove non-membership themselves

### Privacy Protection

Nullifiers employ isolation strategies:
- **Siloed by contract**: Prevents cross-contract interference
- **Deterministically derived** from note data using secrets
- Prevents linking notes to their nullifiers

### Efficiency Optimization

The system uses unbalanced **"wonky trees"** for efficient rollup composition without padding empty transactions.

---

## Architecture Layers

The handbook is organized into four main technical areas:

### 1. Background (Available)
- UTXOs and the note-based model
- Nullifiers and double-spend prevention
- Zero-knowledge proof fundamentals
- Privacy mechanisms

### 2. Stack (In Progress)
- Virtual machine execution
- Proof generation
- Multi-tree state structure
- PXE (Private Execution Environment)

### 3. Transactions & Messaging (Coming Soon)
- Private/public function interaction
- Cross-layer messaging with Ethereum L1
- Transaction lifecycle

### 4. Consensus (Coming Soon)
- Network agreement mechanisms
- Block production
- Sequencer operations

---

## Development

### Aztec.nr

Aztec's smart contract language built on Noir (a zero-knowledge proof language).

**Features**:
- `#[note]` attribute for automatic cryptographic function generation
- Support for both private and public functions in the same contract
- Native privacy primitives

### Key Development Concepts

- **Private Functions**: Execute on users' devices, generate ZK proofs
- **Public Functions**: Execute transparently on the network like standard smart contracts
- **Selective Privacy**: Developers choose which functions are private vs public

---

## Use Cases

Given Aztec's privacy-first architecture, ideal applications include:

- **Private DeFi**: Trading, lending, and financial services with transaction privacy
- **Confidential Payments**: Private transfers while maintaining verifiability
- **Private Governance**: Voting and coordination with ballot secrecy
- **Compliance with Privacy**: Selective disclosure for regulatory requirements
- **Supply Chain Privacy**: Confidential business transactions on-chain
- **Identity & Credentials**: Privacy-preserving attestations and verifications

---

## Technical Highlights

### Privacy by Default
- All private state is encrypted and commitments are stored on-chain
- Only the owner can decrypt their notes using secret keys
- Transaction amounts and participants remain confidential

### Zero-Knowledge Proofs
- Users prove transaction validity without revealing transaction details
- Proofs are verified by the network
- Enables privacy while maintaining verifiability

### UTXO-Based Model
- Notes are immutable units of value/state
- State changes involve consuming old notes and creating new ones
- Provides better privacy properties than account-based models

### Ethereum Compatibility
- Built as a Layer 2 rollup on Ethereum
- Inherits Ethereum's security guarantees
- Supports cross-layer messaging

### Flexible Privacy Model
- Developers choose which functions are private vs public
- Same contract can have both private and public state
- Enables gradual migration and hybrid applications

---

## Resources

- **Handbook**: https://aztec.handbook.wonderland.xyz/
- **Official Aztec Protocol**: https://aztec.network/
- **Aztec Discord**: https://discord.com/invite/JtqzkdeQ6G
- **Development Boilerplate**: https://github.com/defi-wonderland/aztec-boilerplate
- **Awesome Aztec**: https://github.com/AztecProtocol/awesome-aztec

---

## Important Notes

1. **Documentation Status**: This handbook is internal onboarding material and may not reflect the latest protocol updates. Refer to official Aztec documentation for production use.

2. **Active Development**: Some sections (Transactions, Consensus) are marked as "Coming Soon," indicating the protocol and documentation are under active development.

3. **Privacy-First Philosophy**: Unlike retrofitted privacy solutions, Aztec's architecture is built from the ground up with privacy as a core design principle.

---

*Last Updated: 2025-01-21*
*Compiled from: Aztec Handbook by Wonderland*
