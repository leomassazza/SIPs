---
sip: <to be assigned>
title: L2 Bridged Governance
status: Draft
author: Leonardo Massazza (@leomassazza), Alejandro Santander (@ajsantander)
discussions-to: https://research.synthetix.io/t/l2-bridged-governance/443

created: 2021-07-13
---

<!--You can leave these HTML comments in your merged SIP and delete the visible duplicate text guides, they will not appear and may be helpful to refer to if you edit it again. This is the suggested template for new SIPs. Note that an SIP number will be assigned by an editor. When opening a pull request to submit your SIP, please use an abbreviated title in the filename, `sip-draft_title_abbrev.md`. The title should be 44 characters or less.-->

## Simple Summary
<!--"If you can't explain it simply, you don't understand it well enough." Simply describe the outcome the proposed changes intends to achieve. This should be non-technical and accessible to a casual community member.-->
Add the ability to govern L2 contracts with a MultiSig (Gnosis Safe) contract instead of using EOA.

## Abstract
<!--A short (~200 word) description of the proposed change, the abstract should clearly describe the proposed change. This is what *will* be done if the SIP is implemented, not *why* it should be done or *how* it will be done. If the SIP proposes deploying a new contract, write, "we propose to deploy a new contract that will do x".-->
This SIP proposes the addition of a bridge to connect L2 contracts to an L1 Gnosis Safe. The bridge will allow the government council to authorize actions on L2 contracts using the same mechanism used on L1. 

## Motivation
<!--This is the problem statement. This is the *why* of the SIP. It should clearly explain *why* the current state of the protocol is inadequate.  It is critical that you explain *why* the change is needed, if the SIP proposes changing how something is calculated, you must address *why* the current calculation is innaccurate or wrong. This is not the place to describe how the SIP will address the issue!-->
Currently L2 contracts are owned by EAO which poses a risk on ownership and security. The proposed SIP allows a contract or multisig to own L2 contracts and enable proper council governance.

## Specification
<!--The specification should describe the syntax and semantics of any new feature, there are five sections
1. Overview
2. Rationale
3. Technical Specification
4. Test Cases
5. Configurable Values
-->

### Overview
<!--This is a high level overview of *how* the SIP will solve the problem. The overview should clearly describe how the new feature will be implemented.-->
The proposed solution is to add a bridge contract that will act as liason between a Gnosis Safe in L1 and the contracts on L2 so that all operations (ownership authorizations on L1 and L2) are done by the council using the same network and known tools.

### Rationale
<!--This is where you explain the reasoning behind how you propose to solve the problem. Why did you propose to implement the change in this way, what were the considerations and trade-offs. The rationale fleshes out what motivated the design and why particular design decisions were made. It should describe alternate designs that were considered and related work. The rationale may also provide evidence of consensus within the community, and should discuss important objections or concerns raised during discussion.-->
During the discussions previous discussions we identified three different options to provide governance on L2 each with its own pros and cons that are shown below.

* **Gnosis Safe in L1 and Gnosis Safe in L2**

    Pros: Same proven mechanism as in L1.

    Cons: Not yet *officialy* available (there are some forks); will require Governance council to connect to both networks.
* **Gnosis Safe in L1 and Legacy Multisig in L2**

    Pros: Easy to implement.

    Cons: Using a Legacy multisig that is not supported by gnosis (there is a working project adapting it to L2); will require Governance council to connect to both networks and use different tools.
* **Gnosis Safe in L1 and Ownership Bridge in L2**

    Pros: Using a single tool to L1 and L2 (Gnosis Safe on L1).

    Cons: Authorizations on L2 will take time due to the bridge propagation process.

From the three options the chosen one is the 3rd that us based on Gnosis Safe in L1 to do all the authorizations (L1 and L2) that will simplify the operations. It requires the addition of a bridge (based on [this CrossChainAccount technique](https://github.com/gakonst/xchain-account/blob/master/contracts/CrossChainAccount.sol)) 

### Technical Specification
<!--The technical specification should outline the public API of the changes proposed. That is, changes to any of the interfaces Synthetix currently exposes or the creations of new ones.-->
Write two new gvernance bridges based on [this CrossChainAccount technique](https://github.com/gakonst/xchain-account/blob/master/contracts/CrossChainAccount.sol) that will link our ownership on L2. 


### Test Cases
<!--Test cases for an implementation are mandatory for SIPs but can be included with the implementation..-->
TBD but will cover
* Set up an integration test to do owner actions on L2 using the bridge and Gnosis Safe
* Test on Kovan using fresh instances
* Deploy and test on mainnet

### Configurable Values (Via SCCP)
<!--Please list all values configurable via SCCP under this implementation.-->
N/A at the moment of writting this SIP

## Copyright
Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
