# Oracles

## Pyth

The marginfi protocol uses [Pyth](https://pyth.network/) oracle price feeds for token market prices where available.

Pyth's price oracles provide extensive safety measures that are not implemented by protocols universally. The marginfi protocol leverages Pyth's safety features to their maximum potentially, allowing for a safer understanding of token price activity and risk management.

Below, the marginfi protocol's implementation of Pyth's safety features are discussed.

### Price Availability

__[_Related Pyth docs_](https://docs.pyth.network/pythnet-price-feeds/best-practices#price-availability)__

#### The marginfi protocol only supports assets that trade 24/7

Today, the marginfi protocol only supports assets which are available for trading globally 24/7 (in other words, crypto markets do not close overnight like traditional equity markets). Pyth supports price feeds for both crypto markets and traditional equity markets, so this distinction is important to note despite it possibly seeming obvious.

#### Because marginfi is only live on Solana today, Pyth prices comes from Solana mainnet-beta, _not_ from Pyth's Pythnet

You can read more about Pythnet [here](https://docs.pyth.network/design-overview/pythnet), but it's key to note that because marginfi is live on Solana today, marginfi's usage of Pyth is also dependent on the Solana blockchain because Solana price feeds from Pyth are the only Pyth feeds that live on Solana, not on Pyth's new Pythnet.

This is a minor note given marginfi's current overall dependence on the Solana blockchain, but for the sake of posterity is noted here.

**The marginfi protocol applies a stricter staleness check than Pyth**

Price staleness happens when an oracle provides price data that is out of date. This can be extremely dangerous to protocol operations, especially in highly volatile market environments.

Pyth SDKs have a guard by default against this failure mode by incorporating a staleness check, but the marginfi protocol goes a **step further** and explicitly defines its own maximum valid price staleness.

### Latency

__[_Related Pyth docs_](https://docs.pyth.network/pythnet-price-feeds/best-practices#latency)__

**MEV-aware protocol design** is a crucial and under-discussed part of protocol architecture. Most protocol architectures make no mention of MEV-aware design or related tradeoffs that have been made, which can affect user experience.

The marginfi protocol is not considered MEV-aware today, which means it is as exposed to MEV searcher activity as any other lending protocol on the Solana blockchain. That said, the foundation for increasingly MEV-aware design has been laid with the v2 protocol and future designs are expected to make progress on this architecture dimension significantly.

### Confidence Intervals

__[_Related Pyth docs_](https://docs.pyth.network/pythnet-price-feeds/best-practices#price-availability)__

One of Pyth's key safety features is the confidence intervals that are published with each price feed.

#### **Why would prices need confidence intervals?**

From Pyth docs:

> Pyth publishes a confidence interval because, in real markets, there is _no one single price for a product_. For example, at any given time, bitcoin trades at different prices at different venues around the world. While these prices are typically similar, they can diverge for a number of reasons, such as when a cryptocurrency exchange blocks withdrawals on an asset. If this happens, prices diverge because arbitrageurs can no longer bring prices across exchanges into line. Alternatively, prices on different venues can differ simply because an asset is highly volatile at a particular point in time. At such times, bid/ask spreads tend to be wider, and trades on different markets at around the same time tend to occur at a wider range of prices.
>
> Pyth represents these possibly-different prices by giving its users a _probability distribution over price_ instead of just a single price. Pyth models the price according to a Laplace distribution centered on the Pyth aggregate price with a standard deviation equal to the confidence interval (the scale parameter b of the Laplace distribution is equal to the standard deviation divided by the square root of 2). The Laplace distribution contains \~95% of the probability mass within \~2.12 standard deviations (\~3 times the scale parameter). If markets are behaving normally, then the confidence interval will be tight -- typically much less than 1% of the price -- and the Laplace distribution will be highly peaked. However, at unusual times, the confidence interval can widen out dramatically.

#### Making conservative price estimates

marginfi makes full use of Pyth's confidence intervals, conservatively pricing tokens **on different sides of confidence bands depending on how the tokens are used within marginfi.**

* **Deposits**, or tokens that are lent, are priced at the _low_ end of Pyth's 95% confidence interval. This causes collateral in marginfi to be valued _less_, which yields a probabilistically more conservative and safer lending experience.
* **Borrows**, or tokens that are borrowed, are priced at the _high_ end of Pyth's 95% confidence interval. This causes liabilities in marginfi to be value _more_, which yields a probabilistically more conservative and safer lending experience.

#### Using Exponential Moving Average price to dampen the effect of volatile price swings

High price volatility creates uncertainty in true asset price, and can happen during times of market turmoil or during attempts of price manipulation.

The marginfi protocol leverages Pyth's exponential moving average price aggregation, which estimates the average price of an asset over a specified time period.

**It's important to understand how Pyth calculates EMA, which can affect final token prices and trust assumptions.** From Pyth EMA price aggregation docs, which are linked below:

> The EMA Price (`ema_price`) and EMA Confidence (`ema_confidence`) values are derived directly from the aggregated prices and confidences Pyth has generated on-chain. Publishers do not submit either EMA Price or EMA Confidence values, they only publish to Solana a “live” price and its associated confidence interval which will, in turn, be used for EMA Price and EMA Confidence calculation.
>
> The current Pyth averaging method is a slot-weighted, inverse confidence-weighted exponential moving average of the aggregate price (and confidence interval).
>
> * **Slot weighted** — The Pyth EMA uses the Solana slot number to measure the passage of time. The averaging period is 5921 slots, which corresponds to approximately 1 hour on Solana mainnet.
> * **Inverse confidence weighted** — Weighting each sample by 1/Confidence lets the EMA give more weight to samples with tight confidence and ignore samples with very wide confidence. Below is an example of an outlier aggregate price with a wide confidence interval. Notice how the average using inverse confidence weighting does not get pulled up by the outlier sample while the uniform weighted average does.

[Learn more about Pyth's EMA price aggregation here.](https://docs.pyth.network/design-overview/ema-price-aggregation)

### Pyth: Putting it all together

EMA Price aggregation _paired_ with using price estimates on conservative sides of confidence bands allow marginfi to achieve a few key things unique things at once:

* Conservative estimation of token prices
* Protection against volatility and price manipulation
* A safer and smoother lending experience for users

Nothing in risk management is bulletproof and everything can be improved. Additional safegaurds are intended to be iteratively and persistently added to the marginfi protocol to continously improve the risk measures of the protocol.

## Switchboard

For tokens that Pyth price oracles do not support, [Switchboard](https://switchboard.xyz/) oracles may be used in the future.

Today, the marginfi protocol only uses Pyth oracles.

## Oracle specification through Web Interfaces

Some web interfaces for marginfi may clarify the oracles behind price data information.
