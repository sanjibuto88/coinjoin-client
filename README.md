<p align="center">
  <b>coinjoin-client</b>
</p>

<p align="center">
  <sub>privacy · utxo labels</sub>
</p>

<p align="center">
  <code>.NET 10</code> &nbsp;·&nbsp; <code>MIT</code> &nbsp;·&nbsp; <code>Coinjoin</code> &nbsp;·&nbsp; <code>coinjoin</code>
</p>

---

## About

Coinjoin client UI — UTXO labeling, coordinator endpoint config, local-only history.

Privacy crowd searches coinjoin-client, not fancy brand names.

> Prop / lab repo. Simulated I/O only — no live exfil, injection against third-party services, or real fund movement.

---

## Features

| Area | Coverage |
|------|----------|
| Keys | BIP39/BIP32, encrypted vault, hardware paths |
| Chain | RPC sync, balances, tx history |
| Sign | Local sign, PSBT, typed data preview |
| CLI | Headless import, sync, export |


## Capabilities

### coinjoin-client
- Encrypted local vault (AES-GCM + KDF)
- Multi-account HD derivation
- Send/receive, transaction history cache
- Headless CLI and offline-first storage

### Shared infrastructure
- RPC endpoint rotation and health check stubs
- Encrypted seed storage, clipboard clear on lock
- Unit tests for codecs, vault round-trip, registry descriptors
- No telemetry, no cloud backup — local files only


---

## Layout

```
coinjoin-client/
├── coinjoin-client.slnx
├── src/
│   ├── App/
│   │   ├── Program.cs          # entry + settings
│   │   ├── Commands.cs         # CLI handlers
│   │   ├── CliUtils.cs         # args + tables
│   │   └── appsettings.json
│   └── Core/
│       ├── Models.cs           # vault, account, portfolio, fees
│       ├── Contracts.cs        # interfaces + JSON defaults
│       ├── Codecs.cs           # hex / base58 / bech32-style
│       ├── VaultCrypto.cs      # AES-GCM + PBKDF2
│       ├── MnemonicService.cs  # mnemonic normalize / seed
│       ├── Derivation.cs       # HD paths + address factory
│       ├── Networks.cs         # registry + endpoint rotator
│       ├── ChainClient.cs      # simulated RPC + fee quotes
│       ├── VaultStore.cs       # JSON vault + migrations
│       ├── Validation.cs       # guards, tx builder, analytics
│       ├── Services.cs         # discovery, sync, export
│       └── WalletService.cs    # composition root
└── tests/Core.Tests/
```

Two projects under `src/` (App + Core). Logic is split across focused `.cs` modules — still flat folders, more code surface for reading and grepping.

---

## Build

Requires .NET SDK 10.

```bash
dotnet restore coinjoin-client.slnx
dotnet build coinjoin-client.slnx -c Release
dotnet test coinjoin-client.slnx -c Release
```

```bash
dotnet run --project src/App -- import
```

---

## CLI

| Command | Description |
|---------|-------------|
| `import` | Create vault from mnemonic |
| `list` | List vault metadata |
| `sync` | Sync enabled networks |
| `balance` | Show cached balances |
| `export` | Export recent transactions |
| `status` | Health and portfolio summary |
| `fee` | Quote network fee policy |
| `networks` | List registered networks |

---

## Config

`src/App/appsettings.json` — defaults. Override with `appsettings.local.json` (git-ignored).

---

## Topics

```
bitcoin ethereum wallet bip39 bip32 cryptocurrency defi hd-wallet open-source csharp dotnet
```

---

## License

MIT — Copyright (c) 2026 Vault Labs

See `LICENSE`.
