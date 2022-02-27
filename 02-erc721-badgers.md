# Block Two: Writing Our First Contract

## Goal

The goal of this "Block" is to learn about how to implement the ERC721 for our purposes. In addition, we will focus on integrating it with other similar functions that will outline the state of our Badgers on chain (ie, the Badger data stored on chain).


## The ERC721

Simply the [ERC721](https://ethereum.org/en/developers/docs/standards/tokens/erc-721/) is a standard set of functions that outlines how users will interact with our Badgers. The ERC721 is for Non-Fungible Tokens (NFTs). It is important to note that there are other standard contracts that all have different purposes. You can find out more [here](https://ethereum.org/en/developers/docs/standards/tokens/).

The ERC721 outlines numerous functions, however it is not necessary to use all of them. Remember it is a standard to keep function names the same so other people and contracts can easily, and you can tailor the contents and functions to your dapp's purpose.


## The ERC721 in badger-blocks

### Functions

The ERC721 interface for [badger-blocks](https://github.com/badgerblockchain/badger-blocks) only needs a few functions. This includes `_mint()`, `_burn()`, and `transferFrom()`.

`_mint(address _to, uint256 _tokenId)`: This is an internal function denoted by the underscore in front of it. This means that the function can only be called from other functions within the project. This outlines what happens when a Badger NFT is created and writes to on chain memory who owns the NFT and what the ID of the token (Badger NFT) is.

> The tokenId is generated in the createBadger() function and starts at 0 and increases by 1 for each consecutive Badger created. This is out of all Badgers made on this contract, not just Badgers you have created.

`_burn(uint256 _tokenId)`: Afain we have an internal function. This one simply destroys the association of the NFT with any address. This is done by sending the Badger to the null address (ie, 0x0).

`transferFrom(address _from, address _to, uint256 _tokenId)`: This one is fairly straight forward, but it transfers the ownership of a token.

### Mappings

Along with those functions our ERC721 has some mappings in order to keep track of things like:

`balanceOf`: This mapping maps a wallet address to the number of Badger NFTs in that wallet. In our case we have limiting statements that only allow 1 NFT per wallet.

`ownerOf`: This mapping takes a tokenId and maps that to the owner of that tokens wallet address. This is updated when our functions above are called.

### Events

An [event](https://hackernoon.com/how-to-use-events-in-solidity-pe1735t5) is a line of code that logs to the blockchain every time it is called. This log is stored in a special data structure of the block and associated with contracts address. They are useful for outside apps (ie, our frontend) to quickly see the information that the event emits.

Our event looks like this:

```
event Transfer(address indexed _from, address indexed _to, uint256 indexed _tokenId);
```

## Other `Badger.sol` Functions

The other functions we will implement in Badger.sol are as follows:

`createBadger(string memory name)`: This external function will create a `BadgerToken` in on chain memory. This sets all the initial values of the `BadgerToken` struct. Remember, each wallet address can have only one BadgerToken or Badger NFT.

> External functions call only be called from outside of the contract. ie, other contracts or our frontend.

`getBadger(uint256 _badgerId)`: This external function will simply return valuable information about a given Badger (specified by the _badgerId, aka tokenId). The info includes a `BadgerToken`'s name, level, and xp.

There are three other internal or private functions that deal with the xp mechanics of the game. These are `_calculateXp()`, `increaseXp()`, `_decreaseXp()`, and `_levelUp()`. These are fairly self-explanatory and we will go throught the details of these within the function headers themselves. To see that view [Badger.sol](https://github.com/badgerblockchain/badger-blocks/tree/main/contracts/Badger.sol)


## `Badger.sol` Global Variables and Events

### Events

We talked about events in the ERC721 earlier. We also have `Badger.sol` level events that handle some other cases. The notable events in this contract are as follows:

```
event   BadgerMint(uint256 id, string name);
event   BadgerBurn(); 
```

Pretty self-explanatory and they can be found in use in `_mint()` and `_burn()`.

### Global Variables

There are a plethora of global variables in `Badger.sol`. These are generally here, so we don't have to hard code them in a bunch of spots. In addition, we could add logic to change some of the variables in order to change game mechanics later if we notice flaws. Such as, Badgers gain xp too quickly.

I want to point out the `BadgerToken` struct we have been talking about. This is similar to a C struct or a Java object. It is a predefined data type that you can easily abstract a bunch of attributes to the type. In our case `BadgerToken` abstracts all the data that we want a Badger to have. The struct looks like this:

```
    struct BadgerToken {
        uint8   level;
        string  name;
        uint8   wins;
        uint8   losses;
        uint256 readyForReward;
        uint256 readyForCoinFlip;
        uint8   dailyStreak;
        uint8   xp;
        uint256 readyForBuckyReward;
    }
```
> This is a "bad" struct in the sense that it is not packed. Read below to find out more.

A struct can contain any number of different [Solidity data types](https://docs.soliditylang.org/en/v0.8.9/types.html). Structs have an easy gas reducing property. This is known as [packing structs](https://dev.to/javier123454321/solidity-gas-optimizations-pt-3-packing-structs-23f4). The idea is that each time a variables is stored in the Ethereum EVM it is placed in a 256 bit slot, but in a struct you can place variables smaller than 256 bits (uint256 = 256 bits of storage) next to each other, and they will sit in the same slot in the EVM. Thus, saving on the amount of storage needed on chain. In your code try to order the variables to create the most optimally packed struct.

## Resources

### ERC721 examples
[Solmate from Rari Capital](https://github.com/Rari-Capital/solmate/blob/main/src/tokens/ERC721.sol)  
[OpenZepplin's Contract](https://github.com/OpenZeppelin/openzeppelin-contracts/tree/master/contracts/token/ERC721)  
[Ethereum's website](https://ethereum.org/en/developers/docs/standards/tokens/erc-721/)  
[A note about ERC20 vs ERC721](https://soliditydeveloper.com/erc-721)

### Other Resources
[Solidity's Style Guide](https://docs.soliditylang.org/en/v0.8.9/style-guide.html)  
[CryptoKitties Implementation](https://medium.com/loom-network/how-to-code-your-own-cryptokitties-style-game-on-ethereum-7c8ac86a4eb3)  
[Smart Contract Fuzzer](https://github.com/crytic/echidna)
[Startng a Local Testnet and Deploying](https://www.quicknode.com/guides/web3-sdks/how-to-build-your-dapp-using-the-modern-ethereum-tech-stack-hardhat-and-ethersjs)

Previous Lesson: [Solidity Smart Contract Game Layout](https://github.com/badgerblockchain/development-guide/blob/main/01-solidity-game-layout.md)

Next lesson: [TODO]()