---
description: >-
  Capminal is a Clanker UI, here is our guideline to prompt and deploy token on
  Clanker
---

# Token Deployment

## Clanker Introduction

Clanker provide flexible setup of Uniswap V4 pools, better control over liquidity ranges, and smarter reward distribution.

Pool fees are now fully customizable. Fees can be set from **1% to 10%**, split across up to 7 addresses, or adjusted by liquidity range using Static or Dynamic Hooks, instead of the fixed 1% fee in V3.

Support extension system for deeper token customization, including AuctionSnipe, DevBuy, ClankerVault, and ClankerAirdrop. For full details, refer to the official [Clanker Documentation](https://clanker.gitbook.io/clanker-documentation/core-contracts/v4.0.0).

## What types of configurations does Capminal support

Since Capminal is an AI Agent and users will deploy tokens via prompting on our client, we make it more simple for our users to launch token, currently we simplified the configuration process for launching Clanker tokens.&#x20;

We will allow customization of the following 3 configurations:

1. **Pool Fee (default: 1%)**: Supports configuration from **1%** to **10%** and only supports static hooks (applying the same fee across all liquidity).
2. **Initial Buy (default: zero)**: Allows creators to execute the first transaction with a specified amount of ETH.
3. **Market Cap (default: 10 ETH**): Allows creators to create token with 2 level of market cap, 10E and 20E default value if user don't specify market cap is 10E
4. **Reward Recipient (cannot modify):** Currently, when fees are generated, we maintain three fixed reward recipients: **Clanker Team** (currently fixed 0.2% at protocol level), Capminal Team, and Creator. We will support configuring additional reward recipients in the future.

{% hint style="warning" %}
We have observed that pool fees above 10% are highly risky for swappers. We recommend deploying tokens with a **1%** to **3%** fee. A 10% fee means that when a user swaps $1000, they pay $100 in fees, which discourages swapping, especially in specific cases.
{% endhint %}

## LP Structure

When you deploy a token, liquidity is automatically distributed across 5 positions on Uniswap V4. This creates a healthy price curve and ensures good trading depth.

#### Position Distribution

<table><thead><tr><th>Position</th><th width="185.32373046875">Allocation</th><th>Description</th></tr></thead><tbody><tr><td>Position 1</td><td>10%</td><td>Initial price range (tightest)</td></tr><tr><td>Position 2</td><td>50%</td><td>Primary liquidity (widest coverage)</td></tr><tr><td>Position 3</td><td>15%</td><td>Mid-range support</td></tr><tr><td>Position 4</td><td>20%</td><td>Upper price range</td></tr><tr><td>Position 5</td><td>5%</td><td>Extended range coverage</td></tr></tbody></table>

#### Why 5 Positions?

* Better Price Discovery: Multiple positions create smoother price curves
* Reduced Slippage: More liquidity depth for traders
* Fee Optimization: Earn fees across different price ranges
* Market Resilience: Liquidity available at various price levels

## Deploy prompt

```
Deploy token DackieSwap, token symbol DACKIE
```

```
Deploy token Capminal, token symbol CAP, with pool fee is 3%
```

```
Deploy token DackieVerse, token symbol VERSE then initial buy 1 ETH
```

```
Deploy token Clanker, token symbol CLANKER, pool fee is 10%, with 10E market cap
```

## Fee Structure

{% hint style="warning" %}
Currently to prevent spaming, we will apply 0.0003E for each deployment, please be noticed!
{% endhint %}

With the Clanker V4 update, the Clanker Team now earns **0.2%** at the protocol level for all transactions. The generated swap fees will be distributed to the Capminal Team and Creator according to the rates in the table below.

<table><thead><tr><th width="139.05078125">#</th><th width="196.828125">% separated </th><th>Example: </th></tr></thead><tbody><tr><td></td><td>In 1% Trading Fee</td><td>If Swap Volume is $10,000 -> Trading Fee is $100</td></tr><tr><td>Creator</td><td><strong>80%</strong></td><td>Earn <strong>80$</strong></td></tr><tr><td>Capminal</td><td><strong>20%</strong></td><td>Earn <strong>20$</strong></td></tr></tbody></table>

