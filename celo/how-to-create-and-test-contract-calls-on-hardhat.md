# How to Create and test contract calls on HardHat 

# Introduction
One of the most essential and helpful tools a blockchain developer has as an arsenal is making contract calls. When working on complex and multi-contract projects it is very likely, that you won't be deploying a single smart contract file for the whole production. You might even deploy some contracts earlier than others.

Making contract calls is a flexible way for deployed contracts to interact with other deployed contracts on the blockchain.
This way rather than having a messy long line of code, you have a network of contracts interacting with each other on the blockchian.


Throughout this tutorial you will learn how to:

* Install and Setup Hardhat
* Create a dummy smart contract
* Use hardhat to deploy to the Celo Alfajores Network  
* Create a proficient test script on a hardhat  
* And make contract calls on your deployed contract using hardhat test scripts


# Prerequisites
To get the best out of this tutorial, you should have a basic  and foundational understanding of the following:
* Celo Alfajores testNet
* Faucets 
* Hardhat, Don't worry, you will be installing hardhat alongside this tutorial 
* Node `node` and Node Package Manager `npm`. This tutorial will make use of the node package manager.
You should have the node package manager `npm` pre-installed. Follow the links more information on installing `node` and node package manager `npm`.



## Brief definition of Keywords
Before you get started with this tutorial, here is a quick recap of the keywords you'll be working with during this tutorial

## Celo Alfajores
The celo Alfajores is a test network run by the Celo Team. It is a blockchain simulation that enables
deployments and testing of smart contracts on a fake blockchain. Although it is regarded as a fake blockchain, it primarily simulates deploying and testing contracts on the Celo Blockchain
It functions exactly as effectively as on the Celo mainnets, except you call transactions using faucet funding (fake money).

## Faucets
Faucets are simply fake money funded into your wallet only to interact with a testNet **fake Blockchain**.
To make transactions on the Alfajores TestNet you need faucets in Celo USD **CUSD**.

