# darkforest-local

The Dark Forest client deploy process is set up for players to easily fork the client and connect to the mainnet game, but that design decision currently makes it difficult to run a playable version of the game locally. This repository provides a setup for running a local game with just a few steps.

## Builder's Guide

For a comprehensive tutorial on using this repository to make custom local games and deploy them, check out the [Builder's Guide](builders_guide.md).

## How `darkforest-local` works

This repo uses [submodules](.gitmodules) to pair the [Dark Forest Ethereum backend](https://github.com/darkforest-eth/eth) with the [Dark Forest TypeScript frontend](https://github.com/darkforest-eth/client) so you can launch a local game.

It also uses Yarn, a package manager (like `npm`) that allows for multiple [workspaces](https://classic.yarnpkg.com/lang/en/docs/workspaces) to exist within a project.

The workspaces allows each [submodule](.gitmodules) to have their own packages and configuration. 
Yarn places all of the packages for each submodule in the top level `node_modules/` folder.

## Requirements
* Install `node >= 14` (You can consider using [nvm](https://github.com/nvm-sh/nvm))
* Install [Yarn](https://classic.yarnpkg.com/en/docs/install)

### Quickstart for running a local game
1. Fork [darkforest-local](https://github.com/projectsophon/darkforest-local) to your GitHub account
2. `git clone --recurse-submodules https://github.com/<your_name>/darkforest-local.git`
3. If you didn't clone with `--recurse-submodules` or already have a cloned version: `git submodule update --init --recursive --remote --merge`
4. `yarn`
5. `yarn start`

### If you plan to make changes to `darkforest-local`
1. Fork [darkforest-local](https://github.com/projectsophon/darkforest-local) to your GitHub account
2. Fork [darkforest-eth/eth](https://github.com/darkforest-eth/eth) to your GitHub account
3. Fork [darkforest-eth/client](https://github.com/darkforest-eth/client) to your GitHub account
4. Fork [darkforest-eth/circuits](https://github.com/darkforest-eth/circuits) to your GitHub account
5. Fork [darkforest-eth/packages](https://github.com/darkforest-eth/packages) to your GitHub account
4. Clone your darkforest-local repo: `git clone https://github.com/<your_name>/darkforest-local.git`
5. Update the `.gitmodules` file to point to your new forks of `eth`, `client`, `circuits`, and `packages` 
    ex: 
    * `url = https://github.com/darkforest-eth/eth` => `url = https://github.com/cha0sg0d/eth`
    * `url = https://github.com/darkforest-eth/client` => `url = https://github.com/cha0sg0d/client`
    * `url = https://github.com/darkforest-eth/circuits` => `url = https://github.com/cha0sg0d/circuits`
    * `url = https://github.com/darkforest-eth/packages` => `url = https://github.com/cha0sg0d/packages`
6. Fetch the code from the submodules
    * `git submodule update --init --recursive`   
7. Add new branches for developing:
    - The `darkforest-local` monorepo detaches the submodules from their current HEADs. If you want to save your changes (for example, if you're testing an new contract in `eth`), you'll need to make a new branch in these submodules.
    1. `cd eth`
        1. `git checkout -b <new_name>`
    2. `cd client`
        1. `git checkout -b <new_name>`
    3. `cd circuits`
        1. `git checkout -b <new_name>`
    4. `cd packages`
        1. `git checkout -b <new_name>`
7. Install packages and dependencies
    * `yarn`
8. Start a game
    * `yarn start`

            
## Run a local game

- Running `yarn start`, will 1) start a local node, 2) deploy the contracts, and 3) run the local client in dev mode
- When finished, the process should pop up your browser to the game client at http://localhost:8081/

- Here are 3 private keys with 100 ETH each to use in the game:
    1. `0x044C7963E9A89D4F8B64AB23E02E97B2E00DD57FCB60F316AC69B77135003AEF`
    2. `0x523170AAE57904F24FFE1F61B7E4FF9E9A0CE7557987C2FC034EACB1C267B4AE`
    3. `0x67195c963ff445314e667112ab22f4a7404bad7f9746564eb409b9bb8c6aed32`


## Static deployment of Dark Forest (no webserver)

If you want to deploy the contracts (with whatever modifications you want) to mainnet, and client
code (with whatever modifications you want), you can follow these instructions. The reasons you
might want to do this could be one of:

- You want to run a community round of Dark Forest
- You want to run a multiplayer round with some friends
- etc.

Deploying to production is quite similar to deploying a local version of the game, but I'm going to
walk through the steps explicitly here.

### Step 1: Deploy contracts

Unlike in development mode, in production mode you will need to create a `.env` file in both the
`client/` and `eth/` submodules. You can find the set of environment variables you will need to
populate those `.env` files with in their adjacent `.env.example` files.

> **Danger!** The `.env` files ARE in the respective `.gitignore`s of the aforementioned submodules,
> however you should also manually make sure that they don't end up checked into your repository.

To randomly generate a new deployer private key and mnemonic for `eth/.env`, run 
```bash
yarn workspace eth hardhat wallet:new
```
You should see something like this:

![yarn workspace eth hardhat wallet:new](img/new_key.png)


To deploy the contracts, you will need to run the following command:

```bash
yarn workspace eth hardhat:prod deploy
```

You should see something like this:

![yarn workspace eth hardhat:prod deploy](img/hardhat_prod_deploy.png)

To find out more information about the `contracts` submodule, you can look here:
[https://github.com/darkforest-eth/eth](https://github.com/darkforest-eth/eth).

### Step 2: Deploy client website

To deploy the website interface, you may either self-host, or use the same infra that we use -
[Netlify](https://www.netlify.com/). This is a simple option, and free for up to some amount of
gigabytes of bandwidth per month, which has often been enough for us.

To use Netlify:

- Make a new [Netlify account](https://app.netlify.com/signup) using your Github profile.
- [Import](https://app.netlify.com/start) your forked **darkforest-local** repo as a new Netlify site.

    - During Step 3 of the import (Site settings, and deploy!):
        - Build command: `yarn workspace client build`
        - Publish directory: `client/dist`

    Your initial settings should look like this:

    ![netlify_settings](img/netlify_import.png)  

    *Importing from Github will automatically trigger an initial build by Netlify, which will take ~5 min.*

- Install the Netlify CLI
    - `npm install netlify-cli -g`
- Login to your account
    - `netlify login`
- Connect to your app
    - `netlify link`
    
    ![Netlify link](img/link.png)
    
- Choose *Enter a site ID*
    
    ![Site ID](img/site_id.png)
    
- Input the id that you find by clicking on your new site on Netlify. In this example, the id is `jolly-hermann-3947ca`
- Now that your site is linked, you can deploy to Netlify from the CLI.
    - `yarn deploy:client:prod`
    - If successful, you will see something like this.
        
        ![deploy_success](img/netlify_deploy.png)
    - By default, all future changes to the branch you specified in the settings will result in an automatic deploy (in this case `master`). 
    - You can still choose to deploy manually (via `yarn deploy:client:prod`).
    - Additionally, if you want to stop auto-publishing via git updates, see this image:
        ![stop_auto_publishing](img/stop_auto_publishing.png)

### Step 3: Allow player addresses

The default implementation of Dark Forest ships with a [whitelist
contract](https://github.com/darkforest-eth/eth/blob/master/contracts/Whitelist.sol). When we
deployed the contracts in Step 1, amongst them was this whitelist contract. A 'static' deployment of
Dark Forest (no web server) isn't capable of submitting a whitelisting transaction on behalf of the
user (which lets a given burner address into the game and drips it a fraction of an xDAI).

This means that if you want to let players into your game, you must first collect their
addresses.

If you want to generate a burner wallet on the CLI for testing, follow the same steps from [Step 1](#step-1-deploy-contracts):

```bash
yarn workspace eth hardhat:dev wallet:new
```


Once you collect the addresses of the people you want to let into your world, you can register them
individually via the following command

```bash
yarn workspace eth hardhat:prod whitelist:register --address $BURNER_WALLET_ADDRESS
# where $BURNER_WALLET_ADDRESS is the network address of the player you want to allow to play in
# your deployment of the game.
```

If everything worked properly, you should be able to log in:

![log in](img/log_in.png)

Then, once you've found a home planet, you should be able to enter the game!

![enter game](img/enter_game.png)

### Step 4: Play your game

- Now go the URL given by Netlify → something like [https://jolly-hermann-3947ca.netlify.app/](https://jolly-hermann-3947ca.netlify.app/) and test out your game! Login with one of the private keys for the addresses that were whitelisted. Make some moves and test that everything works as expected.

## Update to latest Dark Forest code

If theres been new Dark Forest updates released and we haven't yet updated this repo yet, it is possible you can get away with updating yourself by running `git submodule update --remote --merge` and remember to run `yarn` again.

## For maintainers of the repo updating to latest Dark Forest code

- [Update the submodules](#update-to-latest-dark-forest-code).
- Replace the root `yarn.lock` with the `yarn.lock` from `eth/` or `client/`
- Run `yarn`.
- Finally add all changes, commit, and PR.