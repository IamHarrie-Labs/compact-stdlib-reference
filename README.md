# Compact standard library — verified reference examples

Companion code for the tutorial:
**[Compact standard library: a verified reference to every export](https://dev.to/iamharrie/compact-standard-library-a-verified-reference-to-every-export-10k5)**

Submitted for the [Midnight Eclipse Content Bounty Program](https://forum.midnight.network/t/midnight-content-bounty-program-eclipse/1148) — Issue [#293](https://github.com/midnightntwrk/contributor-hub/issues/293).

All contracts compile against **Compact compiler v0.31.0** (language version 0.23). Compilation is verified on every push by [GitHub Actions](../../actions).

---

## Files

| File | Exports demonstrated | Status |
|---|---|---|
| `01-maybe.compact` | `Maybe<T>`, `none<T>()`, `some<T>()`, `.value` | ✅ |
| `02-either.compact` | `Either<L,R>`, `left<L,R>()`, `right<L,R>()`, `.left`, `.right` | ✅ |
| `03-counter.compact` | `Counter`, `.increment()`, `as Field` | ✅ |
| `04-persistent-hash.compact` | `persistentHash`, `pad` | ✅ |
| `05-persistent-commit.compact` | `persistentCommit` | ✅ |
| `06-kernel-types.compact` | `ZswapCoinPublicKey`, `ContractAddress`, `ownPublicKey`, `nativeToken`, `tokenType` | ✅ |
| `07-evolve-nonce.compact` | `evolveNonce`, `shieldedBurnAddress` | ✅ |
| `08-counter-decrement.compact` | `Counter.decrement()` (saturates at zero) | ✅ |
| `09-merkletree-ledger.compact` | `MerkleTree<N, T>` as ledger field with `.insert()` | ✅ |
| `10-ec-ops.compact` | `ecMulGenerator`, `ecAdd`, `ecMul` on `JubjubPoint` | ✅ |
| `11-block-time.compact` | `blockTimeLt`, `blockTimeLte`, `blockTimeGt`, `blockTimeGte` | ✅ |

---

## Key findings vs. common documentation

| Claim in other articles | Actual compiler behaviour (v0.31.0) |
|---|---|
| Use `CurvePoint` | Deprecated — compiler says use `JubjubPoint` |
| `JubjubPoint` is opaque, just use `persistentHash` | Opaque, but `ecAdd`, `ecMul`, `ecMulGenerator` operate on it |
| Use `Scalar` | Unbound identifier — use `Field` |
| `MerkleTree<N,T>` can't live in ledger | Works in v0.31.0 with `.insert()` |
| Counters can't be decremented | `.decrement(n)` exists, saturates at zero |
| `persistentCommit(tree, leaf)` | Signature is `(Bytes<32>, Bytes<32>)` — no MerkleTree arg |
| `evolveNonce(Bytes<32>, tag)` | First arg must be `Uint<128>`, not `Bytes<32>` |
| `tokenType(addr)` | Requires prefix: `tokenType(Bytes<32>, ContractAddress)` |
| `getBlockTime()` / `getEpoch()` | Unbound — use the `blockTime*` family |

---

## Reference

- [example-bboard](https://github.com/midnightntwrk/example-bboard) — canonical reference implementation
- [Midnight Docs](https://docs.midnight.network)
- [Midnight MCP toolchain](https://www.npmjs.com/package/midnight-mcp)
