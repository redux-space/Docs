
# AstraPort

AstraPort is a modular, open-source DeFi portfolio platform built on Stellar. It combines a user-facing DApp, a server-side API, and on-chain smart contracts to provide wallet integrations, portfolio visualizations, analytics, and protocol features (staking, swaps, rewards). AstraPort is designed for transparency, extensibility, and community contribution.

This README gives a high-level public overview of the AstraPort project and how the repositories in the redux-space organization connect. It's intended for visitors, potential contributors, and reviewers.

---

## Repositories and responsibilities

- redux-space/astraport-dapp (this repository)
  - Frontend user interface built in TypeScript.
  - Connects to Stellar-compatible wallets, displays portfolio, charts, and AI-driven insights.
  - Hosts public docs, UI components, and examples for integrating with the API and contracts.
  - Live demo / deployment instructions reside in the /docs or GitHub Pages (if available).
  - URL: https://github.com/redux-space/astraport-dapp

- redux-space/atraport-api
  - Backend API for indexing on-chain data, serving portfolio aggregation, analytics, and authenticated endpoints used by the DApp.
  - Responsible for caching, rate-limiting, and aggregation of multi-account views.
  - URL: https://github.com/redux-space/atraport-api

- redux-space/astraport-contracts
  - On-chain contracts (Rust) implementing protocol-level features: staking, rewards, and core financial primitives.
  - Contracts are designed to be verifiable and audit-friendly.
  - URL: https://github.com/redux-space/astraport-contracts

---

## Public-facing feature summary

- Wallet integrations: Connect Stellar wallets (SEP-10, direct anchor integrations) to authenticate and fetch balances.
- Portfolio aggregation: Consolidate balances, transaction history, and performance across accounts.
- On-chain interactions: Read and, where applicable, submit transactions to interact with AstraPort contracts (staking, swaps, rewards).
- Analytics & insights: Asset allocation, historical P&L, and AI-assisted recommendations (client-side inference or API-powered).
- Notifications & alerts: Event-driven user alerts for large balance changes, staking rewards, or governance events.
- Developer tools: Component library, API reference, contract ABIs/IDL, and local testing scripts.

---

## Architecture overview

High-level component flow (public view):

  +------------+        +-------------+         +--------------------+
  | User Wallet| <----> | AstraPort   | <-----> | AstraPort Contracts|
  | (Stellar)  |        | DApp (UI)   |         | (on-chain, Rust)   |
  +------------+        +-------------+         +--------------------+
                             ^   |
                             |   v
                        +---------+   +-------------+
                        | API     |   | Indexer /   |
                        | (atraport-api) |  Caching    |
                        +---------+   +-------------+

- DApp (astraport-dapp) connects directly to user wallets for signing and can call the API for aggregated views and off-chain features.
- API (atraport-api) indexes events from the chain, caches aggregated data, and exposes endpoints the UI uses for charts, analytics, and recommendations.
- Contracts (astraport-contracts) hold protocol logic. The API may read contract state and emit events used by the DApp.

Security & trust notes:
- Wallet signatures are performed in the user's wallet; private keys never leave the client.
- Contracts are authored in Rust and intended to be auditable; audits are encouraged and welcome.
- API endpoints should be treated as public indexers — sensitive write operations require authenticated wallet signatures.

---

## Quickstart (developer view)

Prerequisites: Node.js (LTS), yarn or npm, Rust (for contracts), and Docker (optional for local chain/indexer).

1. Clone this repo and the supporting repos:

   git clone https://github.com/redux-space/astraport-dapp.git
   git clone https://github.com/redux-space/atraport-api.git
   git clone https://github.com/redux-space/astraport-contracts.git

2. Local dev (frontend):

   cd asport-dapp
   npm install
   npm run dev

3. Run API (see atraport-api README for instructions). For quick local runs, use Docker Compose if provided.

4. Contracts:
   - Build and run unit tests in the contracts repo (see its README for Rust toolchain steps).

See each repository's README for full run and test instructions. This repository links to those docs in the docs/ directory.

---

## Contribution & review guidance (open-source)

We're grateful for contributions. Typical ways to contribute:
- Open issues for feature requests or bugs.
- Submit PRs against the default branch (main). Follow the repository's contribution checklist and include tests where applicable.
- Review contracts carefully — create issues for security concerns.

Suggested review focus areas:
- UI: accessibility, responsiveness, and wallet UX.
- API: correctness of aggregation, caching, and rate limiting.
- Contracts: correctness, invariants, and gas/fee analysis.

Code of conduct: Please follow an inclusive, respectful Code of Conduct in all interactions. If you need one, we recommend adopting the Contributor Covenant.

License: Each repo contains its own license file. If you want a single org-wide license, add or update the LICENSE file in the corresponding repositories.

---

## Public links & resources

- DApp (this repo): https://github.com/redux-space/astraport-dapp
- API: https://github.com/redux-space/atraport-api
- Contracts: https://github.com/redux-space/astraport-contracts

---

## Contact

For project-level questions, open an issue in this repository or reach out to the maintainers via GitHub discussions or the listed maintainer contacts in repo settings.

---

Thank you for checking out AstraPort. We welcome feedback, PRs, and security reports.
