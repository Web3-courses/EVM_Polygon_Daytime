

# Week_02
## Day_09 : Dapp

This is the ninth day of the full day version of the EVM → Polygon bootcamp.

Link for actual repo: [Main repo](https://github.com/Web3-courses/Polygon_Blog)

In this session, we will build a simple dapp.

### INSTRUCTIONS

This repo contains a blog site built using Polygon matic and react js. 
The dapp allows users to visualize their name, biography and the feed of all the posts. The user can also publish posts.

## Create folders

Create two folders --> client and smart contract

Smart contracts contains all the details about smart contract and migration files for that

Client contains the frotend part which will interact with smart contracts


#### Smart contracts folder

1. npm init 
2. npm install
3. npm install --save-dev hardhat
4. npm install --save-dev @nomiclabs/hardhat-ethers 'ethers@^5.0.0'
5. npm install --save-dev @nomiclabs/buidler
6. npm install --save-dev @nomiclabs/hardhat-waffle 'ethereum-waffle@^3.0.0'
7. npm install --save-dev chai

or you can use single line of code

npm install --save-dev hardhat @nomiclabs/hardhat-ethers 'ethers@^5.0.0' @nomiclabs/buidler @nomiclabs/hardhat-waffle 'ethereum-waffle@^3.0.0' chai

** some times you may need to add --force for installing the dependencies **

The most important step here is to create a hardhat project. to do that do npx hardhat

#### Important points to be noted for smart contracts folder after creating hardhat project

1. We contain three new folders --> contracts, scripts and test
2. Contracts contain a dummy sample solidity file named Greeter.sol
3. Scripts folder contains sample-script.js which contains the instructions for deploying the contract
4. Tests folder contain an assertion test for testing whether the contract is deployed or not

** You can name sample-script.js as deploy.js if needed to understand that it is the script for deployment


** Use npx hardhat test in the console to test whether the deployments is done without any error
** In sample-script.js see to it that the const <contract_name> is correctly mentioned, for instance if you have created a new file called sample.sol, then it will be const sample inside the script

#### Important points to be noted for smart contracts folder after test

1. You will get the contract name that is deployed
2. You will also get the "Hello world" that is used inside sample-script.js to be shown after deployment
3. Also two new folders are created ---> artifacts and cache

##### Artifacts folder

1. Artifacts folder contains three folders --> build-info, contracts and hardhat
2. build-info contains the json file which is the ABI code log generated after deploying the contract.
3. The contracts sub-folder contains json file that can be used to interact with the smart contract by the client using ether.js

## Creating new contract

1. Go to the contracts folder (root directory/smart_contracts/contracts)
2. Create a new solidity file with .sol extension and name it accordingly

## Deploying the contract
1. Just change the names in the sample-script.js with the contracts you want to deploy
2. npx hardhat run scripts/sample-script.js --network mumbai
3. BEFORE DEPLOYINg see to it that you get some test matic in your wallet

** Sometimes its advisable to remove the arguments inside contractname.deploy() to the contract go through
** After deployment you might get something like this : Contract deployed to: 0x67194ACaCA9e49540662D17AF7C012dF709047E4


## Using Alchemy

1. Create an account if you dont have one
2. Create an App in your dashboard
3. Enter polygon chain and mumai testnet
4. View the key and copy it.
5. Go to hardhat.config.js file in the smart-contracts folder
6. Add the api and network details in the file.
7. Also add the private key in the accounts

## Create utils folder inside client foder

1. The utils should contain two sub-folders --> constants and contracts
2. Constants folder should contain smart contract specific address
3. Contracts folder should contain json files for the smart contracts which can be used to interact with the blockchain


