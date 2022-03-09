# Block Three: More Solidity and Game Logic


## Goal

In this learning block, our goal is to learn some more Solidity specific features and look at how you can use that to add logic to the game.


## Inheriting Other Contracts

Since we have our smart contracts stored in separate files we will need to import them into our file in order to inherit. When I say "inherit" that means functions and variables can be read from the inherited contract.

Following is the syntax to inherit Badger.sol in BadgerWorld.sol:
```java
import "./Badger.sol";  

contract BadgerWorld is Badger {
    // contract contents...
}
```

Notice how we need to import the file that resolves to the contract since they are in different files.

Another important thing to note is that `BadgerWorld.sol` will only be able to use and access variables with certain visibilities.


## Function/Variable Visibility

There are four kinds of visibilities in Solidity. The following:

+ `public`: any contract, account, or function can access/call this.
+ `private`: can only be accessed from within the contract or function that defines it.
+ `internal`: can only be accessed from within this contract or another contract that inherits the contract it is defined in.
+ `external`: only other contracts and accounts can access this type of function/variable.

If you could imagine, this means that `BadgerWorld.sol` can only access `public` and `internal` functions and variables from `Badger.sol`.


## Other Function Modifiers

There are a few other function declarations that you will need to remember. They will be important for saving gas when used correctly. See the following:

+ `View`: This type of function declares that no state will be changed. In our case, none of our `public` mappings would be updated. You can still read on-chain data in this function.
+ `Pure`: This function takes `view` a step further. No state will be changed or read.
+ `payable`: This function/variable declaration means that the function/variable can accept ether (or another cryptocurrency given you deploy the contracts to another blockchain). If no ether is sent the function call/transaction will fail.

You cannot stack any of these modifiers.


## Custom Function Modifiers

You can however stack custom function modifiers on functions with any of the previously stated modifiers. A custom modifier generally uses a variable from the function parameters and it is passed into the modifier and runs. If the condition outlined is not met the function will not run.

A common custom modifier allows only the owner of an NFT to call a specific function. You wouldn't want another wallet besides yours attacking with your NFT (badger).

The modifier is defined similar to a function, but different. See the following snippet:

```java
modifier onlyOwnerOf(uint256 _badgerId) {
	require(msg.sender == ownerOfId[_badgerId]);
    _;
}
```

The require statement is like any require statement in Solidity. This is saying that the function caller must also own the _badgerId that they are inputting into the modified function.

The underscore is unlike any other languages. In Solidity modifiers it is a signal to the EVM that the modifier has completed and passed. The EVM will then continue executing the function that called the modifier.

The following is how you actually use a modifier:

```java
function attackBadger(
        uint256 _attackId, 
        uint256 _defenseId
    ) external onlyOwnerOf(_attackId) {
    // logic...
}
```

You can see how the modifier is called and only the owner of the _attackId BadgerToken can call this function. The `_;` would not be reached otherwise.


## Storage vs Memory vs Calldata

These three terms are variable modifiers. They are used to declare where in the EVM memory a variable is stored. Don't forget that Solidity is really a lower-level language, and we want to do everything we can to optimize allocation and logic in order to reduce our gas (gwei) prices.

> You can think about gas as an economic incentive to produce code that is the most efficient and memory efficient as possible.

Let's dive deeper into the different modifiers we are focused on here.

+ `storage`: This means the variable it is applied to is a state variable (ie, it is stored on the blockchain).
+ `memory`: This specifies that the variable is stored in memory and is available only while the function is being called.
+ `calldata`: This one is more unique. It specifies a special storage location for function parameters. And it can only be used in `external` functions.


## What about the logic?

The goal of this development guide is to focus on Solidity development. The logic is topic for any programming language. There is nothing special about Solidity in that sense. What is special is what we have discussed so far. Also, you need to remember that you are writing a "contract" and need to adopt a new way of thinking to truly understand the problems being tackled.


## Resources

[Solidity Inheritance](https://www.geeksforgeeks.org/solidity-inheritance/#:~:text=Solidity%20supports%20inheritance%20between%20smart,is%20called%20a%20derived%20contract.)

[Solidity by example](https://solidity-by-example.org/). This is a great website for syntax and how to do stuff.

What is the [EVM](https://ethereum.org/en/developers/docs/evm/)

More on [gas?](https://ethereum.org/en/developers/docs/gas/)

Blockchain/web3 use cases [here](https://consensys.net/blockchain-use-cases/)


Previous Lesson: [ERC721 Contract and Badger Attributes](https://github.com/badgerblockchain/development-guide/blob/main/02-erc721-badgers.md)

Next lesson: [TODO]()