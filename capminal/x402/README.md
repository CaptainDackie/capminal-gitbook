---
description: Capminal x402 Overview
cover: ../../.gitbook/assets/capminal_x402.png
coverY: 0
---

# x402

Pay-as-you-go access to premium API features with onchain payments. x402 makes every request simple, transparent, and wallet‑native.

{% hint style="success" %}
### x402 V2 Upgrade

* As of December 17, 2025, we have upgraded our x402 APIs to version 2 (V2).&#x20;
* Backward compatibility is supported for clients using version 1 (V1), so existing integrations do not require any changes.&#x20;
* However, we strongly recommend upgrading to V2 to ensure better compatibility with future x402 API updates.
{% endhint %}

## What is x402?

x402 extends HTTP 402 Payment Required to gate API access with onchain micropayments. Your client first gets a 402 with payment instructions, completes a quick wallet payment, then retries the same request with a cryptographic proof in the `X-PAYMENT` header.

## Pricing

* Price: Depend on each API
* Network: **Base**
* Pricing can evolve; always trust the live 402 instructions returned by the API

## How it works

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. Call a protected endpoint (e.g., `/x402/research`) without `X-PAYMENT`.
2. Receive `402 Payment Required` with live payment instructions (price, network, recipient, time window, etc.).
3. Pay using a compatible wallet/client.
4. Retry the exact same request with `X-PAYMENT: <payment-proof>`.
5. We verify onchain proof, s and return `200 OK` with the result.

## Header

* `X-PAYMENT`: Cryptographic proof of payment sent on retry.

## Under the hood

* Standardized 402 responses include machine‑readable payment requirements
* Secure, server‑side verification of the `X-PAYMENT` proof.&#x20;
* Settlement on Base mainnet in USDC for low fees and speed

{% hint style="success" %}
We are using Coinbase CDP's x402 facilitator to verify partner transactions, read detail [**HERE**](https://docs.cdp.coinbase.com/x402/welcome)
{% endhint %}

## Where it’s used

**x402 API host endpoint:**  `https://www.capminal.ai/api/x402/`

1. `GET ${host}/research` — Token research with AI deep search analysis (x402‑protected).
2. T.B.U (we will release soon)
3. T.B.U (we will release soon)

## Quick start for partners

* Build a two‑step client: handle 402 → pay → retry with `X-PAYMENT`
* Show a wallet deep link or QR to streamline checkout
* Keep the original request inputs identical on retry

Following Coinbase Docs:

{% embed url="https://docs.cdp.coinbase.com/x402/quickstart-for-buyers" %}

## Status codes at a glance

* `200 OK`: Payment verified and request processed
* `402 Payment Required`: Missing/invalid payment or not yet paid
* `400 Bad Request`: Invalid inputs
* `500 Internal Server Error`: Something went wrong server‑side

## Security & reliability

* Proofs are verified server‑side against onchain intent
* No long‑lived secrets required for protected endpoints
* Payments settle on a reliable L2 (Base) with predictable fees

## Integration tips

* Handle the 402 → pay → retry loop seamlessly in your UI
* Cache user inputs between the two calls
* Show clear progress states during payment and verification
