# ✨ So you want to sponsor a contest

This `README.md` contains a set of checklists for our contest collaboration.

Your contest will use two repos: 
- **a _contest_ repo** (this one), which is used for scoping your contest and for providing information to contestants (wardens)
- **a _findings_ repo**, where issues are submitted. 

Ultimately, when we launch the contest, this contest repo will be made public and will contain the smart contracts to be reviewed and all the information needed for contest participants. The findings repo will be made public after the contest is over and your team has mitigated the identified issues.

Some of the checklists in this doc are for **C4 (🐺)** and some of them are for **you as the contest sponsor (⭐️)**.

---

# Contest setup

## ⭐️ Sponsor: Provide contest details

Under "SPONSORS ADD INFO HERE" heading below, include the following:

- [ ] Name of each contract and:
  - [ ] source lines of code (excluding blank lines and comments) in each
  - [ ] external contracts called in each
  - [ ] libraries used in each
- [ ] Describe any novel or unique curve logic or mathematical models implemented in the contracts
- [ ] Does the token conform to the ERC-20 standard? In what specific ways does it differ?
- [ ] Describe anything else that adds any special logic that makes your approach unique
- [ ] Identify any areas of specific concern in reviewing the code
- [ ] Add all of the code to this repo that you want reviewed
- [ ] Create a PR to this repo with the above changes.

---

# ⭐️ Sponsor: Provide marketing details

- [ ] Your logo (URL or add file to this repo - SVG or other vector format preferred)
- [ ] Your primary Twitter handle
- [ ] Any other Twitter handles we can/should tag in (e.g. organizers' personal accounts, etc.)
- [ ] Your Discord URI
- [ ] Your website
- [ ] Optional: Do you have any quirks, recurring themes, iconic tweets, community "secret handshake" stuff we could work in? How do your people recognize each other, for example? 
- [ ] Optional: your logo in Discord emoji format

---

# Contest prep

## ⭐️ Sponsor: Contest prep
- [ ] Make sure your code is thoroughly commented using the [NatSpec format](https://docs.soliditylang.org/en/v0.5.10/natspec-format.html#natspec-format).
- [ ] Modify the bottom of this `README.md` file to describe how your code is supposed to work with links to any relevent documentation and any other criteria/details that the C4 Wardens should keep in mind when reviewing. ([Here's a well-constructed example.](https://github.com/code-423n4/2021-06-gro/blob/main/README.md))
- [ ] Please have final versions of contracts and documentation added/updated in this repo **no less than 8 hours prior to contest start time.**
- [ ] Ensure that you have access to the _findings_ repo where issues will be submitted.
- [ ] Promote the contest on Twitter (optional: tag in relevant protocols, etc.)
- [ ] Share it with your own communities (blog, Discord, Telegram, email newsletters, etc.)
- [ ] Optional: pre-record a high-level overview of your protocol (not just specific smart contract functions). This saves wardens a lot of time wading through documentation.
- [ ] Designate someone (or a team of people) to monitor DMs & questions in the C4 Discord (**#questions** channel) daily (Note: please *don't* discuss issues submitted by wardens in an open channel, as this could give hints to other wardens.)
- [ ] Delete this checklist and all text above the line below when you're ready.

---

# SKALE contest details
- $118,750 USDC main award pot
- $6,250 USDC gas optimization award pot
- Join [C4 Discord](https://discord.gg/code4rena) to register
- Submit findings [using the C4 form](https://code4rena.com/contests/2022-02-skale-contest/submit)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts February 17, 2022 00:00 UTC
- Ends March 2, 2022 23:59 UTC

This repo will be made public before the start of the contest. (C4 delete this line when made public)

## DKG & BLS signature

SKALE Network is a network of nodes running by different validators which are running SKALE chains.
Each SKALE chain running on 16 randomly picked nodes and consume some part of node(1/32, 1/8, 1).
Creating of schain is a on chain operation in SKALE Manager contracts.
After transaction of creating a SKALE chain "A" was sent, DKG round between all these 16 nodes started.
During DKG round each party should generate and send encrypted key share and receive and decrypt key shares
from other parties. When everyone sent and received all information each party should send a tx that
everything is good. After the last transaction was sent common BLS public key of SKALE chain "A"
would be calculated and stored in SKALE Manager contracts.

After successful DKG round between nodes, SKALE chain "A" would start working(blockchain is spinned up &
all services start working). Each node has its own BLS private key, and the common BLS public key stored
in SKALE Manager contracts. When new block is mined on a SKALE chain "A" that means that at least 11 of 16
nodes signed this block by BLS private key and this block was verified by common BLS public key of SKALE
chain "A". Also during each transfer (Mainnet -> Schain), (Schain -> Mainnet) and (Schain -> Schain)
BLS signature would be verified.
- (Mainnet -> Schain "A"), (Schain "A" -> Mainnet) - BLS signature would be verified by common BLS public key of SKALE chain "A".
- (Schain "A" -> Schain "B") - BLS signature would be verified by common BLS public key of SKALE chain "B".

To read more about DKG & BLS:
- https://skale.network/blog/bls-deep-dive/
- https://docs.skale.network/technology/intro-ecc
- https://docs.skale.network/technology/dkg-bls

By the way DKG & BLS was audited.

[ ⭐️ SPONSORS ADD INFO HERE ]
