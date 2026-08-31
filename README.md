# Nova Market

[![CI/CD Pipeline](https://img.shields.io/github/actions/workflow/status/Himanshu-engineer/NovaMarket/ci.yml?branch=main&label=CI%2FCD%20Pipeline&logo=githubactions&logoColor=white)](https://github.com/Himanshu-engineer/NovaMarket/actions/workflows/ci.yml)
[![Stellar](https://img.shields.io/badge/Stellar-Soroban%20Smart%20Contracts-7B36D9?logo=stellar&logoColor=white)](https://stellar.expert/explorer/testnet/contract/CAPTI5FMEUCVNH44T7UVRQDLMLA44FVXY4R36IZRAWQU6VLLGRQUVKTP)
[![Rust](https://img.shields.io/badge/Rust-soroban--sdk%2025-DEA584?logo=rust&logoColor=black)](contract/contracts/contract/src/lib.rs)
[![Next.js](https://img.shields.io/badge/Next.js-16%20(App%20Router)-black?logo=nextdotjs&logoColor=white)](https://nextjs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org)
[![React](https://img.shields.io/badge/React-19-61DAFB?logo=react&logoColor=black)](https://react.dev)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind%20CSS-v4-38BDF8?logo=tailwindcss&logoColor=white)](https://tailwindcss.com)
[![Bun](https://img.shields.io/badge/Bun-runtime-FBF0DF?logo=bun&logoColor=black)](https://bun.sh)
[![Stellar SDK](https://img.shields.io/badge/%40stellar%2Fstellar--sdk-17-FDDA24?logo=stellar&logoColor=black)](https://www.npmjs.com/package/@stellar/stellar-sdk)
[![Wallets](https://img.shields.io/badge/StellarWalletsKit-Freighter%20%C2%B7%20xBull%20%C2%B7%20Albedo%20%2B%20more-6E56CF)](https://stellarwalletskit.dev)
[![TanStack Query](https://img.shields.io/badge/TanStack%20Query-v5-FF4154?logo=reactquery&logoColor=white)](https://tanstack.com/query)
[![Zustand](https://img.shields.io/badge/Zustand-state-443E38?logo=react&logoColor=white)](https://zustand.docs.pmnd.rs)
[![Deployed on Vercel](https://img.shields.io/badge/Deployed%20on-Vercel-black?logo=vercel)](https://nova-marketdapp.vercel.app/)
[![License](https://img.shields.io/badge/License-MIT-97CA00)](LICENSE)

**Mint. List. Bid. Offer. Trade.** A full-stack NFT marketplace built on Stellar/Soroban with **fixed-price listings**, **English auctions**, **escrowed offers**, and **creator royalties enforced at the smart-contract level**. Every sale path — purchases, auctions, and accepted offers — distributes royalties atomically. No one can bypass them.

| | |
|---|---|
| 🔗 **Live link** | [nova-marketdapp.vercel.app](https://nova-marketdapp.vercel.app/) |
| 📜 **Stellar smart contract (Testnet)** | [`CAPTI5FMEUCVNH44T7UVRQDLMLA44FVXY4R36IZRAWQU6VLLGRQUVKTP`](https://stellar.expert/explorer/testnet/contract/CAPTI5FMEUCVNH44T7UVRQDLMLA44FVXY4R36IZRAWQU6VLLGRQUVKTP) |
| 🧾 **Deploy Transaction** | [`523b1e1fbc4618f8594a1cafe8b40187a6e766ff0e3b755382f4f5481c7df083`](https://stellar.expert/explorer/testnet/tx/523b1e1fbc4618f8594a1cafe8b40187a6e766ff0e3b755382f4f5481c7df083) |
| 👨‍💻 **Developed by** | [@Himanshu-engineer](https://github.com/Himanshu-engineer) |
| 🎬 **Demo Intro Video** | [Watch on Google Drive](https://drive.google.com/file/d/1v5eVxMbYF6-UDfznE3xQZHyBXOVfEkRO/view) |

## Overview

Nova Market replaces centralized NFT marketplace trust with **on-chain enforcement**. Creators mint NFTs with a royalty percentage baked into the token — and the Soroban contract enforces that royalty on every single sale, no matter the path:

```
                 ┌──────────────┐
                 │   NFT Sale   │
                 └──────┬───────┘
                        │
              ┌─────────▼─────────┐
              │ Soroban Contract  │
              └─────────┬─────────┘
                        │
                 Calculate royalty
                        │
              ┌─────────┴─────────┐
              │                   │
       Creator royalty       Seller proceeds
              │                   │
              └─────────┬─────────┘
                        │
                  Atomic payout
```

Royalties aren't a frontend convention you can skip — they're computed and distributed inside the contract on every transfer of funds.

### The three sale paths

| Path | How it works | Royalty enforced? |
|---|---|---|
| **Fixed-price listing** | Seller lists at a price → buyer purchases → contract splits payment atomically between creator and seller | ✅ Yes |
| **English auction** | Seller creates a time-boxed auction → bidders place escrowed bids → outbid refunds are instant → anyone settles after deadline → proceeds split atomically | ✅ Yes |
| **Escrowed offers** | Buyer makes an XLM-escrowed offer on any NFT → owner accepts → contract transfers NFT and splits payment atomically | ✅ Yes |

## Features

- **NFT Minting** — mint NFTs with a name, metadata URI, and creator royalty (0–50%). Royalties are permanently stored with the NFT and enforced by the contract.
- **Fixed-Price Listings** — list NFTs for a fixed XLM price. Cancel anytime. Purchases atomically transfer the NFT and split payment between seller and creator.
- **English Auctions** — create time-boxed ascending auctions. Bids are escrowed in the contract. Previous highest bidders are refunded immediately when outbid. NFTs are locked while an auction is active. Anyone can settle an expired auction.
- **Escrowed Offers** — anyone can make an offer on an NFT they don't own. Offers are escrowed in XLM. Buyers can raise or cancel offers. NFT owners can accept — royalties enforced on acceptance.
- **Enforced Creator Royalties** — royalties cannot be bypassed through any marketplace flow. Every completed sale distributes the royalty atomically inside the contract.
- **On-Chain Sales History** — every completed sale is recorded on-chain. Query sales history with `get_sales`. Read NFTs, listings, auctions, and offers directly from the contract.
- **Multi-Wallet Support** — powered by StellarWalletsKit. Supports Freighter, xBull, Albedo, and other compatible Stellar wallets through a single connect modal.
- **Real-Time Event Feed** — polls Soroban RPC `getEvents` for mints, listings, bids, sales, and other marketplace activity. No backend or indexer required.
- **Transaction Tracking** — transaction status feedback with links to Stellar Expert for on-chain verification.
- **Dark Mode & Responsive UI** — built with shadcn/ui components, fully responsive across devices.

## Architecture

Nova Market draws a clear line between what's trustless and what's convenience:

| Concern | Where it lives | Why |
|---|---|---|
| NFT ownership, royalties, listings, auctions, offers, sales | **On-chain** (Soroban contract, persistent storage) | Ownership and payments must be verifiable and atomic |
| Payment splitting & royalty calculation | **On-chain** (computed inside every sale path) | Royalties you can skip are worthless |
| Global config (admin, payment token, counters) | **On-chain** (instance storage) | Small, fixed-size, loaded with every call |
| UI rendering, event polling, wallet interaction | **Off-chain** (Next.js frontend) | Presentation layer doesn't need chain storage |

The frontend talks to the chain two ways: **reads** are free simulations against Soroban RPC (the marketplace works before you connect a wallet), and **writes** build a transaction, simulate it, get it signed by the connected wallet, submit it, and poll until confirmed.

## Tech Stack

| Layer | Choice |
|---|---|
| Framework | Next.js 16 (App Router) + TypeScript |
| Styling | Tailwind CSS v4 + shadcn/ui (Radix primitives) |
| Wallets | `@creit.tech/stellar-wallets-kit` |
| Chain | `soroban-sdk` 25 (Rust) + `@stellar/stellar-sdk` 17 (JS) |
| Server state | TanStack Query v5 (polling reads, mutation lifecycle) |
| Client state | Zustand (wallet session, transaction tracker) |
| Package manager | Bun |
| Blockchain | Stellar Testnet (Soroban) |

## Project Structure

```
NovaMarket/
├── client/                         # Next.js frontend
│   └── src/
│       ├── app/                    # Next.js App Router pages
│       │   └── (dapp)/             # Marketplace, auctions, dashboard, etc.
│       ├── components/             # UI components (NFT grid, auction panel, etc.)
│       ├── hooks/                  # Data & wallet hooks (useContractData, useWallet, etc.)
│       ├── lib/                    # Stellar/Soroban helpers, config, event polling
│       ├── stores/                 # Zustand stores (wallet, transactions)
│       └── types/                  # Shared TypeScript types
│
├── contract/                       # Soroban workspace
│   └── contracts/
│       └── contract/
│           └── src/
│               ├── lib.rs          # NFT marketplace contract (~760 lines)
│               └── test.rs         # 17 contract tests
│
└── scripts/
    ├── deploy.ps1                  # Windows deployment
    └── deploy.sh                   # macOS/Linux deployment
```

## Smart Contract Design

`contract/contracts/contract/src/lib.rs` implements a complete NFT marketplace:

### Write Methods

| Method | Purpose |
|---|---|
| `mint` | Mint an NFT with name, URI, and royalty (0–50%) |
| `list_fixed` | Create a fixed-price listing |
| `cancel_listing` | Remove a listing |
| `buy` | Purchase a listed NFT (royalty split atomic) |
| `create_auction` | Start a time-boxed English auction |
| `place_bid` | Place an escrowed bid on an auction |
| `cancel_auction` | Cancel an auction with no bids |
| `settle_auction` | Settle an expired auction (royalty split atomic) |
| `make_offer` | Make an escrowed XLM offer on any NFT |
| `cancel_offer` | Cancel and refund an offer |
| `accept_offer` | Accept an offer (royalty split atomic) |

### Read Methods

| Method | Purpose |
|---|---|
| `get_nft` | Retrieve a specific NFT |
| `list_nfts` | List all NFTs |
| `get_listing` | Retrieve a fixed-price listing |
| `list_listings` | List active listings |
| `get_auction` | Retrieve an auction |
| `list_auctions` | List all auctions |
| `get_offers` | Retrieve offers for a token |
| `get_sales` | Retrieve completed sales history |
| `token_count` | Total NFTs minted |
| `auction_count` | Total auctions created |
| `payment_token` | The payment token address (XLM SAC) |

### Error Handling

Errors are a typed `Error` enum (16 variants — `TokenNotFound`, `NotOwner`, `InvalidAmount`, `InvalidRoyalty`, `AlreadyListed`, `NotListed`, `SelfPurchase`, `AuctionNotFound`, `AuctionActive`, `AuctionEnded`, `AuctionSettled`, `BidTooLow`, `SelfBid`, `OfferNotFound`, `TokenLocked`, `HasBids`) so the frontend can show specific, friendly messages instead of raw RPC errors.

Run the contract's 17 tests with:

```bash
cd contract && cargo test
```

## Setup

### 1. Prerequisites

- **Bun** or Node.js 20+
- **Rust** toolchain
- **Stellar CLI** (`stellar` command)
- A Stellar-compatible wallet (e.g. [Freighter](https://www.freighter.app/))

### 2. Install Rust & Soroban target

```bash
rustup target add wasm32v1-none
```

### 3. Install Stellar CLI

```bash
cargo install --locked stellar-cli
```

### 4. Install frontend dependencies

```bash
cd client
bun install
```

### 5. Environment variables

```bash
cp .env.example .env.local    # inside client/
```

| Variable | Description | Default |
|---|---|---|
| `NEXT_PUBLIC_CONTRACT_ID` | Deployed marketplace contract | `CAPTI5FMEUCVNH44T7UVRQDLMLA44FVXY4R36IZRAWQU6VLLGRQUVKTP` |
| `NEXT_PUBLIC_SOROBAN_RPC_URL` | Soroban RPC endpoint | `https://soroban-testnet.stellar.org` |
| `NEXT_PUBLIC_HORIZON_URL` | Horizon endpoint | `https://horizon-testnet.stellar.org` |
| `NEXT_PUBLIC_NATIVE_TOKEN_CONTRACT` | Native XLM SAC | `CDLZFC3SYJYDZT7K67VZ75HPJVIEUVNIXF47ZG2FB2RMQQVU2HHGCYSC` |

### 6. Wallet setup

Install the [Freighter wallet](https://www.freighter.app/) browser extension, switch to **Testnet**, and fund your account via [Friendbot](https://friendbot.stellar.org).

### 7. Local development

```bash
cd client && bun run dev
```

Visit `http://localhost:3000`. Connect a funded testnet wallet and start minting, listing, and trading NFTs.

## Contract Deployment

Deployment scripts are provided for both platforms:

```bash
# macOS / Linux
./scripts/deploy.sh

# Windows
.\scripts\deploy.ps1
```

The deployment process:

1. Verifies that the Stellar CLI is installed.
2. Builds the Soroban contract.
3. Creates and funds a `deployer` identity on Testnet if required.
4. Resolves the native XLM Stellar Asset Contract.
5. Deploys the marketplace contract with `__constructor(payment_token)`.
6. Prints the deployed contract ID and writes it to `client/.env.local`.

## CI/CD

Every push and pull request to `main` runs the GitHub Actions pipeline defined in [`.github/workflows/ci.yml`](.github/workflows/ci.yml):

| Job | Steps |
|---|---|
| **Frontend** | `bun install --frozen-lockfile` → `bun run lint` (ESLint) → `bun run typecheck` (tsc) → `bun run build` (Next.js production build) |
| **Contract** | Rust stable toolchain + cargo cache → `cargo test` (all 17 Soroban contract tests) |

Nothing lands on `main` broken — a lint error, type error, failed build, or failing contract test turns the pipeline red.

**Continuous deployment** is handled by Vercel's Git integration: every push to `main` that passes CI is automatically built and deployed to [nova-marketdapp.vercel.app](https://nova-marketdapp.vercel.app/). The smart contract deploys separately via `scripts/deploy.sh` — frontend deploys never touch the chain.

## Deploying to Vercel

1. Push this repo to GitHub and import it into [Vercel](https://vercel.com/new).
2. Set the project's **Root Directory** to `client`.
3. Add the four `NEXT_PUBLIC_*` environment variables.
4. Deploy. The contract lives on Stellar Testnet independently — redeploying the frontend never requires redeploying the contract.

## Real-Time Updates

- **Event feed** polls Soroban RPC `getEvents` against the deployed contract, decoding topics/values and merging new events into a Zustand store — the feed grows without refetching what it already has.
- **Marketplace data** (NFTs, listings, auctions, offers) polls contract state via TanStack Query with `refetchInterval`, so updates propagate to every open tab without manual refresh.
- **Transaction tracker** moves each submitted transaction through `pending → success | failed`, storing the hash and linking to `stellar.expert`.

## Payment Token

All marketplace payments use the **native XLM Stellar Asset Contract (SAC)**:

```
CDLZFC3SYJYDZT7K67VZ75HPJVIEUVNIXF47ZG2FB2RMQQVU2HHGCYSC
```

Supplied to the contract constructor during deployment via `__constructor(payment_token)`.

## Useful Links

| Resource | Link |
|---|---|
| Live App | [nova-marketdapp.vercel.app](https://nova-marketdapp.vercel.app/) |
| Contract on Explorer | [Stellar Expert](https://stellar.expert/explorer/testnet/contract/CAPTI5FMEUCVNH44T7UVRQDLMLA44FVXY4R36IZRAWQU6VLLGRQUVKTP) |
| Stellar | [stellar.org](https://stellar.org/) |
| Stellar Developers | [developers.stellar.org](https://developers.stellar.org/) |
| Freighter Wallet | [freighter.app](https://www.freighter.app/) |
| Friendbot (Testnet XLM) | [friendbot.stellar.org](https://friendbot.stellar.org) |

## License

MIT — built as a demonstration project for Soroban smart-contract + Next.js integration.

---

**Nova Market — Mint. List. Bid. Offer. Trade — with creator royalties enforced on-chain.**
