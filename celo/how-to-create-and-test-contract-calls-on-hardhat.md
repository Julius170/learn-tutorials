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




## Creating your Smart Contracts


## Deploying on celo Alfajores


## Creating a proficient test script


## Making Contract Calls