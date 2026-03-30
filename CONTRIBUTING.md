# Contributing

This document covers everything you need to know before opening your first pull request.

---

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Local Setup](#local-setup)
3. [Branch Naming](#branch-naming)
4. [Commit Message Format](#commit-message-format)
5. [Running Tests](#running-tests)
6. [Submitting a PR](#submitting-a-pr)
7. [Code Style](#code-style)

---

## Prerequisites

Install the following tools before you begin.

| Tool                | Minimum version | Notes                                                                                               |
| ------------------- | --------------- | --------------------------------------------------------------------------------------------------- |
| Node.js             | 20.x            | Use [nvm](https://github.com/nvm-sh/nvm) or [fnm](https://github.com/Schniz/fnm) to manage versions |
| Rust toolchain      | stable          | Install via [rustup](https://rustup.rs/)                                                            |
| wasm32 target       | —               | `rustup target add wasm32-unknown-unknown`                                                          |
| Stellar CLI         | latest          | Install via `cargo install --locked stellar-cli`                                                    |
| Freighter extension | latest          | Browser wallet available at the [Freighter website](https://www.freighter.app/)                     |

Verify your setup:

```bash
node --version        # v20.x.x
rustup show           # active toolchain: stable
stellar --version
```

---

## Local Setup

### 1. Clone the repository

```bash
git clone https://github.com/walterthesmart/Stellar-Dex-Chat.git
cd Stellar-Dex-Chat
```

### 2. Configure environment variables

The frontend requires a `.env.local` file. Copy the example and fill in the values:

```bash
cp .env.example dex_with_fiat_frontend/.env.local
```

The required variables are defined in the README. Ensure you have your `GEMINI_API_KEY` and `PAYSTACK_SECRET_KEY` ready.

### 3. Install frontend dependencies

```bash
cd dex_with_fiat_frontend
npm install
```

### 4. Run the development server

```bash
npm run dev
```

The app is available at `http://localhost:3000`.

### 5. Build and test the Soroban contract

From the repository root:

```bash
cd stellar-contracts
cargo build --target wasm32-unknown-unknown --release
cargo test
```

If you use VS Code, install the `rust-lang.rust-analyzer` extension for contract diagnostics.

---

## Branch Naming

Use one of the following prefixes:

| Prefix     | When to use                |
| ---------- | -------------------------- |
| `feature/` | New functionality          |
| `fix/`     | Bug fixes                  |
| `docs/`    | Documentation-only changes |

Example: `feature/add-swap-confirmation-modal`

---

## Commit Message Format

This project follows [Conventional Commits](https://www.conventionalcommits.org/).

Example: `feat(swap): add slippage tolerance input`

---

## Running Tests

### Contract tests

```bash
cd stellar-contracts
cargo test
```

Update snapshots if contract logic changed:
```bash
cargo test -- --update-snapshots
```

### Frontend checks

```bash
cd dex_with_fiat_frontend
npm run build
npm run lint
```

---

## Submitting a PR

- [ ] PR description references the related issue: `Closes #ISSUE_NUMBER`
- [ ] `cargo test` and `cargo clippy` pass
- [ ] `npm run build` and `npm run lint` pass
- [ ] Snapshots are updated if necessary
- [ ] Screenshots included for UI changes

---

## Code Style

### Rust
Format with `rustfmt` and check with `clippy`:
```bash
cargo fmt
cargo clippy --all-targets --all-features -- -D warnings
```

### TypeScript
Format with Prettier and lint with ESLint:
```bash
npm run format
npm run lint
```

