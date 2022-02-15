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

The SKALE Network is an Ethereum-native multichain network, where dApps run on dApp-specific SKALE chains. The entire network, its chains, and validators are orchestrated by SKALE Manager contracts, which are deployed on Ethereum mainnet. 

Each SKALE chain is supported by 16 randomly selected nodes in the SKALE Network. Each node runs SKALE software, and communicates with other SKALE chains and Ethereum.

SKALE chains operate in a cost-free gas environment using a native gas token called sFUEL. sFUEL has no economic value, and is allocated from the SKALE chain owner (SKALE chain owner is the dApp developer who operates a dApps-specific SKALE chain). Owners are free to use any way to distribute sFUEL to end-users, either by onboarding, faucet, or allowing end-users to run a small PoW script.

## SKALE Network flows

### Example use case 1

A Dapp Developer (say *TRISWAP*) desires a "gas-free" platform for its DEX. *TRISWAP* requests a SKALE chain from the network and deposits SKL tokes for leasing a SKALE chain. The SKALE chain is created, designates *TRISWAP*'s multisig as the owner, and IMA SKALE chain contracts are pre-deployed on this chain. TRISWAP can then begin to customize the IMA bridge settings, and permission system.

TRISWAP, being a stablecoin-only DEX, decides to only allow specific ERC20 stablecoins. TRISWAP, with whitelist enabled, adds the stablecoin contracts to IMA mainnet designating it's SKALE chain name. https://docs.skale.network/ima/1.2.x/managing-erc20#_3_register_ethereum_mainnet_contract_to_ima.

TRISWAP enables automatic deployment, such that any time a user first deposits any one of the whitelisted stablecoins, a token clone (ERC20OnChain.sol) is created and mapped/linked.  Any subsequent deposit of this token by any other user will use this mapping.  Once a token is linked to it's mainnet contract, it cannot be relinked.

TRISWAP wishes to improve the exit process. The out-of-the-box exit process requires end-users to first deposit ETH into a CommunityPool. This CommunityPool is used to reimburse SKALE nodes that submit the exit transaction to Ethereum. Because of Ethereum network gas volatility, the deposit required for safe exits is more than the exit transaction itself. TRISWAP wishes to subsidize the exit process from a specific wallet. TRISWAP registers extra contracts on Ethereum, and deploys new contracts such that each user exit pulls from a single wallet on Ethereum.

### Example use case 2

A dApp developer (say *ETHMan*) desires a "gas-free" platform for its Play2Earn game. As in the above example, ETHMan is provisioned a SKALE chain. ETHMan 


The IMA Bridge is the native bridge for all SKALE chains: enabling messages to be sent between Ethereum and SKALE chains, and between any two SKALE chains. 

The IMA Bridge consists of four parts:

1.  Message Proxy contracts (Ethereum + SKALE chains)
2.  Deposit Box contracts (on Ethereum)
3.  Token Manager contracts (on SKALE chains)
4.  IMA Agent - a containerized service on each SKALE chain node that relays messages between chains.

