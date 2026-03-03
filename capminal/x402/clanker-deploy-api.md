---
description: Capminal x402 Flash Clanker Token Deployment API
---

# Clanker Deploy API

Deploy token very easily via API, no auth needed, no account needed, paid per request via x402. Designed for speed, clarity, and wallet‑native checkout.

{% hint style="success" %}
* Clanker tokens deployed via **Capminal x402 API** will be the same [**FEE STRUCTURE**](../product-features/token-deployment.md#fee-structure) as when you deploy on Capminal UI or using Captain Dackie on X.
* Clanker tokens deployed via **Capminal x402 API** will use Clanker V4.&#x20;
{% endhint %}

## Endpoint

* Host: `https://www.capminal.ai/api/x402`
* Method: `POST`
* Path: `/deploy`
* x402Version: 2

## Authentication (payment)

* This endpoint is protected by x402 micropayments.
* First call without `X-PAYMENT` → you’ll receive `402 Payment Required` with live payment instructions.
* Pay, then retry with `X-PAYMENT: <payment-proof>`.

## Pricing

* **$0.5** per successful request on **Base**
* Request body (JSON)
  * `chainId` (string, required): EVM chain id. Example: `8453` for Base
  * `name` (string, required): Token name
  * `symbol` (string, required): Token symbol
  * `description` (string, optional): Short token description
  * `imageUrl` (string, optional): URL to token image/logo. Use can use any public upload image website to upload your logo and get the url, png/jpeg is recommended.
  * `fee` (string, required): Percentage fee, e.g., `"1%"` to `"10%"`
  * `marketCap` (string, required): One of `"low"`, `"medium"`, `"high"` stand for 1E, 5E and 10E init marketcap
  * `ownerAddress` (string, required): ERC‑20 owner wallet, starts with `0x` + 40 hex chars

## Headers

* `Content-Type: application/json`
* `X-PAYMENT` (string, on retry): Cryptographic proof of payment

## Request/response

1. Initial request (expect 402):

```bash
curl -X POST \
  'https://www.capminal.ai/api/x402/clanker/deploy' \
  -H 'Content-Type: application/json' \
  -d '{
    "chainId": "8453",
    "name": "Capminal",
    "symbol": "CAP",
    "description": "Type to DeFAI",
    "imageUrl": "https://example.com/logo.png",
    "fee": "1%",
    "marketCap": "medium",
    "ownerAddress": "0x1234567890abcdef1234567890abcdef12345678"
  }'
```

Example 402 response (shape may include additional fields):

```json
{
  "success": false,
  "message": "Payment Required",
  "statusCode": 402,
  "paymentRequirements": {
    "scheme": "exact",
    "network": "base",
    "price": { "display": "$0.5", "amount": "500000", "currency": "USDC", "decimals": 6 },
    "resource": "hhttps://capminal.ai/api//x402/clanker/deploy",
    "maxTimeoutSeconds": 300,
    "extra": {
      "inputSchema": {
        "type": "object",
        "required": [
          "chainId",
          "name",
          "symbol",
          "fee",
          "marketCap",
          "ownerAddress"
        ]
      }
    }
  }
}
```

2. Retry with payment proof:

```bash
curl -X POST \
  'https://www.capminal.ai/api/x402/clanker/deploy' \
  -H 'Content-Type: application/json' \
  -H 'X-PAYMENT: <facilitator-payment-proof>' \
  -d '{
    "chainId": "8453",
    "name": "Capminal",
    "symbol": "CAP",
    "description": "Type to DeFAI",
    "imageUrl": "https://example.com/logo.png",
    "fee": "1%",
    "marketCap": "medium",
    "ownerAddress": "0x1234567890abcdef1234567890abcdef12345678"
  }'
```

Success (200) response:

```json
{
  "success": true,
  "message": "Token deployment initiated successfully",
  "data": {
    "token": {
      "name": "Capminal",
      "symbol": "CAP",
      "address": "0xabc...def",
      "ownerAddress": "0x1234567890abcdef1234567890abcdef12345678",
      "chainId": "8453",
      "fee": "1%",
      "marketCap": "medium",
      "imageUrl": "https://example.com/logo.png"
    },
    "transaction": {
      "txHash": "0xdeadbeef...",
      "explorerUrl": "https://basescan.org/tx/0xdeadbeef..."
    },
    "clanker": "https://www.clanker.world/clanker/0xabc...def"
  }
}
```

## Errors

* `400 Bad Request`: Missing/invalid body fields
* `402 Payment Required`: Missing/invalid payment or not yet paid
* `503 Service Unavailable`: Upstream services temporarily unavailable

## Tips

* Keep the request body identical between the first call and the retry
* Validate `ownerAddress` format and symbol constraints on your side for best UX
