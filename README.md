# ✨ So you want to sponsor a contest

This `README.md` contains a set of checklists for our contest collaboration.

Your contest will use two repos: 

-   **a _contest_ repo** (this one), which is used for scoping your contest and for providing information to contestants (wardens)
-   **a _findings_ repo**, where issues are submitted. 

Ultimately, when we launch the contest, this contest repo will be made public and will contain the smart contracts to be reviewed and all the information needed for contest participants. The findings repo will be made public after the contest is over and your team has mitigated the identified issues.

Some of the checklists in this doc are for **C4 (🐺)** and some of them are for **you as the contest sponsor (⭐️)**.

* * *

# Contest setup

## ⭐️ Sponsor: Provide contest details

Under "SPONSORS ADD INFO HERE" heading below, include the following:

-   [ ] Name of each contract and:
    -   [ ] source lines of code (excluding blank lines and comments) in each
    -   [ ] external contracts called in each
    -   [ ] libraries used in each
-   [ ] Describe any novel or unique curve logic or mathematical models implemented in the contracts
-   [ ] Does the token conform to the ERC-20 standard? In what specific ways does it differ?
-   [ ] Describe anything else that adds any special logic that makes your approach unique
-   [ ] Identify any areas of specific concern in reviewing the code
-   [ ] Add all of the code to this repo that you want reviewed
-   [ ] Create a PR to this repo with the above changes.

* * *

# ⭐️ Sponsor: Provide marketing details

-   [ ] Your logo (URL or add file to this repo - SVG or other vector format preferred)
-   [ ] Your primary Twitter handle
-   [ ] Any other Twitter handles we can/should tag in (e.g. organizers' personal accounts, etc.)
-   [ ] Your Discord URI
-   [ ] Your website
-   [ ] Optional: Do you have any quirks, recurring themes, iconic tweets, community "secret handshake" stuff we could work in? How do your people recognize each other, for example? 
-   [ ] Optional: your logo in Discord emoji format

* * *

# Contest prep

## ⭐️ Sponsor: Contest prep

-   [ ] Make sure your code is thoroughly commented using the [NatSpec format](https://docs.soliditylang.org/en/v0.5.10/natspec-format.html#natspec-format).
-   [ ] Modify the bottom of this `README.md` file to describe how your code is supposed to work with links to any relevent documentation and any other criteria/details that the C4 Wardens should keep in mind when reviewing. ([Here's a well-constructed example.](https://github.com/code-423n4/2021-06-gro/blob/main/README.md))
-   [ ] Please have final versions of contracts and documentation added/updated in this repo **no less than 8 hours prior to contest start time.**
-   [ ] Ensure that you have access to the _findings_ repo where issues will be submitted.
-   [ ] Promote the contest on Twitter (optional: tag in relevant protocols, etc.)
-   [ ] Share it with your own communities (blog, Discord, Telegram, email newsletters, etc.)
-   [ ] Optional: pre-record a high-level overview of your protocol (not just specific smart contract functions). This saves wardens a lot of time wading through documentation.
-   [ ] Designate someone (or a team of people) to monitor DMs & questions in the C4 Discord (**#questions** channel) daily (Note: please _don't_ discuss issues submitted by wardens in an open channel, as this could give hints to other wardens.)
-   [ ] Delete this checklist and all text above the line below when you're ready.

* * *

# SKALE contest details

-   $118,750 USDC main award pot
-   $6,250 USDC gas optimization award pot
-   Join [C4 Discord](https://discord.gg/code4rena) to register
-   Submit findings [using the C4 form](https://code4rena.com/contests/2022-02-skale-contest/submit)
-   [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
-   Starts February 17, 2022 00:00 UTC
-   Ends March 2, 2022 23:59 UTC

This repo will be made public before the start of the contest. (C4 delete this line when made public)

[ ⭐️ SPONSORS ADD INFO HERE ]

| Contract Name                                  | Lines of Code |
| ---------------------------------------------- | ------------- |
| `MessageProxy.sol`                             |               |
| `Messages.sol`                                 |               |
|                                                |               |
| `mainnet/CommunityPool.sol`                    |               |
| `mainnet/DepositBox.sol`                       |               |
| `mainnet/Linker.sol`                           |               |
| `mainnet/MessageProxyForMainnet.sol`           |               |
| `mainnet/SkaleManagerClient.sol`               |               |
| `mainnet/Twin.sol`                             |               |
|                                                |               |
| `mainnet/DepositBoxes/DepositBoxEth.sol`       |               |
| `mainnet/DepositBoxes/DepositBoxERC20.sol`     |               |
| `mainnet/DepositBoxes/DepositBoxERC721.sol`    |               |
| `mainnet/DepositBoxes/DepositBoxERC1155.sol`   |               |
|                                                |               |
| `schain/CommunityLocker.sol`                   |               |
| `schain/KeyStorage.sol`                        |               |
| `schain/MessageProxyForSchain.sol`             |               |
| `schain/TokenManager.sol`                      |               |
| `schain/TokenManagerLinker.sol`                |               |
|                                                |               |
| `schain/bls/FieldOperations.sol`               |               |
| `schain/bls/Precompiled.sol`                   |               |
| `schain/bls/SkaleVerifier.sol`                 |               |
|                                                |               |
| `schain/TokenManagers/TokenManagerERC20.sol`   |               |
| `schain/TokenManagers/TokenManagerERC721.sol`  |               |
| `schain/TokenManagers/TokenManagerERC1155.sol` |               |
|                                                |               |
| `schain/tokens/ERC20OnChain.sol`               |               |
| `schain/tokens/ERC721OnChain.sol`              |               |
| `schain/tokens/ERC1155OnChain.sol`             |               |
| **Total**                                      |               |


## SKALE Network - IMA Bridge

The SKALE Network is an Ethereum-native multichain network, where dApps run on dApp-specific chains. The entire network, its chains, and validators are orchestrated by SKALE Manager contracts, which are deployed on Ethereum mainnet. 

Each chain is supported by 16 randomly selected nodes in the SKALE Network. Each node runs SKALE software, and communicates with other SKALE chains and Ethereum. 

The IMA Bridge is the native bridge for all SKALE chains: enabling messages to be sent between Ethereum and SKALE chains, and between any two SKALE chains. 

The IMA Bridge consists of four parts:

1. Message Proxy contracts (Ethereum + SKALE chains)
2. Deposit Box contracts (on Ethereum)
3. Token Manager contracts (on SKALE chains)
4. IMA Agent - a containerized service on each SKALE chain node that relays messages between chains.

<img src="http://www.plantuml.com/plantuml/svg/ZP5TQiGW58NVxoekBc10ku59cNaeRI3GRa3CfGcD6hm6KahsNdz2dr8oFiWv7F4xNgySTOYBdS3vdl0U1mgqMFm1JCluQI8JH-yOnOrcpsF4PxyI2zICjwwSqf_a8egMc9F4BlZrk-Hsbh01xFbBss2JPScIa_yc2ceTyVxQlDtH37fqA4lAHXwL-_1VvB3LBbqPQhjevLaz1TiHIUqazJ19dP6UCkblkfTBVN_Uic5JjAfQGV9Prad0bLoVV-WN">

### Setup

### General Flows

#### Ethereum --> SKALE deposit

 
#### SKALE --> Ethereum exit


#### SKALE --> SKALE transfer



### Upgradeability

The IMA Bridge implements a transparent upgradeable proxy for the Mainnet contracts to be controlled by multisig and eventually governance. IMA contracts on SKALE chains are upgradeable only by the SKALE chain owner.
