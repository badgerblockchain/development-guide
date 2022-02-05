# Introductory Block: Enviornment Setup

By following this introductory block you will be able to setup your workspace for blockchain development.


## What You Need to Start

Before you can follow this tutorial you will need to have a few things installed on your computer.

+ Install an IDE. Any will work if you are comfortable with it, but we are using [Visual Studio Code](https://code.visualstudio.com/download)
+ Download [NodeJS](https://nodejs.org/en/download/) >16.13.1 for your system
  + If you are on Windows you will need to add Node to your env variables PATH. Follow this [stack overflow answer](https://stackoverflow.com/a/27864253)
+ A [GitHub](https://github.com/) account
+ Download [git](https://git-scm.com/downloads) onto your machine
  + Follow the [Git Setup](https://docs.github.com/en/get-started/quickstart/set-up-git#setting-up-git)
  + Setting up [https git authentication](https://docs.github.com/en/get-started/quickstart/set-up-git#next-steps-authenticating-with-github-from-git) will save you time later  


## What is our *stack*?

A developer stack is all of the tools and frameworks used in order to create an app. In our case a decentralized application.

- IDE (integrated development enviornment): VS Code, if you are comfortable use whatever
- Backend Language: Solidity
- Frontend Language: React JavaScript
- Solidity Development Enviornment: Hardhat


## Getting Familiar with the Project

You can find the starting blocks of the app we will be building out [here](https://github.com/badgerblockchain/badger-blocks). If you miss any meetings you can follow along with this [development guide](https://github.com/badgerblockchain/development-guide).


### Cloning the Project

In order to write your own code you will need to have our starter code on your machine. Let's start by navigating to [Badger Blocks](https://github.com/badgerblockchain/badger-blocks) on GitHub.

Start by copying the HTTPS link from the green dropdown

<img src="images/clone-repo.png" alt="drawing" width="375"/>

Jump over to your command line and clone the repository and install dependencies:
```sh
git clone https://github.com/badgerblockchain/badger-blocks.git
cd badger-blocks
TODO: dependencies
```

## Steps to setup env - pretty later

- Install node js 17 https://nodejs.org/en/download/current/
    - make sure u have npm 8.3> and node 17.4>
- Install hardhat
    - issue with ethers path thingy with tests: https://stackoverflow.com/questions/69692842/error-message-error0308010cdigital-envelope-routinesunsupported
    - change to using solidity 0.8.11 change in hardhat.config
- console.log feature for debugging
- show how to test and compile and debug code
- bring resources: https://hardhat.org/getting-started/


## Resources

A list of useful resources we found while creating this learning block:

- Ethereum's [developer resources](https://ethereum.org/en/developers/) are a good place to start
- Follow Hardhat's [tutorial](https://hardhat.org/tutorial/) for a quick overview
- For other Hardhat questions visit their [documentation](https://hardhat.org/getting-started/)
- 