![overview-diagram](http://www.plantuml.com/plantuml/svg/ZP91QiCm44NtSuh11mX8u-xZaYnAQmYq5n3Aq9ZQKl0ea59ozqgMwABOs5vzwGr-7pHx2MOCjw47vy-Cnt3XaMy3_W36p_g-PniwxmIh0r-zT06V_PsbGYDuE4rJvfDTmAfbaHZnDFhxzyI7gu87GE4lRODDYXEB9xL8z28Xo4MhzzVcxOZsOZg7Qg9YrLpj3__53blZuY_7t3iCQgsuXiUSIHUJtcpIQoQQDr4nqMOJhPdgULDTJFLcKxrcUagclrtQxV9h_xiWIBVf85Qbh7FMALFE196LUGq0UtRdjAo_)

ifndef:

<figcaption>High Level Architecture. Any SKALE chain may be connected with IMA Bridge to Ethereum or another SKALE chain. Here is an example of four SKALE chains where SKALE chain 1 and 3 are connected to Ethereum, and SKALE chain 2 is connected to SKALE chain 1. SKALE chain 4 is not connected to any other chain. The IMA Agent is a separate multiple instance resource that listens and shuttles messages between chains.</figcaption>

### Setup

You need nodejs 14 or later and yarn to be installed on your machine

1. clone [the repo](https://github.com/skalenetwork/IMA)
1. run

   ```bash
   yarn install
   ```

1. go to `proxy` folder

    ```bash
    cd proxy
    ```

#### Unit tests

To run all unit tests run

```bash
yarn test
```

If you want to run any particular test (for example `MessageProxy.ts`) use

```bash
npx hardhat test test/MessageProxy.ts
```

### General Flows

Setup and development is covered in detail here: <https://docs.skale.network>

👀 current audit scope covers IMA version v1.2.x <https://docs.skale.network/ima/1.2.x/> (be sure the version selector on the top right reads `1.2.x Preview`)

Getting Started <https://docs.skale.network/ima/1.2.x/getting-started>

Diagramed flows <https://docs.skale.network/ima/1.2.x/flows>

#### Ethereum --> SKALE deposit

<https://docs.skale.network/ima/1.2.x/transferring-eth>
<https://docs.skale.network/ima/1.2.x/managing-erc20>
<https://docs.skale.network/ima/1.2.x/managing-erc721>
<https://docs.skale.network/ima/1.2.x/managing-erc1155>

#### SKALE --> Ethereum exit

<https://docs.skale.network/ima/1.2.x/transferring-eth#_retrieve_eth>
<https://docs.skale.network/ima/1.2.x/managing-erc20#_2_exit_from_skale_chain>
<https://docs.skale.network/ima/1.2.x/managing-erc721#_2_exit_from_skale_chain>
<https://docs.skale.network/ima/1.2.x/managing-erc1155#_2_exit_from_skale_chain>
<https://docs.skale.network/ima/1.2.x/funding-exits>

#### SKALE --> SKALE transfer

<https://docs.skale.network/ima/1.2.x/s2s-transferring-erc20>

### Adding custom messages

<https://docs.skale.network/ima/1.2.x/message-proxy>

### Access Control

IMA Bridge uses OpenZeppelin's Access Control framework to set roles and permissions. A developer overview is here: 

<https://docs.skale.network/ima/1.2.x/access-control>

### Prior Audits

IMA Bridge

-   Nov 2020 <https://certificate.quantstamp.com/full/skale-proxy-contracts>
-   Jun 2021 <https://bramah.systems/audits/SKALE_Audit_Bramah.pdf>

Cryptography contracts (FieldOperations.sol, Precompile.sol, SkaleVerifier.sol)

-   <https://consensys.net/diligence/audits/2020/10/skale-network/appendices/SKALE%20Audit%20V2.pdf>

### Note on contract sizes

SKALE chains can support contract sizes greater than sizes allowed on Ethereum (24kB), therefore you will notice some TokenManager contract sizes > 24kB.

### Special Interfaces

IMA Bridge mainnet interaction with SKALE Manager:

-   requesting SKALE chain names
-   verifying BLS signatures on Ethereum mainnet

IMA Bridge SKALE chain contracts load config file BLS public keys for a SKALE chain using a special Precompile.sol contract.

### Gas Optimization Notes

Everything on the SKALE chain operates in a cost-free gas environment, so no need for optimizations there (`schains/*`). Of course, gas optimization strategies are welcome for IMA contracts on Ethereum mainnet.

### Upgradeability

The IMA Bridge implements OpenZepplin's `contracts-upgradeable` system. Mainnet contracts are upgradeable by mutlisig and eventually governance. SKALE chains are upgradeable only by the SKALE chain owner which may be multisig or governance at the discretion of the SKALE chain owner.
