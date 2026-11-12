# SwissSwap Periphery

SwissSwap Periphery is the set of router and helper smart contracts for SwissSwap, a decentralized token exchange modelled on Uniswap V2. The router is the contract that users and apps talk to when they want to swap tokens or add and remove liquidity. It works together with a separate SwissSwap factory and pair contracts, which are not part of this repository.

## What it does

- `UniswapV2Router02`: swap tokens, add and remove liquidity, including ETH pairs and fee-on-transfer tokens.
- `UniswapV2Router01` and `UniswapV2Migrator`: the earlier router and a helper for moving liquidity from Uniswap V1 style exchanges.
- `WETH`: a wrapped Ether contract, deployed on test networks and local chains.
- Libraries for pair address lookup, safe math and price oracle maths.
- Examples in `contracts/examples`: flash swaps, a simple price oracle, a sliding window oracle and swap to price.
- Test helpers in `contracts/test`, such as a deflating ERC20 token and a WETH9 contract.

## Tech stack

- Solidity 0.6.6
- Truffle (compile, migrate, test)
- `@uniswap/v2-core` and `@uniswap/lib` from npm

## Run it

You need Node.js and Truffle (`npm install -g truffle`).

```bash
npm install
truffle compile
```

To deploy to a local chain, start one on port 8545 (for example Ganache) and run:

```bash
truffle migrate --network development
```

The migration deploys a WETH contract (on mainnet it uses the existing canonical WETH address) and then the `UniswapV2Router02` router. The factory address is hardcoded in `migrations/2_deploy_contracts.js`. Replace it with the address of your own factory if you deploy elsewhere. The router also computes pair addresses with a hardcoded init code hash in `contracts/libraries/UniswapV2Library.sol`, which must match the pair bytecode of the factory you use.

The `test` folder is empty and `npm test` is not set up, so there are no automated tests yet. Pre-compiled contract artifacts are committed in `build/contracts`.

## Status

Prototype. The contracts compile as a Truffle project, but there are no tests, and the router depends on a factory deployment that is configured by hand. It has not been audited, so do not use it with real funds without a review.

## Credits

This code is based on Uniswap V2 Periphery by Uniswap (GPL-3.0 licensed). `WETH.sol` is the Dapphub WETH9 contract. The SwissSwap adaptation, configuration and deployment scripts are by Max Awad. Please check the upstream licenses before reusing the code.
