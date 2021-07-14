# darkforest-quickstart

The Dark forest client deploy process is set up for players to easily fork the client and connect to the maininet game, but that design decision currently makes it difficult to run an end to end version of the game locally. This repo fixes that.

This repo uses submodules to pair the [DarkForest Ethereum backend](https://github.com/darkforest-eth/eth) with the [Dark Forest Frontend Client](https://github.com/darkforest-eth/client) so you can launch a local game.

## Install

- Clone with submodules `git clone --recurse-submodules https://github.com/projectsophon/darkforest-quickstart` or if you've already cloned and want to update the module `git submodule update --init --recursive`
- Install [Yarn](https://classic.yarnpkg.com/en/docs/install)
- Run `yarn` at the top level to automatically install all dependencies from subfolders.

## Run a local game

- Open a terminal tab and run `yarn start`, which will start 1) local node, 2) deploy the contracts, and 3) build the local client in dev mode
- When finsihed, the process should pop up your browser to the game client at http://localhost:8081/

You won't have a webserver to drip you a few cents to start playing (which Dark Forest usually does) so instead of creating a new burner wallet, you'll want to import one of the private keys the node funded for you. See the node page where it prints wallets like:

> Account #2: 0x3097403b64fe672467345bf159f4c9c5464bd89e (100 ETH)
>
> Private Key: 0x67195c963ff445314e667112ab22f4a7404bad7f9746564eb409b9bb8c6aed32
