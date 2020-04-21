---
sip: ?
title: SUSD liquidity smart contract risk diversification
status: Proposed
author: Kenny White <kenny@cowri.io> (@kenny-white) and James Foley <james@cowri.io> (@realisation) 
discussions-to: <https://discord.gg/8W8vBfK>

created: 2020-04-21
---

<!--You can leave these HTML comments in your merged SIP and delete the visible duplicate text guides, they will not appear and may be helpful to refer to if you edit it again. This is the suggested template for new SIPs. Note that an SIP number will be assigned by an editor. When opening a pull request to submit your SIP, please use an abbreviated title in the filename, `sip-draft_title_abbrev.md`. The title should be 44 characters or less.-->

## Simple Summary

<!--"If you can't explain it simply, you don't understand it well enough." Provide a simplified and layman-accessible explanation of the SIP.-->

This is an SIP to add an incentivized Shell pool for sUSD in order to diversify smart contract risk.

## Abstract

<!--A short (~200 word) description of the technical issue being addressed.-->

Incentivized liquidity provision for sUSD is an important aspect of the protocol. Recently, the Curve pool for sUSD found a bug and had to be taken down. This highlights the smart contract risk of relying on only one AMM implementation. Synthetix can diversify their exposure to smart contract risk by incentivizing a Shell protocol liquidity pool. This proposal advocates to divert a portion of the SNX inflation to incentivize sUSD liquidity in Shell.



## Motivation

<!--The motivation is critical for SIPs that want to change Synthetix. It should clearly explain why the existing protocol specification is inadequate to address the problem that the SIP solves. SIP submissions without sufficient motivation may be rejected outright.-->

An sUSD pool on Curve was enticing because unlike Uniswap and Balancer, Curve is highly efficient for stablecoin-to-stablecoin trades. Its design can facilitate large trades with low slippage. However, the pool had to be taken down because of a vulnerability in the smart contract. In order to diversify smart contract risk, there needs to be a second audited stablecoin-optimized AMM implementation. 

The Shell Protocol is a weighted liquidity pool optimized for stablecoin-to-stablecoin conversion. Like Curve, Shell can facilitate large trades at low slippage. Currently, 40% of a stablecoin’s balance can be traded at 3.5 bps of slippage (assuming the pool is balanced). 

Beyond low slippage, Shell has two additional features that benefit liquidity providers. First, Shell pools have built-in protections against a broken stablecoin that has permanently lost its peg. When the pool becomes too unbalanced, i.e. there is too much or too little of a token, it will halt trades that exacerbate the imbalance until it has been rebalanced. That way, a broken peg will not drain the entire pool, which would be the case in Uniswap or Curve.

The second feature is dynamic liquidity provider fees. In most protocols, the liquidity provider fee is constant and any additional price slippage would accrue to arbitrage traders. In the Shell Protocol, some of this price slippage will instead accrue to liquidity providers in the form of an additional dynamic fee. Under the right circumstances, liquidity provider fees can be 10x-100x higher on certain trades. 

## Specification

<!--The technical specification should describe the syntax and semantics of any new feature.-->

1. Users add liquidity to the Shell<>sUSD pool. 
2. Users then stake their pool tokens (shells) to the Shellpool time staking contract. 
3. Anyone can call Synthetix.mint() to mint the inflationary supply. This will then be sent to the RewardsDistribution contract where it will send an amount of tokens to the Shellpool contract. 
4. Shell token stakers will be assigned their % amount of SNX rewards based on their % of staked shell tokens. 
5. Shell token stakers will go to the Shellpool contract or use Mintr UI to claim their SNX rewards anytime.

## Rationale

<!--The rationale fleshes out the specification by describing what motivated the design and why particular design decisions were made. It should describe alternate designs that were considered and related work, e.g. how the feature is supported in other languages. The rationale may also provide evidence of consensus within the community, and should discuss important objections or concerns raised during discussion.-->

This is the same specification for incentivizing liquidity on Uniswap and Curve. From a mechanism design standpoint, both programs have proven to be successful.

## Test Cases

<!--Test cases for an implementation are mandatory for SIPs but can be included with the implementation..-->

TBD

## Implementation

<!--The implementations must be completed before any SIP is given status "Implemented", but it need not be completed before the SIP is "Approved". While there is merit to the approach of reaching consensus on the specification and rationale before writing code, the principle of "rough consensus and running code" is still useful when it comes to resolving many discussions of API details.-->

Currently, the Shell protocol is being audited by ABDK. The first pool will feature sUSD.

## Copyright

Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
