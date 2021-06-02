# E-Cert-Dapp
 ## Introduction

 ### Checks:
 - Only <b>educator</b> can register certificates and issue certificates.
 - The certificate which is to be issued, must be registered first.
 - No single user can register twice.
 - No hash of a certificate can exist more than one

 ### Actors:
There are 3 types of actors the system provides support to:

 - <b>Educator</b>: This is the certifying authority, which registers new certificates, then issues the desired student that certificate.
 - <b>Student</b>: This is the recipient of the certificate. It first registers itself in the system. He request for a certificate after a course is finished and the stored on-chain
 - <b>Verifier</b>: This can be any anonymous user, who wants to verify the student's certificate.

 ### Events:
Events are the logs of all the transactions done in the blockchain. So for every function of the smart contract, we log its details in events. Our system tracks these events:

 - <b>LogNewHashStored</b>: Ths event is triggered when a hashed is stored on-chain. It logs details of every hash added to an address registered.

### Process Flow:
 - <b>Issuing</b>: This is the process of receiving and generating certificate hash on the ui. Certificate will be received from the frontend, a unique hash (ie that represents the fingerprint of the certificate) will be generated by the hash-generator function
 - After hash generation, a call to a function on the smart contract to ensure this hash is stored on the
blockchain will be made
 - When this occurs, the UI also sends an email to the student with a hash of the certificate.
 - <b>Sharing</b>: this is the process by which the student of a certificate shares that certificate with a third-party.Simple way to share is that once given a hash to the student, the student can send his or her certificate to
their verifier via mail

 - <b>Verification</b>: this is the process by which a third-party verifies the authenticity of the certificate.
 - Once the verifier receives the student certificate, they upload it to the UI for verification. The frontend calls on a function in the smart contract in order to verify that the hash was authenticated by the university.
 - The true/false boolean result is then displayed on the frontend,
in the verifying window


![Alt text](./diagrams/DAOM_E-Cert.jpg?raw=true "E-Cert Daom")

### Milestone 1

- 1. Get certificate data and sub-functions
- 2. Verify certificate data and sub-functions.

### Milestone 2:

 - 1. Manage key and sub-functions
 - 2. Integration with e-learning platform

### Milestone 3:
 - 1. Manage wallet and sub-functions
 - 2. Deployment to permanent web server I will provide.


## Technology stack:

 - <b>Truffle</b> - ( development framework for dapps based on the Ethereum blockchain: https://truffleframework.com/),
 - <b>Ganache</b> - ( A personal blockchain for Ethereum development that can be used to deploy contracts, develop applications, and run tests: https://truffleframework.com/ganache),
 - <b>Solidity</b> - (contract-oriented programming language for writing smart contracts: https://solidity.readthedocs.io/en/v0.4.24/),
 - <b>Web3.js</b> - (Ethereum JavaScript API: https://github.com/ethereum/web3.js/)
- <b>Truffle Contract</b> -(Better Ethereum contract abstraction, for Node and the browser):https://www.npmjs.com/package/@truffle/contract
 - <b>MetaMask</b> - (A browser plugin which allows users to make transactions to Ethereum or other networks through browsers, eliminating the need for dedicated user interfaces for Ethereum or other networks: https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn?hl=en)
 - <b>OpenZeppelin Contracts</b> - OpenZeppelin Contracts is a library for secure smart contract development: https://github.com/OpenZeppelin/openzeppelin-contracts
 - <b>NodeJS</b> - (An open source and cross-platform runtime environment for executing JavaScript code outside of a browser: https://nodejs.org/en/),
 - <b>Angular</b> - (TypeScript-based open-source web application framework led by the Angular Team at Google and by a community of individuals and corporations: https://angular.io/).

 ## Set Up
 ### Install truffle
  - Run the command `npm install -g truffle`
  - Git clone the E-cert-Dapp repo
  - Cd into the directory and run ` yarn install`
  - Run ` yarn run compile` to compile the smart contract
  - Run `yarn run migrate` to migrate the contract. `truffle deploy` is an alias for `truffle migrate`. They both do the same thing.
  - Run `yarn run console` to interact with the smart contract on the ganache ethereum blockchain

  ### Install Ganache
 - Go to https://truffleframework.com/ganache and download a version dedicated to your operating system.
 - Install by a double click, then run.
 - Ganache runs with default values which should be the same or similar to these on-screen. The crucial part is a section defining RPC Server.
 - Leave it running.

 ### Install Nodejs
 - To download Nodejs, navigate to  navigate to https://nodejs.org/en/download/ and click the version that suits your machine
 - After downloading it, click the installer to get it installed on your machine
 - Verify installation by running the command on your CLI ` node -v`
 - You can use npm or yarn for package management

### Testing Results
- Open a terminal and run:
 `truffle test or yarn run test`


![Alt text](./diagrams/test-results.png?raw=true "Test results")

### Test Coverage Results
- Open a terminal and run:
 `truffle run coverage or yarn run coverage`

![Alt text](./diagrams/test-coverage.png?raw=true "Test coverage results")


### Contract deployment gas cost on local network - Ganache
- Open a terminal and run:
 `truffle run migrate or yarn run migrate`

![Alt text](./diagrams/cost-local.png?raw=true "gas cost")


### Contract deployment gas cost on ropsten network - testnet on infuria
- Open a terminal and run:
 `truffle run ropsten or yarn run ropsten`

![Alt text](./diagrams/cost-ropsten.png?raw=true "gas cost")

### Contract deployment gas cost fee on ropsten etherscan explorer
- Open a terminal and run:
 `truffle run ropsten or yarn run ropsten`

![Alt text](./diagrams/etherscan.png?raw=true "gas cost")
- link: https://ropsten.etherscan.io/address/0x0268B3D69FbD4b83F2a51E579ed0953f7a8775E2


### Contract Graph
- Use Solidity Visual Developer to generate the graph for the contract

![Alt text](./diagrams/contractGraph.png?raw=true "Test coverage results")



### Contract UML Diagram
- Use Solidity Visual Developer to generate the UML with PlantUML embedded

![Alt text](./diagrams/contract-uml.png?raw=true "Test coverage results")

### CertificateRegistry:
- This is the main contract. The contract handles the generation and verification of certificates.

- storeHash() — generates a certificate by calculating a hash of the student name and details.
Can be called only by the owner.
Emits a certificate generation event with the timestamp.
The issuer puts the certificate on the blockchain by storing it in the global variable records by passing records[certificate] = msg.sender.
- owningAuthority() — returns the address of issuer/authority.
- verifyCertificateData() — calculates a hash of the student name and details, and checks if the contract is on the blockchain.
Can be called by anyone.

#### Interact with the contract on your local development network
- run 'yarn console' in your Truffle console, create an instance of the deployed contract
- Declare the contract owner:
```let instance = await DocStamp.deployed()``
- Declare the contract owner:
```let owner = await instance.owningAuthority()```

- Issue the certificate:
let result = await instance.storeHash("0x94f3e4c13989c51472ce78354b5205c5411f82e83c745b6f675e0c9aeb8ab4d1", {from: owner})

- Run result.logs to view the full certificate details.

- Run the certificate verification:
```let verify = await instance.verifyCertificateData("0x94f3e4c13989c51472ce78354b5205c5411f82e83c745b6f675e0c9aeb8ab4d1", {from: owner})