# How to Create and test contract calls on HardHat 

# Introduction
One of the most essential and helpful tool a blockchain developer has as an arsenal is making contracts calls. When working on complex and multi-contract project it is very likely, that you wont be deploying a single smart contrcat file for the whole production. You might even deploy some  contracts earlier that others.
Making contract calls is a very flexible way to enable a contract to interact with other deployed contracts on the blockchain.
This way rather that having a messy long line of code, 

Over the course of this tutorial you will learn how to:

* Install and Setup Hardhat
* Create a dummy smart contract
* Use hardhat to deploy to the Celo Alfajores Network  
* Create a proicient test script on hardhat  
* And make contract calls on your deployed contract using hardhat test scripts


# Prerequisites
To get the best of this tutorial, you should have a basic  and foundational understanding of the following:
* Celo Alfajores testNet
* Faucets 
* Hardhat, Don't worry, you will be installing hardhat along side this tutorial 
* Node `node` and Package Manager `yarn` or `npm`. You should have `node` and you're prefered package manager pre-installed.
This tutorial will make use of the `yarn` package manager, but you can follow along you're prefered PM


## Brief defination on Keywords
Before you getting started with this tutoral, here is a quick recap on the keywords you'll be working with along this tutorial

## Celo Alfajores
The celo Alfajores is a test network run by the Celo Team. It a blockchain simulation that enables
deployments and testing of smart contracts on a fake blockchain. Alghough it is regarded a fake blockchain, primarily to simulate deploying and testing contracts on the Celo Blockchain
It functions exaclty as effective as on the Celo mainnets, except you call transactions using faucet funcdings (fake money).

## Faucets
Faucets are simply fake money funded into your wallet only for the purpose of interacting with a testNet "fake Blockchain".
To make transaction on the Alfajores TestNet you need fuacets in Celo USD **CUSD**.
Following this tutorial you will need **CUSD** faucets to deploy and make transaction on the celo Alfajores blockchian   


## HardHat
Hardhat is an Ethereum development environment that runs on `ether-js` and `solc-js`. It is used when to compiling, running and deploying solidity smart contracts

## Contract calls
What are the contract calls reffered to in this tutorial?
Making a contract call simply means calling the functions from a deployed contract into another deployed contract on the blockchain.
The call can either be a function on query to from one deployed contract to another, to call a function or make a query some information from the second contract

Now that you've been reminded on the tools we'll be needing, its time to get your hands dirty with writing code to understanding the purpose of this tutorial.

## Installing Hardhat
In order to get started with the coding part o this tutorial, you need to install Hardhat.
In the next couple of steps you will learn how to install Hardhat into you local work environment using yarn on you're prefered Package Manager  

1.- Create a work space in you're prefered code editor.
2.- Go to the your terminal of your work environment and run the code `npm init -y`. This is to initialize a `package.json` file 
3.- Next run the command `npx hardhat` to fire up your hardhat development evnironment.
You will be promt to choose the language you'll be working with.
4.- Click enter twice to enable the option `Create a Javascript Project`. and to verify the project location.
You will notice a new folder structure on your code editor file explorer. 

Now that you have sucessfully installed ane Setup your hardhat development environment. next you will create the examplary contracts you need to test the contract calls  


## Creating your Smart Contracts
In order to simulate a contract call you will need to create two smart contracts. These two contracts will be deployed on the Celo Blockchain.
One of the contract will have the calling functions `TestContract.sol`, while the other contract `StudentIntro` will have the functions you will be calling from the previous contract `TestContract.sol`.

### The Calling Contract ***StudentIntro***:
Navigate to the contract folder in your work space and rename the existing contract to `StudentIntro.sol`, like in the image below.
To initialize the contract and the needed variables, copy and paste the code below:
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.9;

contract StudentIntro {
// Initializing the variables to Null or None
        string name;
        string university;
        string course;
        uint256 age;
        bool has_payed;

}
```
Inside the first contract `SudentIntro.sol` you will create will the following simple functions:
* The first fucntion will be an external function `StudentInfo` that modifies the public variables `name`, `age`, `university`, and `course`. The Function will accept student's details as inputs and asign them to the oublic variables.
Add the `studentDetail` function below, to the `StudentIntro.sol` contract created earlier.

```solidity

function studentDetails(
        string memory _name, 
        uint256 _age, 
        string memory _uni, 
        string memory _course
        ) external {
        string name = _name;
        age = _age
        university = _uni ;
        course = _course;
        }
        
```

* The next function `Introduction` will also be an external function that simply returns a string format of the student's information stored in the `studentDetails` function. 
Add the code below into the `StudentIntro.sol`file as the next function.

 ```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.9;

    function Introduce() external view returns(
            string memory,
            string memory, 
            uint256,
            string memory, 
            string memory) {
        return("Hi My Name is '%s' I am '%i'  years old and I am currently studying '%s' in the university of '%s' ", name, age, course, university);
    }
}
```

* The last function `payFee` will be an external payable function for that transfers money into the contract to simulate a student making payment, the function asigns the bool variable `is_payed` to `true` and the vaireable payed amount `amount` to `msg.value`, and finally returns a string format that shows the information of the payment made.

Copy and add the code below to the `StudentIntro.sol` contract.

```solidity
function payFee(uint _amount) external payable returns(string uint256, bool) {
    msg.sender(amount)
    amount = msg.value
    is_payed = True
    return ("'%b' : '%i' was payed by '%s'", is_payed, name, value)
}
```
The three function created are sample function to copy a real scenerio of calling different types of functions from a contract  
Note: ***Alternatively, When creating contract calls you can also use the keyword `Interface` to initialize the calling contract. To know more about the interface Keyword and other Basic Solidity Data Types click here***. 


### The Caller Contract ***TestContract.sol***:

The second contract being the caller function `TestContract.sol` will be the testing contract that will make the contract calls to the  `StudentIntro.sol` contract.
The contract will also have three different functions to call the three different functions from the first contract `StudentIntro.sol`.

Note: ***When cdereating a contract calling function the first inpu t in the function will be the deployed contract address of the calling contract. followed by the name of the function in the contractg you wanr to call***.  
* The first function will be calling call the function `Studentdetails` from the `StudentIntro` contract.  

```solidity
function callStudentIntro(address contractAddress) {
    return (name, bool, value)
}
```

After adding aall the functions created above, your complete `StudentIntro.sol` contract should look exactly like the code below.

For Uniformity purposes copy and paste the entire code below into the `StudentIntro.sol` contract file


## Deploying to Celo Alfajores
Hopeully you should be familiar with deploying a contract on the Celo blockchian. If not Here is a quick quide on how to deploy to the Celo Blockchain.
In the next few steps you will deploy both of the previously created contracts to the celo blockchian, to begin making the contract calls.


## Creating a proficient test script


## Making Contract Calls
