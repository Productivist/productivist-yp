# The Productivist Blockchain Architecture

<!-- toc -->

- [Overview](#overview)
  * [Organic, decentralized production chain](#organic-decentralized-production-chain)
    + [The 3D printing use-case](#the-3d-printing-use-case)
    + [Designing a blockchain architecture with Hyperledger](#designing-a-blockchain-architecture-with-hyperledger)
  * [The Productivist core blockchain](#the-productivist-core-blockchain)
    + [Architecture](#architecture)
    + [Members](#members)
    + [Productivist blockchain applications](#productivist-blockchain-applications)
      - [Core applications](#core-applications)
      - [User applications](#user-applications)
- [Blockchain architecture](#blockchain-architecture)
  * [Organizations and members roles](#organizations-and-members-roles)
    + [Members](#members-1)
    + [Roles](#roles)
  * [Peers, Clients, and other blockchain nodes](#peers-clients-and-other-blockchain-nodes)
    + [Peers](#peers)
    + [Clients](#clients)
    + [Orderers](#orderers)
    + [Certificate Authority servers](#certificate-authority-servers)
- [Blockchain applications](#blockchain-applications)
  * [The *productoken* application](#the-productoken-application)
    + [Synopsis](#synopsis)
    + [Members and roles](#members-and-roles)
    + [Database structure](#database-structure)
    + [Chaincode commands](#chaincode-commands)
      - [Invocations](#invocations)
      - [Queries](#queries)
    + [Sequence diagram](#sequence-diagram)
  * [The *modelcert* application](#the-modelcert-application)
    + [Synopsis](#synopsis-1)
    + [Members and roles](#members-and-roles-1)
    + [Database structure](#database-structure-1)
    + [Chaincode commands](#chaincode-commands-1)
      - [Invocations](#invocations-1)
      - [Queries](#queries-1)
    + [Sequence diagram](#sequence-diagram-1)
  * [The *prodcontrol* application](#the-prodcontrol-application)
    + [Synopsis](#synopsis-2)
    + [Members and roles](#members-and-roles-2)
    + [Database structure](#database-structure-2)
    + [Chaincode commands](#chaincode-commands-2)
      - [Invocations](#invocations-2)
      - [Queries](#queries-2)
    + [Sequence diagram](#sequence-diagram-2)
  * [The *qualitycheck* application](#the-qualitycheck-application)
    + [Synopsis](#synopsis-3)
    + [Members and roles](#members-and-roles-3)
    + [Database structure](#database-structure-3)
    + [Chaincode commands](#chaincode-commands-3)
      - [Invocations](#invocations-3)
      - [Queries](#queries-3)
    + [Sequence diagram](#sequence-diagram-3)

<!-- tocstop -->

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
  * **prodcontrol**: Triggers object production from a model.
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

### Peers, Clients, and other blockchain nodes

#### Peers

Blockchain peer nodes can be either managed by the Productivist organization, private entities, or conglomerates. In order to follow good governance principles, individuals fulfilling any of the Customer / Designer / Producer / Expert roles mentioned above should have access to a peer affiliated to the corresponding organization.

#### Clients

Several kinds of client software need to be developed in order to interact with the chaincode.

  * **Wallets**: The client-side for the **productoken** chaincode. Holds the membership information and credentials for all participants.
  * **Modelers**: Where a **Designer** can show a model to a **Customer**, and an **Expert** can validate it. Client-side software for the **modelcert** chaincode. This module is intended to display and sign a model design, not to create the design itself.
  * **Controllers**: Used by a **Producer** to build a validated design. The medium-term target for the **Controller** code is to run on the *Productivist device*, along with the **Modeler** code. Client-side software for the **prodcontrol** chaincode. 
  * **Validators**: Used by an **Expert** to run a testing campaign on a finished product. Client-side software for the **qualitycheck** chaincode. 

A Note about the *Productivist device*: The device (Productivist WP ch. 3.2) is primarily intended to control the manufacturing process, hence run a **Controller** client software. However, while it may end-up holding all 4 kinds of client software, it is currently not intended to hold a blockchain peer.

#### Orderers

The Hyperledger blockchain Orderer network is managed by the Productivist organization. While adding specific channels for 3rd party organizations is on the Productivist roadmap, providing 3rd parties with their own orderers is not. This policy may evolve if a relevant use case arises that would justify delegating part of the orderer network to 3rd parties.

#### Certificate Authority servers

The CA servers and Membership services manager systems are run by the Productivist organization, as far as the **Roles** management is concerned. Individual members are granted membership to any and all of the Customer / Designer / Producer / Expert roles they can take.

As for private channels managed by 3rd parties, the relevant actors will be granted their own CAs on demand.


## Blockchain applications

We are going to define here the specifications of the 4 **Productivist core blockchain applications**:

  * **productoken**: Tokenized service marketplace
  * **modelcert**: Pre-production 3D model certification
  * **prodcontrol**: Triggers object production from a model.
  * **qualitycheck**: Post-production object validation

It is important to state that these applications, whilst functionally autonomous, are nonetheless interdependent. All production interactions in a commercial context are going to involve token transfer, hence an invocation of the **productoken** chaincode from one of the others.


### The *productoken* application

#### Synopsis

#### Members and roles

#### Database structure

#### Chaincode commands

##### Invocations

##### Queries

#### Sequence diagram


### The *modelcert* application

#### Synopsis

#### Members and roles

#### Database structure

#### Chaincode commands

##### Invocations

##### Queries

#### Sequence diagram


### The *prodcontrol* application

#### Synopsis

#### Members and roles

#### Database structure

#### Chaincode commands

##### Invocations

##### Queries

#### Sequence diagram


### The *qualitycheck* application

#### Synopsis

#### Members and roles

#### Database structure

#### Chaincode commands

##### Invocations

##### Queries

#### Sequence diagram

