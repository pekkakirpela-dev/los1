# What Does This Code Do?

## Overview

This is a **Solana Wallet Asset Transfer Tool** (also known as "Solana Money Mover") that automatically transfers all SOL and SPL tokens worth more than $5 from one Solana wallet to another in a single transaction.

## Primary Purpose

The tool is designed for **legitimate wallet management** purposes such as:
- Consolidating multiple wallets into one
- Migrating assets during wallet upgrades
- Emergency fund transfers
- Personal or business wallet reorganization

⚠️ **IMPORTANT**: This tool should ONLY be used with wallets you own or have explicit permission to access. Unauthorized use is illegal.

## How It Works

### Core Functionality

The application performs the following steps:

1. **Authentication**: Accepts a BS58-encoded private key to access the source wallet
2. **Asset Discovery**: Scans the wallet for all SOL balance and SPL token accounts
3. **Price Fetching**: Retrieves real-time USD prices for SOL and tokens from public APIs
4. **Value Calculation**: Computes the USD value of each asset
5. **Filtering**: Identifies only assets worth $5 or more
6. **Fee Management**: Automatically calculates and reserves SOL for transaction fees
7. **Transaction Building**: Creates a single transaction containing all asset transfers
8. **Execution**: Sends the transaction to the Solana blockchain

### Key Components

#### 1. **MoneyMover** (`src/moneyMover.ts`)
The main orchestrator that:
- Coordinates the entire transfer process
- Applies the $5 minimum value threshold
- Manages the transfer workflow
- Handles error cases

#### 2. **WalletService** (`src/walletService.ts`)
Handles all blockchain interactions:
- Connects to Solana RPC nodes
- Retrieves wallet balances and token accounts
- Estimates transaction fees
- Creates and signs transactions
- Sends transactions to the network

#### 3. **PriceService** (`src/priceService.ts`)
Manages token pricing:
- Fetches SOL price from CoinGecko or Binance
- Fetches SPL token prices from DexScreener
- Caches prices for 5 minutes to reduce API calls
- Handles known stablecoins (USDC, USDT)

#### 4. **CLI Interface** (`src/index.ts`)
Provides interactive command-line interface:
- Prompts for private key and destination wallet
- Displays wallet information
- Shows transfer preview
- Requests confirmation before executing

## Transaction Structure

A typical transaction includes:

1. **SOL Transfer** (if balance > $5 after fees)
   - Transfers native SOL to destination
   - Reserves enough SOL to cover all transaction fees

2. **SPL Token Transfers** (for each token worth > $5)
   - Creates associated token account at destination (if needed)
   - Transfers entire token balance
   - Processes all tokens in a single transaction

## Safety Features

### Fee Management
- Automatically calculates transaction fees based on:
  - Number of instructions (transfers)
  - Number of new accounts to create
  - Rent-exemption requirements
- Reserves 120% of estimated fees as safety buffer
- Prevents "insufficient funds" errors

### Value Filtering
- Only transfers assets worth $5 or more
- Ignores dust and worthless tokens
- Reduces transaction size and costs

### Error Prevention
- Validates wallet addresses
- Checks balance before transfer
- Handles network errors gracefully
- Provides detailed error messages

### User Confirmation
- Shows wallet information before transfer
- Displays estimated transfer details
- Requires explicit "yes" to proceed

## Usage Modes

### 1. Interactive CLI
```bash
npm run build  # Build the TypeScript code first
npm start      # Run the CLI
```
Prompts for all required information interactively.

### 2. Programmatic API
```typescript
const moneyMover = new MoneyMover(privateKey, rpcUrl);
const result = await moneyMover.transferAllAssets(destinationWallet);
```
Can be integrated into other applications.

### 3. Development Mode
```bash
npm run dev
```
Runs directly with TypeScript for development/testing.

## Technical Stack

- **Language**: TypeScript
- **Blockchain**: Solana
- **Libraries**:
  - `@solana/web3.js` - Solana blockchain interactions
  - `@solana/spl-token` - SPL token program
  - `axios` - HTTP requests for price APIs
  - `bs58` - Base58 encoding/decoding

## Real-World Example

If a wallet contains:
- 10 SOL (worth $1,000 at $100/SOL)
- 100 USDC (worth $100)
- 50,000 of TOKEN_A (worth $2)
- 1,000 of TOKEN_B (worth $50)

The tool will:
1. Transfer ~9.99 SOL (reserving ~0.01 for fees)
2. Transfer 100 USDC (value > $5)
3. Transfer 1,000 TOKEN_B (value > $5)
4. **Skip** TOKEN_A (value < $5)

All in a single transaction costing approximately 0.01 SOL in fees.

## Security Considerations

### What This Tool Does:
✅ Transfers assets from wallets you own  
✅ Consolidates your own wallets  
✅ Helps with legitimate wallet management  

### What This Tool Should NEVER Be Used For:
❌ Accessing wallets without permission  
❌ Stealing or draining others' assets  
❌ Any unauthorized or malicious activity  
❌ Any illegal purposes  

### Best Practices:
1. **Test first** with small amounts
2. **Verify** destination addresses carefully
3. **Keep** private keys secure
4. **Use** on a secure computer
5. **Never** share private keys

## API Endpoints Used

- **CoinGecko**: Free SOL price data
- **Binance**: Backup SOL price source
- **DexScreener**: SPL token price data
- **Solana RPC**: Blockchain data and transaction submission

## Output Information

After a successful transfer, you'll see:
- Transaction signature (for verification on block explorers)
- Total USD value transferred
- List of transferred items with individual values
- Solscan explorer link

## Limitations

- Requires internet connection
- Depends on external price APIs
- Subject to Solana network fees and congestion
- May not work with all exotic SPL tokens
- Price data may have slight delays

## Summary

This is a **legitimate wallet management tool** for transferring valuable assets between Solana wallets you control. It automates the complex process of identifying, valuing, and transferring multiple assets in a single efficient transaction while managing fees appropriately.
