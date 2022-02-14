# Dark Forest Dapp Overview

This page will provide a high level overview of the components and structure of the Dark Forest codebase. 

*This page is not official in any way and is subject to change as the game evolves.*

# Intro
- Dark Forest has a lot of moving parts, but at its core, it is a blockchain-based application, commonly referred as a [dapp](https://ethereum.org/en/developers/docs/dapps/).
    
    > A dapp has its backend code running on a decentralized peer-to-peer network (blockchain). Contrast this with an app where the backend code is running on centralized servers. A dapp can have frontend code and user interfaces written in any language (just like an app) to make calls to its backend
    > 
- Dark Forest has a backend that contains the **[code](https://github.com/darkforest-eth/eth/)** that enforces the game constraints and rules. This code is divided into files called **[smart contracts](https://github.com/darkforest-eth/eth/tree/master/contracts),** and it runs on a blockchain.
- Players interact with these contracts via a frontend called the **[client](https://github.com/darkforest-eth/client/)**. This **client** shows a visual representation of the state of the Dark Forest universe and serves as the connection between players and the smart contracts on the blockchain.
- To create a round of Dark Forest, you need to do 3 things:
    1. (optional) Customize the **smart contracts** and **client** to your liking.
    2. Deploy the **smart contracts** to a blockchain.
    3. Deploy the **client** to a frontend hosting service like Netlify.

- Let's dive deeper into each component of the code base.

# Client overview

## Backend

### GameManager

### GameUIManager

## Frontend

# Eth overview

## What is Hardhat?
- [https://hardhat.org/getting-started/](https://hardhat.org/getting-started/)
- Hardhat is a development environment to compile, deploy, test, and debug your smart contracts. 
- Hardhat simulates a local blockchain and deploys your contracts to this chain for development purposes.
- There are many cool features in Hardhat, including the ability to manually mine blocks, speed up blockchain time, and easily deploy contracts to public chains.
- Hardhat also lets you define custom tasks that relate to deploying and interacting with smart contracts. 
    > For example, the `deploy:contracts` task deploys the Dark Forest contracts and the `game:createPlanets` task adds any custom planets to the universe.
- Additionally, Hardhat has a variety of additional plugins that add features such as [unit tests](https://hardhat.org/tutorial/testing-contracts.html#_5-testing-contracts) and [types](https://www.npmjs.com/package/@typechain/hardhat) for smart contracts.
- When running tasks for the local network, use `hardhat:dev`.
- When running tasks for xDai, use `hardhat:prod`.

## contracts

## test

## tasks

# Circuits overview

