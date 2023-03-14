---
description: Where do you pay money? How do you make money?
---

# Fees + Yield

## The Basics

* You pay when you borrow assets
* You earn when you lend assets
* You're penalized with a fee if you get liquidated
* marginfi collects fees for asset-specific insurance funds
* Today, the protocol takes **no fee** for itself (marginfi makes no revenue)

## Borrow Fees

Borrowing on marginfi incurs a fee. Fees are specific to each asset that marginfi supports, usually expressed in terms of APR (Annual Percentage Rate).

The APRs for borrowing each asset are typically exposed in marginfi web interfaces, and can be found in protocol configuration.

### Liquidation Fees

When borrowed trader positions fall below configured margin requirements, they are exposed to liquidation. Liquidations on marginfi are automatic and permissionless.

Liquidations are executed by third-party liquidators who provide this service for a return, and marginfi awards a fee for successful liquidations.

When borrowed positions fall below requirements and are liquidated, liquidated borrowers (or, liquidatees) pay a fee as a penalty.

Currently, liquidation penalties, liquidator fees, and insurance fund fees are fixed. However, liquidation penalties, liquidator fees, and insurance fund fees can be configured for each asset pool.

Today, fees for pools are set as follows (unless specified otherwise):

* Liquidatee penalty: 5% of the liquidatee's position collateral at time of liquidation
* Liquidator fee: Of the 5% the liquidatee pays as a penalty, the liquidator earns half; or, 2.5% of liquidatee's liquidated collateral.
* Insurance fund fee: Of the 5% the liquidatee pays as a penalty, the collateral asset-specific insurance fund collects half; or, 2.5% of the liquidatee's liquidated collateral.

## Deposit Yield

marginfi allows users to deposit supported tokens into the protocol and earn yield on them. This is made possible by lenders on the platform who borrow these tokens and pay interest on them.&#x20;

The deposit yield on marginfi is typically expressed in terms of APY (Annual Percentage Yield). Yield farming has become increasingly popular in DeFi, and marginfi is one of the lending protocols that allows users to earn yield on their deposited assets.

The APYs for lending each asset are typically exposed in marginfi web interfaces, and can be found in protocol configuration.

### Regular marginfi deposits

Traditional marginfi deposits have **no lockup** and earn yield on a continuous basis.

### Liquidity Incentive Program (LIP) deposits

Deposits into marginfi's LIP program may be locked up depending on the LIP campaign they're deposited to, which is available to users in each LIP campaign configuration and can only be set when a campaign is initially created.

LIP lockup timelines cannot be adjusted after campaigns are created by anyone, including campaign creators.

## Protocol Fees

When you borrow from marginfi, part of the fee you pay builds up asset-specific insurance funds in the protocol. The other fee goes directly to lenders in the pools of the assets you borrowed.

Today, marginfi takes no protocol fee for operations. There are no additional fees other than the ones mentioned above.

The lack of additional protocol fees beyond the insurance fund makes marginfi an attractive option for users looking for low-cost lending options.
