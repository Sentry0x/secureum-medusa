
# Secureum Medusa workshop

The goals of this workshop are to:
- Learn about invariants development
- Become familar with the medusa fuzzer

Medusa is a [new experimental fuzzer](https://github.com/crytic/medusa). Do not hesitate to ask questions on secureum's discord, or create [github issues](https://github.com/crytic/medusa/issues/new) if you encounter any issue.

## Before starting

To install medusa, follow [the installation instructions](https://github.com/crytic/medusa/#installation).

## The contest

The goals of the contest is to write invariants for three targets. All the contracts are coming from [solmate](https://github.com/transmissions11/solmate).

### SignedWadMath
- [`SignedWadMath`](./contracts/SignedWadMath.sol) is a signed 18 decimal fixed point (wad) arithmetic library.
- [`SignedWadMathTest](./contracts/SignedWadMathTest.sol) is an example of test for `SignedWadMath` 

### FixedPointMathLib
- [`FixedPointMathLib`](./contracts/FixedPointMathLib.sol) is an arithmetic library with operations for fixed-point numbers.
- [`FixedPointMathLibTest](./contracts/FixedPointMathLibTest.sol) is an example of test for `SignedWadMath` 

### ERC20
- [`ERC20`](./contracts/ERC20.sol) is an arithmetic library with operations for fixed-point numbers.
- [`ERC20Burn`](./contracts/ERC20Burn.sol) extends `ERC20`  with a burn function
- [`ERC20Test](./contracts/ERC20Test.sol) is an example of test for `ERC20Burn` 
- [`ERC20TestAdvanced](./contracts/ERC20TestAdvanced.sol) is an example of an advanced test for `ERC20Burn` 
   - `ERC20TestAdvanced` uses the [external testing approach](https://secure-contracts.com/program-analysis/echidna/basic/common-testing-approaches.html#external-testing) and uses a proxy contract to simulate a user. This approach is more complex to use, but allows to test for more complex scenario

### Helper
- [`helper](./contracts/helper.sol) comes from the [properties](https://github.com/crytic/properties) repo, and contains functions helper to ease the creation of invariants. 

## How to start

A few pointers to start:

- Read the documentation
- Start small, and create simple invariants first
  -  Start with `SignedWadMath`
- Consider when operation should or it should not revert
- Some properties could require to use certain tolerance
-  `ERC20TestAdvanced` is recommended only for users that have already explored the other contracts
- Do not hesitate to introduce bugs in your code to verify that your invariants can catch them


To start a fuzzing campagn
```bash
medusa fuzz --target contracts/NAME.sol --deployment-order CONTRACT_NAME
```
Replace `NAME.sol` and `CONTRACT_NAME`.

## Expected Results and Evaluation

User should be able to fully test the contracts. It is worth mentioning that the code is unmodified and there are no known issues. If you find some security or correctness issue in the code do NOT post it in this repository nor upstream, since these are public messages. Instead, contact us to confirm the issue and discuss how to proceed.

For Secureum, the resulting properties will be evaluated introducing an artificial bug in the code and running a short fuzzing campaign.

We encourage you to try different approaches and invariants. Invariants based development is a powerful tool for developer and auditors that require practices and experience to master it. 

## Configuration
[medusa.json](./medusa.json) was generated with `medusa init`. The following changes were applied:
- `testAllContracts` was set to true

## Documentation
- [Medusa configuration](https://github.com/crytic/medusa/wiki/Project-Configuration)
- [Fuzzing workshop](https://www.youtube.com/watch?v=QofNQxW_K08&list=PLciHOL_J7Iwqdja9UH4ZzE8dP1IxtsBXI)
- [Fuzzing training](https://secure-contracts.com/program-analysis/echidna/index.html)