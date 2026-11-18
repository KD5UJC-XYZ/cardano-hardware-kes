# KES benchmark plan (draft v0.1)

## Inputs and references

- [cardano-kes-forge](https://github.com/AndrewWestberg/cardano-kes-forge): inspect `kes-core/src/signing.rs`, firmware's signing path and per-stage performance instrumentation. Project latency goals are **not measured device performance**.
- [dilf4s, unify/base](https://github.com/scasplte2/dilf4s/tree/unify/base): Scala Sum6KES implementation for independent functional reference.
- Owned hardware: ZimaBoard 832 and Red Pitaya (exact board identity pending).

## Workloads

- Generate keys internally when testing the trusted target; for host-only exploratory baselines use disposable test keys.
- Public-key retrieval.
- Warm `sign` at periods 0, 1, 31, 32 and 63, using 0-, 256- and 4096-byte messages.
- All 63 evolution boundaries, notably 31→32.
- Attribute total latency to public-tree loading, authentication, flash/state commitment, bare Sum6KES `sign_into`, optional internal self-verification and local transport.
- Test interrupted evolution, stale requests and replayed external state independently of performance.
- Start with one pool before attempting synchronized 4/16/32-pool loads.

## Measurements

Record versioned raw results, commit SHA, compiler flags, board/silicon ID, CPU frequency, governor, firmware hash, memory peaks and measurement method. Report p50/p95/p99/max, timing distribution and CPU cycles when possible. Verify returned signatures with an independent implementation.

Separate cryptographic-only measurements from entire local signing round-trip and evolution paths. Never publish secret test vectors or expose live keys through test hooks.

## Initial engineering targets — unvalidated

- Warm local sign p99 <= 100 ms.
- Warm local sign p50 <= 25 ms (stretch).
- Period-boundary signs reported separately, with a target <= 500 ms.
- All stale-period signing rejected after acknowledged evolution.

No figure may be reported as achieved without actual hardware measurements. A failed measurement or unavailable environment is not a pass.
