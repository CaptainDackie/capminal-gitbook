---
description: Easily to setup a Lucky Draw thread. (deprecated)
---

# Lucky Draw Feature

{% hint style="warning" %}
**NOTE:** The feature is temporarily disabled
{% endhint %}

This feature helps creators easily set up a Lucky Draw thread that asks participants to complete simple social tasks, then automatically selects winners at random and distributes rewards.

<figure><img src="../../.gitbook/assets/luckydraw001.png" alt="Lucky Draw Example Prompt"><figcaption><p>Lucky Draw Example Prompt</p></figcaption></figure>

## Required

Your Lucky Draw post should include the following information:

* Reward token symbol or address: If you only provide the token symbol, please ensure your token is listed on CoinGecko so Captain can retrieve the token address.
* Reward per person and total number of winners
* Required tasks (currently supported tasks are):
  * Follow (only following the creator, not a specific account)
  * Like
  * Retweet
  * Tag X friends **(must)**: currently we do **NOT** support tasks for participants to **comment their wallet address**, we just support distribute reward directly to participant's Capminal wallet.
* Duration or deadline: You can specify a duration (e.g., 1 hour, 1 day, 1 week) or set a specific deadline (e.g., 2025/12/31).

{% hint style="warning" %}
**IMPORTANT:** When you set up a Lucky Draw post, Captain will collect the total amount of tokens you intend to reward in advance to ensure there are enough tokens available for distribution to the winners. Please be aware of this process.
{% endhint %}

## Pre-condition

Both creator and participants must have Capminal account before create Lucky Draw post or participate in.

## Notes

### For lucky draw creators

1️⃣ You must have sufficient funds in your Capminal account because the system will take the reward from your wallet first before distributing it to participants.

2️⃣ If the time expires without any participants, the system will refund the lucky draw creator.

3️⃣ If the number of participants does not reach the maximum number of winners, participants will still receive rewards, and the remaining amount will be refunded to the lucky draw creator.

4️⃣ When lucky draw creator prompt the post, you should place the instruction at first to make sure Captain can read your full content, the remain content keep as next.

### For participants

1️⃣ Ensure you have a Capminal account before completing tasks and commenting.

2️⃣ Complete all tasks before commenting and tagging friends.

3️⃣ If you fail to complete the tasks before commenting, your entry will not be recorded (Captain will not notify to avoid spam).

4️⃣ Spam accounts may not record as entry.

5️⃣ You must need Captain confirm to the Lucky Draw post first, then comment later. If you command before Captain confirm, your entry cannot be recorded.

## Examples

> Lucky draw: 100$ ETH to 5 winners&#x20;
>
> \- Tag 3 friends, follow and like&#x20;
>
> \- Ends tomorrow

> Random giveaway: 1000 CAP each for 15 people&#x20;
>
> \- Retweet and tag 2 friends&#x20;
>
> \- Duration: 1 week

> Please init a random airdrop with below information&#x20;
>
> \- Reward 300 USDC each people&#x20;
>
> \- Like/retweet/tag 3 friends on this post&#x20;
>
> \- There are 10 lucky winners&#x20;
>
> \- Deadline: 2025/07/17

> Init random airdrop&#x20;
>
> \- 50 USDC per winner&#x20;
>
> \- Like and follow and tag 2 friends&#x20;
>
> \- 25 lucky winners&#x20;
>
> \- Deadline: December 31, 2025
