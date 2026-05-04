# Compact Standard Library — Verified Reference Examples

Companion code for the tutorial:
**[Compact Standard Library: A Verified Reference to Every Export](https://dev.to/iamharrie/compact-standard-library-a-verified-reference-to-every-export-10k5)**

Submitted for the [Midnight Eclipse Content Bounty Program](https://forum.midnight.network/t/midnight-content-bounty-program-eclipse/1148) — Issue [#293](https://github.com/midnightntwrk/contributor-hub/issues/293).

All contracts compiled and verified against **Compact compiler v0.30.0**.

---

## Files

| File | Exports Demonstrated | Status |
|---|---|---|
| `01-maybe.compact` | `Maybe<T>`, `none<T>()`, `some<T>()`, `.value` | ✅ |
| `02-either.compact` | `Either<L,R>`, `left<L,R>()`, `right<L,R>()`, `.left`, `.right` | ✅ |
| `03-counter.compact` | `Counter`, `.increment()`, `as Field` | ✅ |
| `04-persistent-hash.compact` | `persistentHash`, `pad` | ✅ |
| `05-persistent-commit.compact` | `persistentCommit` | ✅ |
| `06-kernel-types.compact` | `ZswapCoinPublicKey`, `ContractAddress`, `ownPublicKey`, `nativeToken`, `tokenType` | ✅ |
| `07-evolve-nonce.compact` | `evolveNonce`, `shieldedBurnAddress` | ✅ |

---

## Key Findings vs. Common Documentation

| Claim in other articles | Actual compiler behaviour (v0.30.0) |
|---|---|
| Use `CurvePoint` | Deprecated — compiler says use `JubjubPoint` |
| Use `Scalar` | Unbound identifier in v0.30.0 |
| `MerkleTree<N,T>` as ledger field | Compile error — store `Bytes<32>` root instead |
| `persistentCommit(tree, leaf)` | Signature is `(Bytes<32>, Bytes<32>)` — no MerkleTree arg |
| `evolveNonce(Bytes<32>, tag)` | First arg must be `Uint<128>`, not `Bytes<32>` |
| `tokenType(addr)` | Requires prefix: `tokenType(Bytes<32>, ContractAddress)` |
| `getBlockTime()` / `getEpoch()` | Not found in v0.30.0 |

---

## Reference

- [example-bboard](https://github.com/midnightntwrk/example-bboard) — canonical reference implementation
- [Midnight Docs](https://docs.midnight.network)
- [Midnight MCP toolchain](https://www.npmjs.com/package/midnight-mcp)
