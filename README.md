`SmartContract-Assessment`
This Solidity smart contract, named WaterRefillingStation, is developed to establish an efficient system for managing a water refilling station, enabling seamless tracking and handling of water sales on the Ethereum blockchain.

`Description`
This contract demonstrates the usage of require(), assert(), and revert() statements for error handling.

`Requirements`
Contract successfully uses require()
Contract successfully uses assert()
Contract successfully uses revert() statements
Components and Functionality
buyWater: This function allows customers to purchase water from the station. It takes the number of gallons to purchase as a parameter, checks if the number of gallons is greater than zero, calculates the total cost, and ensures that the sent Ether is equal to or greater than the total cost. If successful, it updates the total gallons sold and emits a purchase event.

withdrawFunds: This function allows the owner to withdraw the contract's balance. It checks if there are funds available for withdrawal and transfers the entire balance to the owner's address. If the withdrawal fails, it reverts the transaction.

getContractBalance: This function retrieves the current balance of the contract and returns it.

pricePerGallon: A public variable that represents the cost per gallon of water.

totalGallonsSold: A public variable that keeps track of the total number of gallons sold.

owner: An address variable representing the owner or administrator of the Water Refilling Station system.

`Modifiers`
onlyOwner: A modifier that restricts certain functions to be callable only by the contract's administrator.

`Getting Started`
To interact with this contract, you can deploy it on Remix Ethereum IDE or any Ethereum-compatible blockchain.

Open Remix Ethereum IDE.
Create a new file and paste the provided Solidity code.
Compile the code.
Deploy the contract.
Interact with the deployed contract by calling its functions.

```Solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract WaterRefillingStation {
    address public owner;
    uint256 public pricePerGallon;
    uint256 public totalGallonsSold;

    event Purchase(address indexed buyer, uint256 gallons, uint256 amountPaid);

    modifier onlyOwner() {
        require(msg.sender == owner, "Only the owner can perform this action.");
        _;
    }

    constructor(uint256 _pricePerGallon) {
        owner = msg.sender;
        pricePerGallon = _pricePerGallon;
        totalGallonsSold = 0;
    }

    function buyWater(uint256 gallons) public payable {
        require(gallons > 0, "You must buy at least one gallon.");
        uint256 totalCost = gallons * pricePerGallon;
        require(msg.value >= totalCost, "Insufficient funds sent.");

        totalGallonsSold += gallons;

        emit Purchase(msg.sender, gallons, totalCost);
    }

    function withdrawFunds() public onlyOwner {
        uint256 balance = address(this).balance;
        require(balance > 0, "No funds available for withdrawal.");

        (bool success, ) = owner.call{value: balance}("");
        require(success, "Withdrawal failed.");
    }

    function getContractBalance() public view returns (uint256) {
        return address(this).balance;
    }
}
````

This is the whole functionality within the code itself and the generalization of how the code will run.

```Author
Joana A. Abdulmanan
8213866@ntc.edu.ph
