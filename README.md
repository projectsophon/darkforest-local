# darkforest-local

The Dark Forest client deploy process is set up for players to easily fork the client and connect to the maininet game, but that design decision currently makes it difficult to run a playable version of the game locally. This repository provides a setup for running a local game with just a few steps.

This repo uses submodules to pair the [Dark Forest Ethereum backend](https://github.com/darkforest-eth/eth) with the [Dark Forest TypeScript frontend](https://github.com/darkforest-eth/client) so you can launch a local game.

## Install

- Clone with submodules `git clone --recurse-submodules https://github.com/projectsophon/darkforest-local` or if you've already cloned and want to update the module `git submodule update --init --recursive`
- Install [Yarn](https://classic.yarnpkg.com/en/docs/install)
- Run `yarn` at the top level to automatically install all dependencies from subfolders.

## Run a local game

- Open a terminal tab and run `yarn start`, which will 1) start a local node, 2) deploy the contracts, and 3) run the local client in dev mode
- When finsihed, the process should pop up your browser to the game client at http://localhost:8081/

You won't have a webserver to drip you a few cents to start playing (which Dark Forest usually does) so instead of creating a new burner wallet, you'll want to import one of the private keys the node funded for you. See the node page where it prints wallets like:

> Account #2: 0x3097403b64fe672467345bf159f4c9c5464bd89e (100 ETH)
>
> Private Key: 0x67195c963ff445314e667112ab22f4a7404bad7f9746564eb409b9bb8c6aed32

## Update to latest Dark Forest code

If theres been new Dark Forest updates released and we haven't yet updated this repo yet, it is possible you can get away with updating yourself by running `git submodule update --remote --merge` and remember to run `yarn` again.

## For maintainers of the repo updating to latest Dark Forest code

- [Update the submodules](#update-to-latest-dark-forest-code).
- Replace the root `yarn.lock` with the `yarn.lock` from `eth/` or `client/`
- Run `yarn`.
- Finally add all changes, commit, and PR.
