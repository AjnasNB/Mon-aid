# MonadRelief (Mon-Aid)

A real-time micro-donation platform for disaster relief built on Monad L1.

## Repos
- `blockchain/`: Hardhat workspace with `MonadRelief` smart contract
- `backend/`: TypeScript Express API + WebSocket for live stats
- `frontend/`: Next.js + Tailwind UI
- `docs/blueprint.md`: Architecture blueprint and case study

## What is Mon-Aid?
Mon-Aid is a real-time disaster-relief donation platform built on the Monad blockchain. It enables micro-donations from $0.01 with under-1s finality, routing funds only to wallets verified by a government SBT registry and a community jury. Donations and disbursements are fully on-chain and transparent.

### Why Monad
- Parallel execution handles crisis surges (10k+ TPS)
- Ultra-low fees make penny donations viable
- Instant finality means victims can use funds immediately
- Immutable transparency builds trust

### Pitch (Story)
In 2022, Assam floods stranded millions. Rina, a mother of two, waited three days on a rooftop. International pledges took weeks to arrive. Imagine if people could have sent $1 instantly to her phone wallet while she was stranded — usable in seconds for food or a bus ticket.

Mon-Aid makes this possible: micro-donations processed in under a second on Monad, going directly to verified victims and NGOs, with government + community validation to prevent fraud.

With Monad’s power, we’re building a future where no mother like Rina waits days for help. She can get it in seconds.

### UI Concepts
Below are concept images included in `/frontend/public` that illustrate the brand and dashboards:
- `ui1.png`, `ui5.png` (primary)
- `ui2.png`, `ui3.png`, `ui4.png` (additional)
Open the in-app page `/pitch` to view embedded concepts.

## Prereqs
- Node.js 18+
- pnpm/yarn/npm
- A Monad-compatible RPC (configure `MONAD_RPC`), or local EVM RPC for dev

## Setup

### 1) Blockchain
```bash
cd blockchain
npm install
npm run build
# start a local node if needed (e.g. anvil/hardhat node) and set MONAD_RPC
npm run deploy
```
On Monad testnet, deployed addresses:
- GovernmentRegistry: `0x7154b061045a03b9fF86C83c606c64afC790791b`
- JuryStaking: `0xf91DCe7082D1721563C69b56b82d051bC55A332b`
- BeneficiaryRegistry: `0xDb22ba96790144c5dE4FAfb06690d73BB6B551d1`
- MonadReliefV2 (native): `0xa6FfdFaB1134E7B5C2864732576AfA3b4320a47d`
- MockUSD (test token): `0x7C57F3DdcDF82C97eBE70c4f4FDf2Bc6Ea910629`
- MonadReliefERC20 (stablecoin path): `0x1AD44BAa0897D0C22CCb20098477D635FAb271d7`

Use `MonadReliefV2` for `RELIEF_CONTRACT_ADDRESS` and `BeneficiaryRegistry` for `BENEFICIARY_REGISTRY_ADDRESS` in the backend.

### 2) Backend
```bash
cd backend
npm install
# Create environment
# PORT=4000
# MONAD_RPC=http://127.0.0.1:8545
# RELIEF_CONTRACT_ADDRESS=0xYourDeployedContract
# DEPLOYER_KEY=0xYourKeyIfNeeded
npm run dev
```
- REST: `GET /api/stats`
- WS: `ws://localhost:4000/ws` (broadcast live stats)

### 3) Frontend
```bash
cd frontend
npm install
# Set NEXT_PUBLIC_BACKEND_URL=http://localhost:4000 (via env or shell)
npm run dev
```
Open `http://localhost:3000`. Use the donation form and view live stats.

## Notes
- The MVP contract accepts native donations and instantly forwards to verified beneficiaries for transparent, on-chain disbursement.
- Add ERC20 stablecoin flows and FX guardrails as a next step.
- See `docs/blueprint.md` for governance, scaling, and case study details.


