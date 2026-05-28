<div align="center">

<h1>🔐 cwt.io</h1>
<p><strong>Browser-based CBOR Web Token (CWT) Debugger</strong></p>
<p>Decode, inspect, verify, and generate <a href="https://www.rfc-editor.org/rfc/rfc8392">RFC 8392</a> CBOR Web Tokens — right in your browser.<br/>The <a href="https://jwt.io">jwt.io</a> equivalent for the CWT/COSE ecosystem.</p>

<p>
  <img alt="License" src="https://img.shields.io/github/license/MarcosT96/cwt.io?style=flat-square"/>
  <img alt="Stars" src="https://img.shields.io/github/stars/MarcosT96/cwt.io?style=flat-square"/>
  <img alt="Issues" src="https://img.shields.io/github/issues/MarcosT96/cwt.io?style=flat-square"/>
  <img alt="PRs Welcome" src="https://img.shields.io/badge/PRs-welcome-brightgreen?style=flat-square"/>
</p>

</div>

---

## What is cwt.io?

**cwt.io** is an open-source, client-side debugger for [CBOR Web Tokens (CWT)](https://www.rfc-editor.org/rfc/rfc8392) — a compact, binary alternative to JWT defined in RFC 8392.

CWT is used in constrained environments like IoT devices, edge computing, and bandwidth-sensitive systems where JSON overhead is impractical. Despite being an IETF standard, there are almost no developer tools to easily inspect and debug CWT tokens. **cwt.io fills that gap.**

> **Nothing leaves your browser.** All decoding, verification, and generation happens client-side. No tokens are ever sent to a server.

---

## Features

- 🔍 **Decode** — Paste a CWT (hex or base64url) and instantly see the decoded CBOR header and payload
- ✅ **Verify** — Validate COSE signatures (HMAC, ES256, EdDSA) with a provided key
- ✏️ **Generate** — Build and sign CWT tokens from structured claim inputs
- 📋 **Claim Inspector** — Human-readable display of standard CWT claims (`iss`, `sub`, `aud`, `exp`, `nbf`, `iat`, `cti`)
- 🔒 **Security Warnings** — Highlights expired tokens, missing claims, and invalid signatures
- 🌙 **Dark / Light mode** — Full theme support
- ⚡ **Zero server** — 100% static, deployable anywhere

---

## Why CWT?

[CBOR Web Token (RFC 8392)](https://www.rfc-editor.org/rfc/rfc8392) uses [CBOR](https://www.rfc-editor.org/rfc/rfc7049) for binary encoding and [COSE (RFC 9052)](https://www.rfc-editor.org/rfc/rfc9052) for signing and encryption — producing tokens significantly smaller than JWT. This makes CWT ideal for:

| Use case | Why CWT fits |
|---|---|
| IoT / embedded devices | Smaller payloads, faster parsing, low memory footprint |
| Edge computing | Compact tokens reduce transmission overhead |
| Constrained networks | Binary encoding vs JSON text overhead |
| mDL / digital identity | ISO 18013-5 (mobile driver's license) uses COSE/CWT structures |
| EUDI Wallet (EU) | European Digital Identity Wallet uses CWT-compatible formats |

---

## JWT vs CWT at a glance

| | JWT | CWT |
|---|---|---|
| **RFC** | RFC 7519 | RFC 8392 |
| **Encoding** | JSON (text) | CBOR (binary) |
| **Signing** | JWS (RFC 7515) | COSE (RFC 9052) |
| **Size** | ~200–500 bytes typical | ~50–150 bytes typical |
| **Human readable** | ✅ | ❌ (requires decoder) |
| **Ideal for** | Web APIs, web auth | IoT, edge, constrained devices |
| **Claim keys** | Strings | Integers (more compact) |

---

## Getting Started

### Use online

Visit **[cwt.io](https://marcost96.github.io/cwt.io)** *(coming soon)*

### Run locally

```bash
git clone https://github.com/MarcosT96/cwt.io.git
cd cwt.io
# Open index.html in your browser — no build step required
open index.html
```

### Development

```bash
npm install
npm run dev
```

---

## CWT Claim Reference

Standard claims defined in [RFC 8392 §3.1](https://www.rfc-editor.org/rfc/rfc8392#section-3.1):

| Claim key | Integer key | Type | Description |
|---|---|---|---|
| `iss` | `1` | text string | Issuer |
| `sub` | `2` | text string | Subject |
| `aud` | `3` | text string | Audience |
| `exp` | `4` | integer | Expiration time (NumericDate) |
| `nbf` | `5` | integer | Not before (NumericDate) |
| `iat` | `6` | integer | Issued at (NumericDate) |
| `cti` | `7` | byte string | CWT ID (equivalent of JWT `jti`) |

---

## Supported Algorithms

| Algorithm | COSE label | Notes |
|---|---|---|
| HMAC-SHA256 | `5` (HS256) | Symmetric, shared secret |
| HMAC-SHA384 | `6` (HS384) | Symmetric |
| HMAC-SHA512 | `7` (HS512) | Symmetric |
| ES256 | `-7` | ECDSA P-256, most common asymmetric |
| ES384 | `-35` | ECDSA P-384 |
| ES512 | `-36` | ECDSA P-521 |
| EdDSA | `-8` | Ed25519 — compact and fast |

---

## Roadmap

- [ ] Decode and display CWT tokens (hex / base64url input)
- [ ] Human-readable claim rendering
- [ ] Signature verification (HS256, ES256, EdDSA)
- [ ] Token generation / signing UI
- [ ] Share token via URL (encoded, no server)
- [ ] COSE_Sign1 and COSE_Encrypt0 structure visualization
- [ ] RFC 9597: CWT Claims in COSE Headers support
- [ ] Library mode (npm package)
- [ ] CLI tool

---

## Relevant RFCs

| RFC | Title |
|---|---|
| [RFC 8392](https://www.rfc-editor.org/rfc/rfc8392) | CBOR Web Token (CWT) |
| [RFC 9052](https://www.rfc-editor.org/rfc/rfc9052) | CBOR Object Signing and Encryption (COSE) |
| [RFC 9053](https://www.rfc-editor.org/rfc/rfc9053) | COSE: Initial Algorithms |
| [RFC 7049](https://www.rfc-editor.org/rfc/rfc7049) | CBOR — Concise Binary Object Representation |
| [RFC 8747](https://www.rfc-editor.org/rfc/rfc8747) | Proof-of-Possession Key Semantics for CWT |
| [RFC 9597](https://www.rfc-editor.org/rfc/rfc9597) | CWT Claims in COSE Headers |

---

## Contributing

Contributions are very welcome! This project is in early development — the best time to get involved.

1. Fork the repository
2. Create a feature branch (`git checkout -b feat/my-feature`)
3. Commit your changes (`git commit -m 'feat: add my feature'`)
4. Push to the branch (`git push origin feat/my-feature`)
5. Open a Pull Request

Please read [CONTRIBUTING.md](./CONTRIBUTING.md) before submitting *(coming soon)*.

---

## License

MIT © [Marcos Tomassi](https://github.com/MarcosT96)

---

<div align="center">
  <sub>Inspired by <a href="https://jwt.io">jwt.io</a> · Built for the CWT/COSE ecosystem · RFC 8392</sub>
</div>