Following this tutorial, you will need **CUSD** faucets to deploy and make transactions on the Celo Alfajores blockchain.
Getting faucets is always as easy as taking these few baby steps:
1. Head over to the [faucet](https://link-url-here.org) site for the testnet you need. For example a Celo Alfajor faucet will give you fake money to interact with the Celo Alfajore testnet.  

2. Copy your wallet address from metamask or your prefered wallet and paste it into the tab.

3. complete the authentication process, usually `i am not a robot`. Click the und button and wait for about 15 to 90 seconds depanding on the requesting network and you'll notice an increase in your wallet balance. 


## HardHat
Hardhat is an Ethereum Development Environment that runs on `ether-js` and `solc-js`. It is used for compiling, running, and deploying solidity smart contracts


## Calling Contracts 
What are the contract calls referred to in this tutorial?
Making a contract call simply means calling the functions from a deployed contract into another deployed contract on the blockchain.
The calls can be made to retireve data from a query function , or to a payable function for making payment, or even a modifier function for modifying a variable state


Now that you've been reminded of the tools we'll be needing, it's time to get your hands dirty with writing code to understand the purpose of this tutorial.

## Installing Hardhat
To get started with the coding part o this tutorial, you need to install Hardhat.
In the next couple of steps, you will learn how to install Hardhat into your local work environment using yarn on you're preferred Package Manager  

1. Create a workspace in you're preferred code editor.

2. Go to the terminal of your work environment and run the code `npm init -y`. This is to initialize a `package.json` file 

3. Run the command  `npm install --save-dev hardhat @nomiclabs/hardhat-waffle ethereum-waffle chai @nomiclabs/hardhat-ethers ethers` on your terminal to install all the required dependencies you'lll need for this tutorial

4. Next run the command `npx hardhat` to fire up your hardhat development environment. You will be prompted to choose the language you'll be working with.

5. Click enter twice to enable the option `Create a Javascript Project`. and to verify the project location.
You will notice a new folder structure on your code editor file explorer. 

Now that you have successfully installed and Setup up your hardhat development environment. next you will create the exemplary contracts you need to test the contract calls  


## Creating your Smart Contracts
To simulate a contract call, you will need to create two smart contracts. These two contracts will be deployed on the Celo Blockchain.
One of the contracts will have the calling functions `TestContract.sol`, while the other contract `Person.sol` will have the functions you will be calling from the previous contract `TestContract.sol`.

### The Calling Contract **`Person`**:
Navigate to the contract folder in your workspace and rename the existing contract from `Lock.sol` to `Person.sol`.

To initialize the contract and the needed variables, copy and paste the code below:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.9;

contract Person {

// Initializing the variables to Null or None
    string name;
    uint256 age;
    bool has_payed;
    
}
```
Inside the `Person.sol` contract you will create the following simple functions:
* The first function will be an external function `getDetails` that modifies the public variables `name`, and `age`. The function will accept a person's details as inputs and assign them to the public variables.
Add the `getDetails` function below to the `Person.sol` contract created earlier.

```solidity

    function getDetails(string memory _name, uint256 _age) external {
        name = _name;
        age = _age;
    }
        
```

* The second function `sayDetails` will also be an external view function that simply returns the most recent pereson's details stored in the `getDetails` function.
 
Copy and add the code below into the `Person.sol` Contract as the next function.

 ```solidity
   function sayDetails() external view returns (string memory, uint256) {
        return (name, age);
    }

```

* The third function `payFee` will be an external payable function that transfers money into the contract to simulate a person making a payment, the function assigns the bool variable `is_payed` to `true` and the variable paid amount `amount` to `msg.value`.

Copy and add the functiton below into the `Person.sol` contract.

```solidity

    function payFee() external payable {
        value = msg.value;
        has_payed = true;
    }
    
```

* The last contract is an external view function that returns multiple variables `value`, `contract_balance`, `has_payed` based on the payment function `payFee` being called earlier.
 
```solidity

    function getValue() external view returns(uint256, uint256, bool) {
        return (value, address(this).balance, has_payed);
    }
    
```

The four functions created are sample functions to copy a real scenario of calling different types of functions from a contract.


Note: ***Alternatively, When creating contract calls you can also use the keyword `Interface` to initialize the calling contract. To know more about the interface Keyword and other Basic Solidity Data Types click here***. 


### The Caller Contract **`TestContract`**:

The second contract `TestContract.sol` will be the testing contract that will make the contract calls to the `Person.sol` contract.
The contract will also have four different functions to call the four different functions from the first contract `Person.sol`.

When you wnat to call contracts from other contracts, one of the imput has to be the address of the contract you are calling to. and following the format below:


```solidity
    
    function <function_name> <(functoin_inputs)> <visibility> <mutability> returns(output_datatype) {
        do something
        return something
}

```
Note: ****Do not copy the function above, it is just a layout on how to structure a calling function.***

To intialize the `TestContract.sol` contract copy the code below:
```olidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.10;


import './Person.sol';

contract TestContract{

}
```
Note: ***You'll need to import the `Person.sol` contract to make reference to the functions in the `Person.sol` contract you'll be calling***.

* The first function `callGetDetails` accepts the address of the deployed `Person.sol` contract  as `_test` and the other arguments `_name`, `_age` to pass to the `getDetails` function in the `Person.sol` contract.  

Copy and add the function below to the contract:

```solidity

    function callGetDetails(address _test, string memory _name, uint256 _age) external {
        Person(_test).getDetails(_name, _age);
    } 
    
```

* The second function `callSayDetails` will call the `SayDetails` function in the `Person.sol` contract

Copy and add the function below to the contract:

```solidity


```
After adding all the functions created above, your complete `StudentIntro.sol` contract should look exactly like the code below.

For Uniformity, purposes copy and paste the entire code below into the `Person.sol` contract file


## Deploying to Celo Alfajores
Hopefully, you should be familiar with deploying a contract on the Celo blockchain. If not Here is a quick guide on how to deploy to the Celo Blockchain.
In the next few steps, you will deploy both of the previously created contracts to the Celo blockchain, to begin making the contract calls.


## Creating a proficient test script


## Making Contract Calls
