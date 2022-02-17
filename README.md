# SKALE contest details

-   $118,750 USDC main award pot
-   $6,250 USDC gas optimization award pot
-   Join [C4 Discord](https://discord.gg/code4rena) to register
-   Submit findings [using the C4 form](https://code4rena.com/contests/2022-02-skale-contest/submit)
-   [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
-   Starts February 17, 2022 00:00 UTC
-   Ends March 2, 2022 23:59 UTC

# Hello from SKALE

The SKALE core team is extremely excited to present the IMA Bridge to the C4 community for audit. The core team will be ready to answer all your questions help with any onboarding, and clarify anything that may be confusing.

Best of luck!

_SKALE Core team_

## tl,dr

-   SKALE Network is a multichain Ethereum-native PoS gas-free scaling network of > 150 nodes.
-   Each chain is provisioned across 16 random nodes and is [customized by a SKALE chain owner](#Dapp-specific) (a dapp developer, community, or DAO).
-   SKALE Chains run in a gas free environment, with a [free gas-token (sFUEL) used to meter transactions against DDoS](#Gas-free-Environment).
-   The [network is orchestrated](https://skale.network/blog/the-skale-network-primer/) (chain provisioning, node registration, delegation, DKG) from smart contracts on Ethereum (SKALE Manager).
-   **Interchain Messaging Agent (IMA)** Bridge is the native bridge for SKALE.
-   The base layer of the bridge is a [Message Proxy system](#Message-Proxy-System), that shuttles messages between chains through an off-chain IMA agent and uses [BLS threshold signatures](#Distributed-Key-Generation-DKG-amp-BLS-signature) to sign messages.
-   [Two main sets of bridge contracts](#IMA-Bridge-Architecture):
    -   DepositBoxes on Ethereum lock tokens and send messages to connected SKALE chains.
    -   TokenManagers are predeployed on each SKALE chain and lock tokens, create clones, and send messages to connected chains.
-   The Bridge has some [default flows](#Development-Flows) for moving tokens between Ethereum and SKALE, and between SKALE chains.
-   Bridge flow can be [customized by developers to support any arbitrary message or flow](#Adding-custom-messages).
-   Exit transactions are conducted by one of nodes of the SKALE chain and is [reimbursed using a default scheme](#Exit-reimbursement).

## Useful links

-   [SKALE Network](https://skale.network)
-   [Twitter: @SkaleNetwork](https://twitter.com/SkaleNetwork)
-   [SKALE Developer Discord](https://discord.gg/PxX3K43JCm)
-   [SKALE Documentation](https://docs.skale.network/)
-   [Youtube videos](https://www.youtube.com/skale)

### Relevant Blog Posts

-   <https://skale.network/blog/the-skale-network-primer/>
-   <https://skale.network/blog/introduction-of-the-skale-ima-bridge/>

#### Older Video Demos

-   ERC20 transfer Rinkeby &lt;-> SKALE demo, <https://www.youtube.com/watch?v=gDj6QRbuFsQ&t=246s>
-   ERC721 transfer Rinkeby &lt;-> SKALE demo <https://www.youtube.com/watch?v=s8N_d_EoTbk>

## Contact us

Discord handles:

-   @chadwick#5132
-   @Ganna | SKALE#9107
-   @Dmytro#9331

## Video walk-through of smart-contracts

If you prefer a video walk through of SKALE Network, IMA Bridge contracts and logic, https://youtu.be/BcHLJ9oFgMc

| Contract Name                                          | Lines of Code | Lines of Comment |
| ------------------------------------------------------ | ------------- | ---------------- |
| `MessageProxy.sol`                                     | 175           | 313              |
| `Messages.sol`                                         | 177           | 368              |
|                                                        |               |                  |
| `mainnet/CommunityPool.sol`                            | 70            | 128              |
| `mainnet/DepositBox.sol`                               | 48            | 55               |
| `mainnet/Linker.sol`                                   | 82            | 96               |
| `mainnet/MessageProxyForMainnet.sol`                   | 147           | 204              |
| `mainnet/SkaleManagerClient.sol`                       | 33            | 32               |
| `mainnet/Twin.sol`                                     | 49            | 46               |
|                                                        |               |                  |
| `mainnet/DepositBoxes/DepositBoxEth.sol`               | 93            | 128              |
| `mainnet/DepositBoxes/DepositBoxERC20.sol`             | 135           | 229              |
| `mainnet/DepositBoxes/DepositBoxERC721.sol`            | 128           | 203              |
| `mainnet/DepositBoxes/DepositBoxERC1155.sol`           | 157           | 386              |
|                                                        |               |                  |
| `schain/CommunityLocker.sol`                           | 113           | 113              |
| `schain/KeyStorage.sol`                                | 46            | 67               |
| `schain/MessageProxyForSchain.sol`                     | 160           | 229              |
| `schain/TokenManager.sol`                              | 129           | 109              |
| `schain/TokenManagerLinker.sol`                        | 86            | 87               |
|                                                        |               |                  |
| `schain/bls/FieldOperations.sol`                       | 150           | 191              |
| `schain/bls/Precompiled.sol`                           | 31            | 39               |
| `schain/bls/SkaleVerifier.sol`                         | 30            | 69               |
|                                                        |               |                  |
| `schain/TokenManagers/TokenManagerERC20.sol`           | 112           | 297              |
| `schain/TokenManagers/TokenManagerERC721.sol`          | 104           | 231              |
| `schain/TokenManagers/TokenManagerERC1155.sol`         | 138           | 449              |
|                                                        |               |                  |
| `schain/tokens/EthErc20.sol`                           | 46            | 28               |
| `schain/tokens/ERC20OnChain.sol`                       | 34            | 22               |
| `schain/tokens/ERC721OnChain.sol`                      | 54            | 64               |
| `schain/tokens/ERC1155OnChain.sol`                     | 46            | 51               |
|                                                        |               |                  |
| `extensions/ERC721ReferenceMintAndMetadataMainnet.sol` | 21            | 54               |
| `extensions/ERC721ReferenceMintAndMetadataSchain.sol`  | 21            | 43               |
| `extensions/interfaces/MessageProxyClient.sol`         | 19            | 12               |
| `extensions/interfaces/MessageSender.sol`              | 19            | 11               |
| `extensions/interfaces/MessageReceiver.sol`            | 20            | 4                |
|                                                        |               |                  |
| `thirdparty/ERC1155ReceiverUpgradeableWithoutGap.sol`  | 6             | 25               |
| **Total**                                              | 2732          | 4458             |

NOTE: contracts in the `extensions/*` folder are example contracts demonstrating how a developer may expand the IMA bridge with any arbitrary logic with MessageProxy.

## SKALE Network - IMA Bridge

### Protocol Overview

The SKALE Network is an Ethereum-native multichain network, where dApps run on dApp-specific SKALE chains. SKALE Manager contracts orchestrate the entire network, its chains, and validators. SKALE Manager is deployed and operating on the Ethereum mainnet. 

Each SKALE chain is supported by 16 randomly selected nodes in the SKALE Network. Each node runs SKALE software and communicates with other SKALE chains and Ethereum.

### Dapp-specific

SKALE chains are deployed and operated by SKALE chain owners - which may be a dapp developer or community. Owners may set deployment permissions to certain accounts, and may set other configuration options for their chain or IMA bridge that is best fit for their dapp and community. Dapps that run on SKALE chains are provisioned bandwidth such that as an owner you are not sharing bandwidth and resources with other dapps like Ethereum. SKALE chain serves the needs for your dapp and community, and if say SKALE chain run by another owner should become overloaded, it will not affect your SKALE chain.

### Gas-free Environment

SKALE chains operate in a gas-free environment using a native gas token called sFUEL. sFUEL has no economic value and is allocated from the SKALE chain owner (SKALE chain owner is a dApp developer or community who operates a dApp-specific SKALE chain). Owners are free to use various methods to distribute sFUEL to end-users, either by onboarding, faucet, or allowing end-users to run a small PoW script. SKALE chain gas serves a way to meter or limit transaction usage on the SKALE chain to prevent malicious execution for DDoS attacks.

### IMA Bridge Architecture

The IMA Bridge is the native bridge for all SKALE chains: enabling messages to be sent between Ethereum and SKALE chains and between any two SKALE chains. 

Unlink other bridges, IMA bridge is designed to be customized, modified and tailored for any SKALE chain by the SKALE chain owner - who is a dapp developer or community who controls a SKALE chain. The IMA bridge part that is deployed to Ethereum Mainnet is designed to connect to any number of SKALE chains, and supports certain customizations.

The IMA Bridge consists of four parts:

1.  Message Proxy contracts (Ethereum + SKALE chains)
2.  Deposit Box contracts (on Ethereum)
3.  Token Manager contracts (on SKALE chains)
4.  IMA Agent - a containerized service on each SKALE chain node that relays messages between chains.

<img width="829" alt="overview-diagram" src="https://user-images.githubusercontent.com/3477197/154558776-f92af1ab-65f9-430e-8ef9-4a2150d2dfdf.png">

<figcaption>High Level Architecture. Any SKALE chain may be connected with IMA Bridge to Ethereum or another SKALE chain. Here is an example of four SKALE chains where SKALE chains 1 and 3 are connected to Ethereum, and SKALE chain 2 is connected to SKALE chain 1. SKALE chain 4 is not connected to any other chain. The IMA Agent is a separate multiple instance resource that listens and shuttles messages between chains.</figcaption>

## IMA Bridge Example Developer Stories

### Example use case 1

A Dapp Developer (say fictitious _SWAP DAO_) desires a "gas-free" platform for its DEX. _SWAP DAO_ requests a SKALE chain from the Ethereum network and deposits SKL tokens to lease a SKALE chain. The SKALE chain is created from SKALE Manager and IMA SKALE chain contracts are pre-deployed on this chain. _SWAP DAO_ can then customize the IMA bridge settings and permission system, and designate _SWAP DAO_'s Gnosis SAFE multisig as the owner. 

_SWAP DAO_, being a stablecoin-only DEX, decides only to allow specific ERC20 stablecoins. _SWAP DAO_, with `whitelist enabled`, adds the stablecoin contracts to IMA mainnet, designating its SKALE chain name. <https://docs.skale.network/ima/1.2.x/managing-erc20#_3_register_ethereum_mainnet_contract_to_ima>.

_SWAP DAO_ enables automatic deployment, such that any time a user first deposits any one of the whitelisted stablecoins, a token clone (ERC20OnChain.sol) is created and mapped/linked. Any subsequent deposit of this token by any other user will use this mapping. Once a token is linked to its Ethereum mainnet contract, it cannot be relinked.

_SWAP DAO_ wishes to improve upon the "out-of-the-box" or default safe exit process. The default safe exit process requires end-users to first to deposit ETH into a CommunityPool. This CommunityPool is used to reimburse SKALE nodes that submit the exit transaction to Ethereum. Because of Ethereum network gas volatility, the deposit required for safe exits is more than the exit transaction itself. _SWAP DAO_ wishes to subsidize the exit process from a specific wallet, for all end-users. _SWAP DAO_ registers extra contracts on Ethereum and deploys new contracts such that each user exit pulls from a single wallet on Ethereum.

### Example use case 2

A dApp developer (say fictitious _ETHDog_) desires a "gas-free" platform for its Play 2 Earn game where many different types of NFT contracts and collections are generated. As in the above example, _ETHDog_ has provisioned a SKALE chain. _ETHDog_ wishes to 1) send NFT tokens earned in the game to another NFT game _ETHCat_ on the "eth-cat" SKALE chain, and 2) allow "FISH" tokens earned in the game to bridge to "SWAP_DAO", where SWAP_DAO has a FISH/USDC pair deployed on their SKALE chain.

Being a game supporting only one FISH erc20, token, _ETHDog_ and _SWAP DAO_ work together to deploy the FISH token on eth-dog chain, and a token clone on swap-dao chain. Since whitelist is enabled by default, _ETHDog_ manually maps the FISH token to it's clone on swap-dao.

To send NFTs to eth-cat chain, and since there are many nft contracts, eth-dog owner disables the whitelist, and enables automatic deployment, enabling any NFT contract to be automatically mapped and cloned on the eth-cat chain. eth-dog then uses the `transferToSchainERC721` to develop the transfer logic in the backend of the UI. When the end-user conducts a transfer to eth-cat, the ERC721 and tokenURI are cloned over to eth-cat for free, and transfers complete within seconds. 

## Setup

You need nodejs 14 or later and yarn to be installed on your machine

1.  clone [the repo](https://github.com/skalenetwork/IMA)

2.  run

    ```bash
    yarn install
    ```

3.  go to `proxy` folder

    ```bash
    cd proxy
    ```

### Unit tests

To run all unit tests run

```bash
yarn test
```

If you want to run any particular test (for example `MessageProxy.ts`) use

```bash
npx hardhat test test/MessageProxy.ts
```

## Development Flows

Developer setup and usage is covered in detail here: <https://docs.skale.network>

👀 current audit scope covers IMA version v1.2.x <https://docs.skale.network/ima/1.2.x/> (be sure the version selector on the top right reads `1.2.x Preview`)

Getting Started <https://docs.skale.network/ima/1.2.x/getting-started>

Diagramed flows <https://docs.skale.network/ima/1.2.x/flows>

### Ethereum --> SKALE deposit

-   <https://docs.skale.network/ima/1.2.x/transferring-eth>
-   <https://docs.skale.network/ima/1.2.x/managing-erc20>
-   <https://docs.skale.network/ima/1.2.x/managing-erc721>
-   <https://docs.skale.network/ima/1.2.x/managing-erc1155>

### SKALE --> Ethereum exit

-   <https://docs.skale.network/ima/1.2.x/transferring-eth#_retrieve_eth>
-   <https://docs.skale.network/ima/1.2.x/managing-erc20#_2_exit_from_skale_chain>
-   <https://docs.skale.network/ima/1.2.x/managing-erc721#_2_exit_from_skale_chain>
-   <https://docs.skale.network/ima/1.2.x/managing-erc1155#_2_exit_from_skale_chain>
-   <https://docs.skale.network/ima/1.2.x/funding-exits>

### SKALE --> SKALE transfer

-   <https://docs.skale.network/ima/1.2.x/s2s-transferring-erc20>

### Adding custom messages

SKALE chain owners can setup other contracts using the message proxy system. This allows developers to expand beyond the "out-of-the-box" functionalities of Deposit Box and Token Managers to support different flows (Mint NFTs on SKALE first, then send to Ethereum examples are <https://github.com/skalenetwork/IMA/tree/develop/proxy/contracts/extensions> and <https://docs.skale.network/ima/1.2.x/flows#_erc7211155_skale_mint_first>), send arbitrary messages, and more!

-   [read the section below](#message-proxy-system)
-   <https://docs.skale.network/ima/1.2.x/message-proxy>

### Message Proxy System

#### General description

On a basic level, a message in IMA is a bytes sequence of arbitrary length. It is sent between two smart contracts deployed on different chains. To conduct a transfer, each chain has an extension of an abstract smart contract named `MessageProxy`. The `MessageProxy` provides 2 main services:

-   send a message to the target chain
-   execute callback function of receiving smart contract when receiving a message from other chains

MessageProxy has slightly different implementations for Ethereum mainnet and SKALE chain. They follow the main concept but verify messages in different ways. This will be described later.

When `MessageProxy` receives a message to send, it emits an event containing the message. The further transferring is done by an off-chain service named `Agent`. It is run on each node (of 16 nodes) of a SKALE chain. Its purpose is to monitor events from a `MessageProxy`, verify them and send transactions to target `MessageProxy` to perform processing on a destination chain.

Thus the message transfer is done in 3 steps:

1.  A `MessageProxy` emits an event on a source chain.
2.  Multiple `Agents` parse the event, verify it and forward to the destination chain by sending a transaction to the target `MessageProxy`.
3.  The `MessageProxy` on the destination chain verifies the message and executes a callback of a receiver smart contract passing the message as a parameter.

#### Message transfer from Ethereum to SKALE chain

To allow a user to send a message, `MessageProxy` has a function:

```solidity
function postOutgoingMessage(
    bytes32 targetChainHash,
    address targetContract,
    bytes memory data
)
public;
```

The first parameter is a destination chain. It is a keccak256 hash of SKALE chain name or `keccak256("Mainnet")` if it targets to Ethereum.

The second parameter is an address of smart contract that needs to be called on delivery. The smart contract must implement interface `IMessageReceiver`.

```solidity
interface IMessageReceiver {
    function postMessage(
        bytes32 schainHash,
        address sender,
        bytes calldata data
    )
    external
    returns (address);
}
```

Besides the message, the target smart contract will be provided with information about the source chain and sender address.

The third parameter of the `postOutgoingMessage` function is the message itself.

As a result of the function execution, an `OutgoingMessage` event will be emitted. It has the following structure:

```solidity
event OutgoingMessage(
    bytes32 indexed dstChainHash,
    uint256 indexed msgCounter,
    address indexed srcContract,
    address dstContract,
    bytes data
);
```

A `msgCounter` field reflects that all messages in IMA are ordered and numbered. Each pair of chains has its own numeration and messages are always delivered in order that they were sent.

For this purpose, `MessageProxy` maintains incoming and outgoing message counters for each pair of chains. Initially, both of them are equal to 0. The sending of a new message increments the outgoing message counter of source `MessageProxy`. The destination `MessageProxy` accepts only the message with `msgCounter` value that is equal to its incoming message counter. After processing of the message, it increments the incoming message counter.

After event emitting on Ethereum random `Agent` on the target SKALE chain sends a transaction to the `MessageProxy` and the function `postIncomingMessages` is executed.

```solidity
function postIncomingMessages(
    string calldata fromSchainName,
    uint256 startingCounter,
    Message[] calldata messages,
    Signature calldata sign
)
external;
```

Parameters are:

-   `fromSchainName` - source chain

-   `startingCounter` - number of first message in the batch

-   `messages` - batch of messages in sequential order. Each message is a structure

    ```solidity
    struct Message {
        address sender;
        address destinationContract;
        bytes data;
    }
    ```

      representing sender address, receiver address and the message

-   `sign` - [BLS signature](https://docs.skale.network/technology/dkg-bls#_bls_signatures) of parameters. This parameter is very important and allows to guarantee that the function will be executed only if supermajority of nodes in SKALE chain are agreed on the payload values.

After signature verification the destination `MessageProxy` calls function `postMessage` of target smart contract passing initial message.

#### Message transfer from SKALE chain to Ethereum

The processing of the return message is almost the same except for the gas reimbursement procedure. `MessageProxy` on Ethereum measures how much gas was consumed for the message processing and transfers the equivalent amount from the beneficiary account to the node wallet.

For a diagram description of the gas reimbursement procedure, please see the sequence diagram here: <https://docs.skale.network/ima/1.2.x/funding-exits#_exit_reimbursement_flow_process>

## Access Control and Configuration

IMA Bridge uses OpenZeppelin's Access Control framework to set roles and permissions. A developer overview of roles and configuration settings is here: 

<https://docs.skale.network/ima/1.2.x/access-control>

## Distributed Key Generation (DKG) & BLS signature

### Overview

SKALE Network is a network of nodes that are run and maintained by different validators. SKALE nodes support running SKALE chains. Each SKALE chain is run on 16 randomly selected nodes and consume a part of node cpu, memory, and storage resources (1/32, 1/8, 1).

SKALE chain creation is an _on-chain operation on Ethereum mainnet_, conducted in SKALE Manager contracts. After SKALE chain create transaction for SKALE chain "A" is sent, a DKG round between 16 randomly selected nodes is started. During the DKG round, each node should generate and send an encrypted key share and receive and decrypt key shares from other nodes. When all nodes have sent and received all information each node should send a tx that everything is good. After the last transaction is sent, a common BLS public key of SKALE chain "A"
would be calculated and stored in SKALE Manager contracts on Ethereum.

After a successful DKG round between nodes, SKALE chain "A" would start working (blockchain is spun up & all services begin operating). Each node has its own BLS private key, and the common BLS public key is stored in SKALE Manager contracts and locally on each node in its configuration. When a new block is mined on a SKALE chain "A" that means that at least 11 of 16 nodes signed this block by BLS private key and this block was verified by common BLS public key of SKALE chain "A". 

#### DKG & BLS in IMA Bridge

Also during each IMA transfer (Ethereum Mainnet -> SKALE chain), (SKALE chain -> Ethereum Mainnet) and (SKALE chain -> SKALE chain) the BLS signature is verified. For example:

-   (Ethereum Mainnet -> SKALE chain "A"), (SKALE chain "A" -> Mainnet) - BLS signature is verified by common BLS public key of SKALE chain "A".
-   (SKALE chain "A" -> SKALE chain "B") - BLS signature is verified by common BLS public key of SKALE chain "B".

To read more about DKG & BLS:

-   <https://skale.network/blog/bls-deep-dive/>
-   <https://docs.skale.network/technology/intro-ecc>
-   <https://docs.skale.network/technology/dkg-bls>

FYI: [DKG & BLS cryptography was audited](#prior-audits).

### Prior Audits

IMA Bridge

-   Nov 2020 <https://certificate.quantstamp.com/full/skale-proxy-contracts>
-   Jun 2021 <https://bramah.systems/audits/SKALE_Audit_Bramah.pdf>

Cryptography contracts (DKG + BLS, and FieldOperations.sol, Precompile.sol, SkaleVerifier.sol)

-   <https://consensys.net/diligence/audits/2020/10/skale-network/appendices/SKALE%20Audit%20V2.pdf>

## Note on contract sizes

SKALE chains can support contract sizes greater than sizes allowed on Ethereum (24kB), therefore you will notice some TokenManager contract sizes > 24kB.

## Special Interfaces

IMA Bridge mainnet interaction with SKALE Manager:

-   requesting SKALE chain names
-   verifying BLS signatures on Ethereum mainnet

IMA Bridge SKALE chain contracts load config file BLS public keys for a SKALE chain using a special Precompile.sol contract.

## Protections

### Gas Limit

There is a limit of 1M of gas units for a message processing. If the limit is exceeded the call to external contract is reverted. It is more than enough to call transfer function of a regular ERC20 token or similar but in general case requires a sender to ensure that target smart contract does not consume too many gas. As an example a transferring of big batch of ERC1155 tokens may overflow the limit. In this case the message will be considered as processed but a state of a smart contract on a target chain will not be modified.

### Kill

In an extraordinary event, a SKALE chain and its Bridge may be killed if both the SKALE chain owner and the IMA mainnet admin role execute a kill process. Once killed, users are able to retrieve locked deposits.

### Exit Rate

Exits are rate limited to a default 5 minutes per message, and can be set by the `CONSTANT_SETTER_ROLE`.

### Exit reimbursement

Using the default exit process, users must fund their CommunityPool account before conducting an exit with 1,000,000 gas \* gas Price in Wei at time of exit transaction submission. The actual exit transaction cost is deducted from this CommunityPool deposit, and users are able to withdraw any unused funds in their CommunityPool. An oracle process to retrieve a more accurate Ethereum gas Price is currently planned to be released. In an extraordinary event of a user not having sufficient funds in the Community Pool, the user is locked from subsequent exits until they refund the Community Pool, and in the meantime the SKALE chain owner wallet is used to reimburse nodes for the exit transaction.

Note that SKALE chain owners may implement a different exit process than the default one described above, by using custom messages with the Message Proxy system.

## Gas Optimization Notes

Everything on the SKALE chain operates in a gas-free environment, so no need for optimizations there (`schains/*`). Of course, gas optimization strategies are welcome for IMA contracts on Ethereum mainnet.

## Upgradeability

The IMA Bridge implements OpenZeppelin's `contracts-upgradeable` system. Mainnet contracts are upgradeable by multisig and eventually governance. SKALE chains are upgradeable only by the SKALE chain owner which may be multisig or governance at the discretion of the SKALE chain owner.

## Areas of concern for Wardens

We would like wardens to focus on any core functional logic (Ethereum -> SKALE, SKALE -> Ethereum, SKALE -> SKALE), boundary case errors or similar issues which could be utilized by an attacker to steal funds or drain wallets.

Gas optimizations are welcome, please see [Gas Optimization Notes](#gas-optimization-notes).

If wardens are unclear on which areas to look at or which areas are important please feel free to ask in the contest Discord channel.

## Known Issues

- Large batch transfer of ERC1155 may cause out of gas
- Outgoing message with large length may cause issues
- A malicious receiver contract can stuck IMA forever by returning huge revert data
