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

The **productoken** chaincode is a basic, stateful - as opposed to bitcoin stateless UTXO model - token account management application. 

#### Members and roles

All participants are potentially involved in **productoken** operations. **Customers** will typically transfer tokens to **Designers** and **Producers**. **Experts** may be retributed by both parties.

#### Database structure

The key-value database unit entry here is a user account, and must hold at least the account balance. Minimal json structure example:

```
john_smith_uid: {
  balance: 1000
}
```

#### Chaincode commands

##### Invocations

  * **Deposit:**

```
Command
-------
  uid_a: <'deposit', value>

Result
------
  uid_a: <balance> -> <balance + value>  
```

  * **Withdrawal:**

```
Command
-------
  uid_a: <'withdrawal', value>

Result
------
  uid_a: <balance> -> <balance - value>  
```

  * **Transfer:**

```
Command
-------
  uid_a,uid_b: <'transfer', value>

Result
------
  uid_a: <balance> -> <balance - value>  
  uid_b: <balance> -> <balance + value>  
```

##### Queries

  * **Balance:**

```
Query
-------
  uid_a: <'balance'>

Result
------
  uid_a: <balance> -> 
```

#### Sequence diagram

Diagram for the productoken **Transfer** operation

```
                       User A                     User B
____________________________________________________________
                          |                          |
 --Transfer-request-----> |                          |
                          |                          |
 <-------Accept---------- |                          |
                          |                          |
 --------------Transfer-notification---------------> |
                          |                          |
 <---------------------Acknowledge------------------ |
                          |                          |
 ----Balance-update-----> | -----------------------> |
                          |                          |
                          |                          |
____________________________________________________________
```


### The *modelcert* application

#### Synopsis

The **modelcert** chaincode is the application used to ensure that a model respects a given set of certifications, be it functional, of origin, or other. 

#### Members and roles

It can be up to any user, be it a **Customer**, a **Producer** or a **Designer** to check a model certifications. On the other hand only an **Expert** performs the reviews and certifications.

#### Database structure

The key-value database unit entry here is a model. Although a model may have several certifications as stated above - origin, suitability for a set of given purposes, abiding to a certain set of rules by the **Designer** and so on - we will only use one *certified* attribute. If set, the *certified* attribute states that the model received one or more certifications, which are to be retrieved in the model's transactions history.

```
poly_2018_ac4708f: {
  name: "poly",
  version: "ac4708f",
  uri: "http://example.com/models/poly_2018_ac4708f.stl",
  hash: "79d10afc247a3fd6c6239f68229c260b",
  designer: "dave_the_designer_uid",
  certified: 0
}
```

*Notes*: 

  * The *version* attribute - version number, git commit or whatnot - distinguishes several versions of the same model name.
  * The *uri* attribute refers to a location where the actual model file can be retrieved, whatever the scheme employed. The *hash* attribute is used to verifiy that the model at the referred location hasn't changed.
  * The *certified* attribute is only valid for the current instance of the model. Any other version, even with trivial differences, should also go through the certification process. The semantics of the attribute are deliberately lax: any nonzero / non-null value will be considered as a boolean positive, and may be also interpreted as a bitfield, a comma-separated string or any mean of convenience that may be used in most cases to avoid going through the ledger to check for a given certification.

#### Chaincode commands

##### Invocations

  * **Certify:** operation implemented with *certified* attribute used as a bitfield.

```
Command
-------
  user_x,expert_y,model_uid_z: <'certify', cert_id>

Result
------
  model_uid_z: <name,...,certified> -> <name,...,certified|cert_id>
```

  * **Design:** operation by which a **Customer** summons a **Designer** create a model. *Note*: this operation will probably end-up in a separate application, but *modelcert* for now is the app that deals with models as DB entries.

```
Command
-------
  customer_x,designer_y: <'design', name, specs>

Result
------
  model_uid_z: <name,...,designer_y,0>  
```

##### Queries

  * **FileCheck:** verify a file at a given uri against the model's hash.

```
Query
-------
  model_uid_z: <'fileCheck', uri>

Result
------
  model_uid_z: <True|False> -> 
```

  * **CertCheck:** Queries the ledger for a given certificate

```
Query
-------
  model_uid_z: <'certCheck', cert_id>

Result
------
  model_uid_z: <cert_id,expert_id> -> 
```

  * **CertList:** Queries the ledger all certificates on a given model

```
Query
-------
  model_uid_z: <'certList'>

Result
------
  model_uid_z: <cert_id,expert_id>* -> 
```

#### Sequence diagram

Diagram for successive modelcert **Design** and **Cert** operations, with external calls to *productoken* chaincode. In this example, the **Customer** pays the **Expert** for the design  certification.

