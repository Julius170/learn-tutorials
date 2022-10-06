# How to Create and test contract calls on HardHat 

# Introduction

Over the course of this tutorial you will learn how to:

* Install Hardhat
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
Faucets are simply fake money funded into your wallet only for the purpose of interacting with a testNet.
To make transaction on the Alfajores TestNet you need fuacets in Celo USD ***CUSD***.


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
One of the contract will have the functions you want to call `Introcudtion.sol`, while the other will be calling the functions from the first conrtact `Person.sol`.

The First contract `Introduction.sol` will have a simple function that accepts a student's information and returns an introduction of the person in a string format.
 Navigate to the contract folder in your work space and rename the existing contract to `Introduction.sol`.

Copy, and paste the code below into the `introduction.sol` file.

 ```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.9;

// Import this file to use console.log

contract Introduction {
        
        string name;
        string university;
        string course;
        uint256 age;



    function Introduce(
        string memory _name, 
        uint256 _age, 
        string memory _uni, 
        string memory _course
        ) public returns(
            string memory, 
            string memory, 
            uint256, 
            string memory, 
            string memory) {
                
        name = _name;
        university = _uni; 
        course = _course; 
        age = _age;


        return("Hi My Name is '%s' I am '%i'  years old and I am currently studying '%s' in the university of '%s' ", name, age, course, university);
    }

}


```

For the second contract, it will have a simple function that tkes in a string input `_gender` s returns a string format.
This Gender.sol contract will be making a contract call to the `introduction.sol` contract    
This contract will also have call the function `introducing` from the `introduction.sol` contract.
```solidity


```

## Deploying on Celo Alfajores


## Creating a proficient test script


## Making Contract Calls