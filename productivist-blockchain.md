# The Productivist Blockchain Architecture


## Overview

Productivist is a blockchain for distributed manufacturing. While the project has its roots in 3D printing, with the [Freelabster](https://www.freelabster.com) organization, Productivist now aims at supporting the manufacturing process in the general acceptation of the term. The Productivist blockchain is designed for providing trust, transparence and trackability to any industrial process involving machine tools, digital product modeling - 3D or otherwise - and customers.

### Organic, decentralized production chain

#### The 3D printing use-case

The [Freelabster](https://www.freelabster.com) organization is the original use case for Productivist, and the first that will make use of the Productivist blockchain. As such, Freelabster encompasses most of the needs for a production blockchain.

There are 3 main types of members, who can naturally overlap:

  * Customers, who want a specific object or serie to be produced.
  * Designers, who create 3D models than can be printed.
  * Producers, aka "Labsters" who will create the object(s) from the model, with a 3D printer.

The main services performed by the Freelabster site are the ones that will be handled by the Productivist blockchain:

  * Producers and designers retribution. Payments are currently centralized by Freelabster. Tokenization on a blockchain will provide the service in a distributed fashion.
  * Model and object certification. Currently Freelabster has a labster certification program. The aim of the Productivist blockchain in this area is to handle partipants reputation / ranking, as well as models and products certification.

#### Designing a blockchain architecture with Hyperledger

The Productivist blockchain will be implemented on a dedicated [Hyperledger](https://www.hyperledger.org/) network. The relevant features of Hyperledger for Productivist are that Hyperledger is open-source, designed to be deployed at will, and does not require proof of work based consensus.

Hyperledger overview:

  * Multiple blockchains channels on the same fabric
  * Applications and smart-contracts
  * Organizations and Certificate Authorities


### The Productivist core blockchain

#### Architecture

As described in the Productivist whitepaper, the blockchain implements a layered architecture. 

  * The public blockchain brings together all users, designers and builders on a common channel
  * Tokenization enables commercial uses, with no exposure to crypto-currencies fluctuations
  * Private solutions for specific production eco-systems are insulated their own blockchain channels

#### Members

These are the main types of Productivist blockchain members. Roles will be cast for those members, and specific organizations implemented for them on the Productivist blockchain Hyperledger network.

  * Customers / end users
  * Independant model designers
  * Independant producers, 3D printers, fab labs
  * Industrials
  * Experts, certification organisms

#### Productivist blockchain applications

Smart-contracts running on the productivist blockchain will enable a variety of applications, providing different services.

The goal here is to cover the services defined by the Freelabster use-case.

##### Core applications

These are the smart-contracts and applications provided by the Productivist organization. Transparent, open-source, they are the backbone of the Productivist service.

  * **productoken**: Tokenized service marketplace
  * **modelcert**: Pre-production 3D model certification
  * **qualitycheck**: Post-production object validation

##### User applications

Customers running their own blockchain channels have the ability to deploy specific applications at will.


## Blockchain architecture

### Organizations and members roles

Each of the individual members listed in the core blockchain overview above has a unique identifier in the blockchain, materialized by credentials and enrollment certificates. Organizations may be delegated certificate authority servers, that will allow them to create affiliated users. Roles will be implemented as organizations from which a member has to be a member in order to perform certain tasks.

#### Members 

Every member has at least the following attibutes:

  * Credentials, including a private/public key pair managed by the network membership services.
  * A ProducToken wallet, with a corresponding account on the **productoken** chaincode.

#### Roles

Members roles will be implemented as organizations. In addition to industrials, certification organisms and other entities that will have their own organization on the blockchain, the following are defined for role membership:

  * **Customer** Requests an object
  * **Designer** Creates 3D models, plans, machine tool code.
  * **Producer** Builds physical objects, as units or series, using 3D printers or other machine tools.
  * **Expert** Certifies models, either by origin or design, and validates finished objects overall quality.