```
            Customer X                 Designer Y               Expert Z
______________________________________________________________________
                |                         |                        |
                | -----Design-request---> |                        |
                |                         |                        |
  <-----productoken-Transfer-initiate---- |                        |
                |                         |                        |
  ------productoken-Transfer-commit-----> |                        |
                |                         |                        |
                | <----Design-result----- |                        |
                |                         |                        |
                |                                                  |
                |                                                  |
                | -------------------Cert-request----------------> |
                |                                                  |
 <-----------------productoken-Transfer-initiate------------------ |
                |                                                  |
 ------------------productoken-Transfer-commit-------------------> |
                |                                                  |
                | <------------------Cert-result------------------ |
                |                                                  |
______________________________________________________________________
```


### The *prodcontrol* application

#### Synopsis

The **prodcontrol** chaincode is the application that triggers a physical production process and initiates a physical object's life-cycle in the blockchain.

#### Members and roles

Participants are typically involved in **prodcontrol** operations are **Customers** who will pay for the process with *prod* tokens and **Producers**. 

#### Database structure

The key-value database unit entry here is a manufactured product. Minimal json structure example:

```
my_poly_bot_uid: {
  model: "poly_2018_ac4708f",
  producer: "bob_the_builder_uid",
  build_ts: "Tue, 13 Mar 2018 10:19:55 +0100"
}
```

To support a bit more complex object tracking, during the manufacturing process and later for certification, more attributes can be supported.

  * Current object **status** in: ``['ordered','building','built','validated']`` for production tracking
  * Current **owner** for life-cycle ownership tracking

As a rule of thumb when designing blockchain applications, it is worth noting that the history of the object life-cycle itself should not be managed in the database but directly retrieved from the transaction history. A radical - if not practical - implementation of this approach would lead to store only the **status** and **owner** fields and let the other informations be derived from the transaction history.

A more complete structure supporting the full object life-cycle:

```
my_poly_bot_uid: {
  model: "poly_2018_ac4708f",
  producer: "bob_the_builder_uid",
  build_ts: "Tue, 13 Mar 2018 10:19:55 +0100",
  status: "validated",
  owner: "customer_x"
}
```

#### Chaincode commands

##### Invocations

For the simplest DB structure version:

  * **Make:** 

```
Command
-------
  customer_x,producer_y: <'make', model>

Result
------
  product_uid_z: <model,producer_y,timestamp>  
```


For the more complex DB structure:

  * **Make:** 

```
Command
-------
  customer_x,producer_y: <'make', model>

Result
------
  product_uid_z: <model,producer_y,'building',customer_x>  
```

  * **Update:** 

```
Command
-------
  producer_y,product_uid_z: <'update', 'built'>

Result
------
  product_uid_z: <model,producer_y,'building',customer_x> -> <model,producer_y,'built',timestamp,customer_x>  
```

  * **Transfer:** 

```
Command
-------
  customer_x,customer_y,product_uid_z: <'transfer'>

Result
------
  product_uid_z: <model,producer_y,'built',timestamp,customer_x> -> <model,producer_y,'built',timestamp,customer_y>
```

##### Queries

The **status** and **owner** attributes may be polled in order to follow the object life-cycle. 

  * **Status:**

```
Query
-------
  product_uid_z: <'status'>

Result
------
  product_uid_z: <status> -> 
```

  * **Owner:**

```
Query
-------
  product_uid_z: <'owner'>

Result
------
  product_uid_z: <owner> -> 
```

A lower-level API may also just return the full json structure, that the client module would have to parse.

#### Sequence diagram

Diagram for successive prodcontrol **Make**,  **Update** and **Transfer** operations, with external calls to *productoken* and *qualitycheck* chaincodes.

```
            Customer X                 Producer Y               Customer Y
______________________________________________________________________
                |                         |                        |
                | -----Make-request-----> |                        |
                |                         |                        |
  <-----productoken-Transfer-initiate---- |                        |
                |                         |                        |
                | <----Status-update----- |                        |
                |                         |                        |
  ------productoken-Transfer-commit-----> |                        |
                |                         |                        |
  <----------qualitycheck-initiate------- |                        |
                |                         |                        |
  -----------qualitycheck-validation----> |                        |
                |                         |                        |
                | <----Status-update----- |                        |
                |                                                  |
                |                                                  |
                |                                                  |
                | <------------------Transfer-request------------- |
                |                                                  |
 <-----------------productoken-Transfer-initiate------------------ |
                |                                                  |
 ------------------productoken-Transfer-commit-------------------> |
                |                                                  |
                | -------------------Transfer-accept-------------> |
                |                                                  |
______________________________________________________________________
```

### The *qualitycheck* application

#### Synopsis

#### Members and roles

#### Database structure

#### Chaincode commands

##### Invocations

##### Queries

#### Sequence diagram

