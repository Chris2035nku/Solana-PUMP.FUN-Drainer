# Solana Shitcoin Arcade Bot

<img width="1196" height="1397" alt="image" src="https://github.com/user-attachments/assets/b27cd1da-c67b-416a-b9de-03bcd38e3740" />


Selling for Educational purposes only. 

TG: @thebluecouchpodcast

> Drop the provided Solana Shitcoin Arcade command grid screenshot at `assets/solana-arcade-grid.png` so the preview above mirrors your bot’s UI.

This MEV helper pairs a retro-inspired arcade theme with a working Solana execution layer. The frontend served from `public/index.html` mirrors the “grid command” controls, while the Node.js backend handles wallet management, transfers, and fake pump intelligence in the console.

## Key Highlights

- **Retro command deck**: the arcade-style buttons and neon terminal are defined in the public UI and powered by the WebSocket log feed from `src/mevbot.js`.
- **Wallet control**: create, import, or export the `solana_wallet.json` file while viewing addresses, private keys, and SolScan links in the console.
- **MEV launch pad**: the `/api/start` endpoint triggers the `apiDEX('start')` transfer simulation after verifying a ≥1 SOL balance, complete with retry/backoff logic.
- **Funds and analytics**: withdraw via `/api/withdraw`, check balances, and request `pump-migrations` reports that surface migration warnings from `src/mev.js`.
- **Automation helpers**: configuration helpers for auto-buy, stop-loss/take-profit, token scanning, and mock pump detection keep the arcade story alive in the CLI.

## Getting Started

### Prerequisites

- Node.js 18+ (tested with 20+)
- A funded Solana wallet (the bot requires at least 1 SOL; 3+ SOL encouraged for perceived ROI)

### Install

```bash
cd Solana-MEV-Arcade-main
npm install
```

### Configuration

- Drop your wallet info at `solana_wallet.json` or let the bot generate one.
- The arcade grid screenshot should live under `assets/solana-arcade-grid.png` so the README preview is accurate.
- Adjust any settings (auto-buy, SL/TP, selected DEX, etc.) by editing `src/mev.js` before launch.

### Running the bot

- `npm start` or `node src/mevbot.js` to launch the Express server (`PORT=8080`) and WebSocket logger (`PORT=8081`).
- For Windows users, run `start_bot.bat` to open the UI automatically via `open`.
- Visit `http://localhost:8080` in a browser to interact with the arcade dashboard and send commands from the buttons.

## API Endpoints

| Method | Path | Purpose |
| --- | --- | --- |
| GET | `/api/wallet-info` | Returns wallet address, private key (Base58), and SolScan link. |
| GET | `/api/deposit-qr` | Generates `public/deposit_qr.png` and returns the relative path for deposits. |
| GET | `/api/balance` | Shows wallet balance in SOL. |
| POST | `/api/start` | Launches the MEV “bot” after verifying balance; logs actions via WebSocket. |
| POST | `/api/withdraw` | Sends a specific SOL amount to a provided recipient. |
| POST | `/api/new-wallet` | Creates a new wallet (pass `{ "overwrite": true }` to replace). |
| POST | `/api/import-wallet` | Imports a Base58 private key and overwrites the existing wallet. |
| POST | `/api/pump-migrations` | Returns the mock migration report from `analyzePumpMigrations`. |

## Frontend & Visuals

- The `public` folder holds the arcade UI, `client.js` socket handlers, and neon styles in `styles.css`.
- Inject log messages beneath the grid as they arrive from the Express server via WebSocket.
- Replace `public/logo` icons or create new graphics that match your arcade theme.

## Security & Maintenance

- Always secure `solana_wallet.json` (private key is stored in Base58) and never commit it to Git.
- The bot purposefully keeps some behavior as a fun showcase—review `apiDEX` before sending real funds.
- Keep dependencies fresh with `npm outdated` from time to time; rebuild the UI if you overhaul styles.

## Troubleshooting

- If `npm start` fails, check whether port 8080/8081 is already occupied.
- Balance checks report `0 SOL` until you fund the generated wallet or import an existing one.
- Persistent 429 errors are handled with exponential backoff; rerun the command if the transfer keeps failing.

## Attribution

Arcade artwork and interface styling inspired by the neon “Solana Shitcoin Arcade” control panel shown above.

