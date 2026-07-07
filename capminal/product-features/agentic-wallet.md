---
description: Secure your funds and give AI agents safe, API-based access to your CAP Wallet.
---

# Agentic Wallet

Capminal's **Agentic Wallet** combines CAP Wallet custody with API-based agent access. It lets users sign in, fund a wallet, and let trusted AI agents or external clients execute wallet, trading, and deployment operations without exposing a private key.

{% hint style="success" %}
**Agentic Wallet:** a wallet that can be used by agents to reason, plan, and execute transactions through controlled API access.
{% endhint %}

## Create Your CAP Wallet

Capminal integrates with [Privy.io](https://www.privy.io/) for social login. When you sign in with your social account, your CAP Wallet is created automatically.

After your wallet is created, you can deposit funds and start trading directly from Capminal.

<figure><img src="../../.gitbook/assets/Screenshot 2026-07-07 at 11.54.44.png" alt="Agentic Wallet screen"><figcaption></figcaption></figure>

## Secure Wallet Custody

Your CAP Wallet is a server wallet secured with [AWS KMS](https://aws.amazon.com/kms/). You do not need to manage a private key, seed phrase, or browser wallet extension.

This design keeps the signing key inside Capminal's wallet infrastructure. Users and agents interact with the wallet through Capminal, while the private key never needs to leave the secure custody layer.

Remember to set a **Backup Email** for your wallet. If you lose access to your social account, you can use the Backup Email to recover your wallet.

## Transfer And Withdraw Funds

You can withdraw or transfer funds by sending natural-language commands, such as:

* `Send all [token_address] to [your_main_wallet_address]`
* `Transfer all ETH to [your_main_wallet_address]`

<figure><img src="../../.gitbook/assets/Screenshot 2026-07-07 at 11.55.57.png" alt="Wallet API Key screen"><figcaption></figcaption></figure>

## Agent Access Through API Key

AI agents and external clients access your Agentic Wallet through a **Wallet API Key**, not a private key.

The Wallet API Key system allows users and builders to securely access CAP services through a standardized authentication mechanism. You can generate an API Key and import it into external clients such as OpenClaw or Hermes to execute wallet, trading, and deployment operations.

## Why API Keys Matter

API Keys are the access layer that turns CAP Wallet into an agentic wallet:

* The private key never leaves Capminal's wallet infrastructure.
* Agents authenticate with a rotatable API Key and ask Capminal to execute operations on their behalf.
* API Keys can be rotated or deleted when they are no longer needed or may be exposed.
* Builders can integrate wallet, trading, and deployment services without building wallet custody infrastructure from scratch.

{% hint style="danger" %}
**Important Security Notice:**

Your API Key grants access to execute trades and transfer funds from your CAP Wallet. If your API Key is compromised, unauthorized parties may drain your wallet. Store it securely and delete or rotate it immediately if it may have been exposed.
{% endhint %}

## Generate An API Key

1. Go to **Settings -> API Key**.
2. Click **Generate New Key**.
3. Copy and store the key securely.

The API Key is shown only once after creation.

## Manage API Keys

You can manage your keys in the dashboard:

* **Rotate Key:** generate a new key to replace the current one if it is compromised or exposed.
* **Delete Key:** permanently remove a key if it is no longer needed or has security issues.

Key rotation and deletion help keep your Agentic Wallet secure while still allowing trusted agents and clients to operate on your behalf.
