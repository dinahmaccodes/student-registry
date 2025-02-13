# Student Registry Smart Contract

This Solidity smart contract manages student registration, attendance, and interests. It allows students to register themselves, and the contract owner can manage attendance and interests. 

## Overview

The Student Registry smart contract allows students to register, manage their attendance, and track their interests. The contract is designed with ownership restrictions and data validation to ensure integrity.

### Features

1.	Student Registration: Users can register as students.
2.	Attendance Management: Students can mark their attendance.
3.	Interest Tracking: Students can add or remove interests (up to five interests).
4.	Owner Controls: The contract owner can transfer ownership.

# Deployment Guide
To deploy the contract on an Ethereum-compatible blockchain, follow these steps:
### Prerequisites
·	Node.js & npm/yarn (for Hardhat/Remix development) <br>
·	Solidity Compiler (via Hardhat or Remix) <br>
·	MetaMask or a compatible Ethereum wallet (it is recommended to use testnet) <br>

### Steps
1.	Set up Hardhat (if using a local environment)
2.	mkdir student-registry && cd student-registry
3.	npm init -y
4.	npm install --save-dev hardhat
5.	npx hardhat
6.	Choose "Create a basic sample project."
7.	Add the contract file
·	Create a new file contracts/StudentRegistry.sol and paste the smart contract code.
1.	Compile the contract
2.	npx hardhat compile
3.	Deploy the contract (Hardhat local network example)

### Create a deployment script 

``` 
scripts/deploy.js: const hre = require("hardhat");
async function main() {
    const StudentRegistry = await hre.ethers.getContractFactory("StudentRegistry");
    const registry = await StudentRegistry.deploy();
    await registry.deployed();
    console.log("StudentRegistry deployed to:", registry.address);
}
main().catch((error) => {
    console.error(error);
    process.exitCode = 1;
});

Run deployment: npx hardhat run scripts/deploy.js --network localhost
–	Deploy on a testnet (Goerli, Sepolia, etc.)
Configure Hardhat for testnet.
Run the deployment script with the testnet flag.

``` 

#### Using Remix
–	Open Remix <br>
Go to Remix Ethereum IDE. <br> 
–	Create a New File <br> 
In the Remix file explorer, create a new Solidity file (StudentRegistry.sol). <br> 
Copy and paste the contract code into the new file. <br> 
–	Compile the Contract <br> 
Navigate to the "Solidity Compiler" tab. <br> 
Select Solidity version 0.8.24. <br> 
Click "Compile StudentRegistry.sol". <br> 
–	Deploy the Contract <br> 
Navigate to the "Deploy & Run Transactions" tab. <br> 
Select the "Injected Provider - MetaMask" environment if deploying on a testnet, or "Remix VM" for local testing. <br> 
Click "Deploy" and confirm the transaction in MetaMask. <br> 





# Working with the Smart Contract
#### Functions Overview
–	registerStudent(_name, _attendance, _interests) <br> 
Registers a student with a name, initial attendance, and interests. <br> 
Registers a student with the given name.<br> 
Default attendance is set to "Absent." <br> 
Example: registerStudent("Alice", 0, ["Coding", "Math", "Pilates","Crocheting"]). <br> 
<br> –	registerNewStudent(_name) <br> 
Registers a new student with the default attendance set to "Absent". <br> 
–	markAttendance(_address, _attendance) <br> 
Updates the attendance status (Present/Absent) of a student. <br> 

–	addInterest(_address, _interest) <br> 
Adds a new interest to a student’s profile (max 5 interests allowed). <br> 

–	removeInterest(_address, _interest) <br> 
Removes a specific interest from the student’s profile. <br> 

–	getStudentName(_address) <br> 
Returns the registered name of a student. <br> 
Retrieves the attendance status of a student. <br> 

–	getStudentAttendance(_address) <br> 
Returns the attendance status of a student. <br> 

–	getStudentInterests(_address) <br> 
Returns the list of interests of a student. <br> 

–	transferOwnership(_newOwner) <br> 
Allows the contract owner to transfer ownership to another address.
 <br> 

#### Events 
StudentCreated(address indexed _studentAddress, string _name) <br> 
It is emitted when a new student is registered. <br> 

<br> AttendanceStatus(address indexed _studentAddress, Attendance _attendance) <br> 
It is emitted when a student's attendance is updated. <br> 

<br> InterestAdded(address indexed _studentAddress, string _interest) <br> 
It is emitted when a student adds a new interest. <br>

 <br> InterestRemoved(address indexed _studentAddress, string _interest) <br> 
Emitted when a student removes an interest. <br> 

#### Security Considerations
–	Ownership Restriction: Only the contract owner can transfer ownership. <br> 
–	Validation Checks: Prevents duplicate interests and ensures students exist before modifying their data.<br> 
–	Gas Optimization: Uses mappings for efficient lookups. <br> 

