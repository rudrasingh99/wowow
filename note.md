# Notes on Web3 Transient Storage and BIOS CTF

## Transient Storage (EIP-1153)

Transient storage is defined in [EIP-1153](https://eips.ethereum.org/EIPS/eip-1153). It introduces two new opcodes, `TSTORE` and `TLOAD`, which behave similarly to `SSTORE` and `SLOAD` but the data is discarded at the end of the transaction. This allows contracts to store temporary data without incurring the gas costs of persistent storage.

Key properties:

- Data written with `TSTORE` is only accessible within the same transaction. After the transaction completes, the data is cleared.
- This can be used for reentrancy guards, temporary variables across calls, or caching values.

## CTF Challenge

The repository only contains a minimal README with the line `CTF challenge from BIOS`. No Solidity contracts or test files are present, so the exact challenge implementation is unavailable. Without access to the actual challenge code, it is unclear how the CTF uses EIP-1153.

In typical CTF challenges that utilize transient storage, the contract might rely on `TSTORE` to keep temporary state between internal calls. To solve such a challenge, you usually:

1. Inspect the contract bytecode or provided source to identify where `TSTORE` and `TLOAD` are used.
2. Understand what values must be written to or read from transient storage to satisfy the contract's logic.
3. Craft a transaction (or series of calls) that writes the expected values and triggers the success condition within the same transaction, since the data disappears afterward.

Because no Solidity files or tests are available here, the best approach is to obtain the actual challenge contracts and analyze how `TSTORE`/`TLOAD` are used.

## Tests

The project does not contain any Forge setup. Running `forge test` after installing Foundry results in the message `No tests found in project!`. Once the challenge contracts are added, tests should be written to replicate and solve the challenge logic.
