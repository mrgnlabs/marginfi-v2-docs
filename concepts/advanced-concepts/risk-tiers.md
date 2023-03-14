# Risk Tiers

The marginfi protocol introduces the concept of **Asset Risk Tiers**, which specify how an asset can be used in the protocol.

This allows the marginfi protocol to support more assets safely. Specifically, this is a major design advantage when considering adding support of new, long-tail tokens - e.g. $BONK or $DUST - with highly unpredictable liquidity.

There are two Risk Tiers in marginfi:

## Collateral Tier

The **Collateral Tier** is marginfi's standard asset risk tier. Assets in this risk tier can be used like assets in a traditional lending protocol: they can be deposited, borrowed, and borrowed against within other relevant protocol limits (deposit limits, borrow limits, and loan-to-value (LTV) constraints).

This is considered the safest risk tier in the marginfi protocol, reserved for assets with higher liquidity.

## Isolated Tier

The **Isolated Tier** is for higher-risk assets supported in the marginfi protocol. If an asset is in the Isolated risk tier, traders are not allowed to borrow any assets _other than one type of Isolated Tier asset_ in their marginfi portfolio at a time.

For example, if there are three assets for which borrows are enabled:

* **$SOL** -  Collateral Tier
* **$USDC** - Collateral Tier
* **$XYZ** - Isolated Tier

A trader can borrow $SOL and $USDC together, but in order to borrow $XYZ there must be no other borrows in the portfolio.

## Risk Tier is independent of other risk constraints

It's important to note that the marginfi protocol implements multiple risk measures in its design, and that each of these risk measures acts independently.

Risk Tiers are specified **per-asset** and are independent of deposit limits, borrow limits, deposit weights, borrow weights, or other risk measures.
