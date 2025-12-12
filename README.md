# KeySpring Demo (Ika Cross-Chain Wallet Demo)

Create an Ethereum wallet from any browser wallet and send ETH on Base Sepolia — all non-custodially using Ika's distributed key generation.

---

> ⚠️ **Testnet Only — Developer Warning**
>
> This cross-chain wallet demo is provided for **developer testing and educational purposes only** and must be used on **Base Sepolia testnet only** (not mainnet).
>
> It has not been audited and may contain bugs or unexpected behavior. **Do not use it with real funds or production wallets.** Use only test keys and disposable testnet amounts.
>
> **You assume all risk by proceeding.**

---

## What This Demo Shows

This demo showcases how Ika enables **cross-chain wallet creation**. Using your existing wallet (MetaMask, Phantom, etc.), you can:

1. **Create a new Ethereum address** — derived through distributed key generation on the Ika network
2. **Send ETH transactions** — sign and broadcast to Base Sepolia testnet
3. **Stay non-custodial** — your secret share never leaves your browser

### The Magic

- Connect with a **Solana** wallet → get an **Ethereum** address
- Connect with **MetaMask** → get a **new, separate** Ethereum address
- Your existing wallet signs once to derive encryption keys, then Ika's DKG creates your new wallet

## Try It Out

### 1. Start the Backend

```bash
cd backend
bun install

# Set your Sui admin key
export SUI_ADMIN_SECRET_KEY="your-base64-encoded-key"

bun run dev
```

### 2. Start the Frontend

```bash
cd frontend
bun install
bun run dev
```

### 3. Use the Demo

1. Open `http://localhost:3000`
2. Connect your wallet (MetaMask, Phantom, etc.)
3. Click **"Create Wallet"** and sign the message
4. Wait for your new Ethereum address to be generated
5. Fund it with [Base Sepolia testnet ETH](https://www.alchemy.com/faucets/base-sepolia)
6. Send a transaction!

## How It Works

```
Your Wallet                    Ika Network                   Base Sepolia
    │                              │                              │
    │  1. Sign message             │                              │
    │─────────────────────────────▶│                              │
    │                              │                              │
    │  2. DKG creates dWallet      │                              │
    │◀─────────────────────────────│                              │
    │                              │                              │
    │  3. You get ETH address      │                              │
    │  (derived from dWallet)      │                              │
    │                              │                              │
    │  4. Sign tx locally          │                              │
    │  (secret never leaves)       │                              │
    │─────────────────────────────▶│                              │
    │                              │                              │
    │  5. Ika completes signature  │  6. Broadcast tx             │
    │                              │─────────────────────────────▶│
    │                              │                              │
    │  7. TX confirmed!            │◀─────────────────────────────│
    │◀─────────────────────────────│                              │
```

### Key Points

- **Non-custodial**: Your secret key share is computed in your browser and never sent to any server
- **Cross-chain**: Use any wallet to control an Ethereum address
- **Secure**: Based on Ika's [Zero-Trust dWallet](https://docs.ika.xyz/sdk/ika-transaction/zero-trust-dwallet) model

## Supported Wallets

| Wallet               | Type     | Works? |
| -------------------- | -------- | ------ |
| MetaMask             | Ethereum | ✅     |
| Phantom (Ethereum)   | Ethereum | ✅     |
| Phantom (Solana)     | Solana   | ✅     |
| Other Solana wallets | Solana   | ✅     |

## Configuration

### Backend Environment

| Variable               | Description                | Default   |
| ---------------------- | -------------------------- | --------- |
| `PORT`                 | Server port                | `3001`    |
| `SUI_ADMIN_SECRET_KEY` | Base64-encoded Ed25519 key | Required  |
| `SUI_NETWORK`          | `testnet` or `mainnet`     | `testnet` |

### Frontend Environment

| Variable              | Description | Default                 |
| --------------------- | ----------- | ----------------------- |
| `NEXT_PUBLIC_API_URL` | Backend URL | `http://localhost:5153` |

## Learn More

- [Ika Documentation](https://docs.ika.xyz)
- [Zero-Trust dWallet](https://docs.ika.xyz/sdk/ika-transaction/zero-trust-dwallet)
- [Get Base Sepolia ETH](https://www.alchemy.com/faucets/base-sepolia)
