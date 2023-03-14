# Margin Requirements

Margin requirements are a foundational pillar to lending protocol architecture and important to understand when lending, borrowing, or trading on margin.

## The Basics

* The marginfi protocol is an **overcollateralized lending protocol**, which means you need to deposit collateral before you can borrow against it
* In decentralized, overcollateralized lending protocols, lenders are primarily exposed to two types of risk that are important to understand:
  * Liquidity Risk
  * Interest Rate Risk
*

## An overview of leverage

When users borrow from lending protocols, they take on _leverage._

In general, taking on leverage means borrowing funds or using financial instruments to increase the potential returns of an investment. When you invest with leverage, you are essentially using borrowed money to increase the size of your investment, allowing you to potentially generate greater returns than you would be able to with your own funds alone.

Throughout finance, leverage can be used in a variety of different financial markets, including stocks, bonds, and currencies. Like everywhere else, it is a popular instrument in decentralized finance, where traders can leverage their investments to magnify their returns.

However, leveraging also increases the risk of losses. If your investments decrease in value, you risk not only losing your own initial funds but also the borrowed funds that you used to leverage your position. Taking on leverage carries a higher level of risk and requires additional consideration and risk management.

## Risks to lenders

Leverage poses several risks to lenders. When lenders provide funds for leveraged investments, they are exposed to the potential losses that can occur if the borrower's investments decrease in value. Traditionally, risks are categorized a few ways:

### Credit Risk

Credit Risk refers to the risk lenders take on that those borrowing their funds will default on their loan and simply not repay it.

In traditional financial systems, loans are often provided uncollateralized or undercollateralized; in other words, lenders lend to borrowers based on a trust that borrowers will repay loans. This trust is often protected by borrower reputations, which can be reflected in credit scores, organizational reputations, or even just personal relationships.

In traditional permissionless lending protocols, borrowers cannot be naively trusted to repay loans. There are many approaches to tackling this problem, including:

* **Overcollateralization:** Requiring users who want to borrow to _first_ deposit assets of higher value than they intend to borrow, deposits which are called **collateral**.
* **On-chain credit scores:** Systems that allow users to build borrowing on-chain reputations, and increase the flexibility in borrows they're allowed to make based on their historical activity.

Today, the marginfi protocol is an **overcollateralized lending protocol.** This means that users are required to deposit assets as collateral before they are allowed to borrow from the protocol.

Technically speaking, credit risk is irrelevant to overcollateralized lending protocols. However, overcollateralization architectures pose other risks, discussed below.

### Liquidity Risk

Liquidity Risk refers to the risk that lenders take on that they will not be able to sell the collateral held from borrowers in a timely manner if need be, leading to losses if the borrower is unable to repay the loan.

Unlike Credit Risk, Liquidity Risk is _maximally_ relevant to overcollateralized lending protocols due to their foundation in collateralized borrowing.

Compared to traditional financial systems, Liquidity Risk looks a bit different in a typical decentralized lending protocol.

#### In most permissionless lending protocols, Liquidity Risk incentives are misaligned

From a financial lens, lenders are ultimately the ones who take on Liquidity Risk (it's _their_ money that is at risk of being lost). However, the practical existence of Liquidity Risk is a bit more nuanced.

In traditional financial systems, Liquidity Risk _taken_ by lenders but _managed_ by the lending institutions that facilitate borrowing. For example, a bank that provides loans and needs funds to facilitate those loans may incentivize bank deposits in return for a favorable yield. In this scenario, customers who deposit are ultimately the lenders that take on Liquidity Risk, but the bank _manages_ that Liquidity Risk by controlling who's allowed to borrow funds and how much.

Looking only at this part of the lending paradigm, permissionless lending protocols work similarly:

* Users can _deposit_ funds into lending protocols to earn a yield, taking on Liquidity Risk
* Other users can _borrow_ those funds
* Protocols _manage_ Liquidity Risk by controlling the safety constraints under which users are allowed to borrow

The difference between traditional financial systems and permissionless lending protocols emerges when borrowers take on losses, and their loans are exposed to liquidation.

In the context of collateralized lending (whether it be traditional financial systems or permissionless ones), borrowers can be liquidated when the collateral they've posted for the loans they're taken out drops too low in value relative to the loans they have outstanding.

Executing liquidations is a key part of _managing_ Liquidity Risk to lenders. Here's where the difference between traditional financial systems and permissionless protocols becomes key:

* In **traditional financial systems**, liquidations are executed either by lending instutitions or related parties that have strong relationships with lending institutions. These parties have organizational reputations at stake and strong incentive to execute liquidations well.
* In **permissionless financial systems**, liquidations for typical lending protocols are executed by anonymous, third-party liquidators with executions off-chain.\
  These liquidators are usually financially incentivized to complete individual liquidations, but bear **zero** reputational risk or future earnings risk. This means that a given liquidator can easily choose _not_ to execute liquidations at any moment without concern for future earnings potential from liquidations, ultimately exposing lenders to Liquidity Risk that is hard to quantify.\
  The misalignment can be framed as such:
  * Liquidators control liquidation execution, bearing only small earnings risk
  * Protocols bear the reputational risk of liquidation execution
  * Lenders bear the liquidity risk of liquidation execution

The marginfi protocol is designed to support highly performant [liquidation engines](../advanced-concepts/high-performance-liquidations.md), with an emphasis on investing in this dimension of protocol safety in the future.

### Market Risk

Market Risk refers to the risk lenders take on that the _investments_ borrowers make with loans they've borrowed decrease due to market fluctuations, leading to losses for both borrowers and lenders.

Market Risk is _directly_ out of scope for overcollateralized permissionless lending protocols due to their overcollateralization, but it is generally relevant for lenders to understand that borrowers are likely taking out loans to do something with them.

### Interest Rate Risk

Interest Rate Risk refers to the risk lenders take on that a change in interest rates may affect:

* Borrowers' solvency
* Lenders' earnings

As mentioned above, borrower solvency exposes lenders to Liqudity Risk, so Interest Rate Risk and Liquidity Risk are related.

\[TBF]
