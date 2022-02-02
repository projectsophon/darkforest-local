# Dark Forest Dapp Overview

This page will provide a high level overview of the components and structure of the Dark Forest codebase.

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