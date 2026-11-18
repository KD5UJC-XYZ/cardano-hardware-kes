# Cardano Hardware KES

Hardware-isolated, forward-secure Cardano Sum6KES signing with **device-generated, non-exportable secrets** and local-only access.

## Purpose

Develop a low-cost signing appliance that makes retaining or extracting historical KES keys significantly harder for a compromised host or malicious stake-pool operator. The signer supports generation, public-key retrieval, signing and irreversible evolution. Verification remains outside the device. No private-key import, export, backup or recovery is planned.

This is research and development, **not a qualified hardware security module**.

## Initial development hardware

- **Existing Red Pitaya:** Zynq FPGA isolation experiments, PS/PL performance, Curve25519 acceleration and secure-boot feasibility.
- **Existing ZimaBoard 832:** Untrusted Linux host, benchmark harness, daemon and Scarab integration.

No new hardware is required for initial work. Additional secure MCUs may be considered once benchmarks or funding justify them.

## Project documents

- [Threat model](docs/threat-model.md)
- [Hardware evaluation](docs/hardware-plan.md)
- [Benchmark plan](docs/benchmark-plan.md)

## Related implementations

- [AndrewWestberg/cardano-kes-forge](https://github.com/AndrewWestberg/cardano-kes-forge)
- [Scala Sum6KES implementation (dilf4s)](https://github.com/scasplte2/dilf4s/tree/unify/base)
- [Scarab Cardano node](https://github.com/KD5UJC-XYZ/scarab)

## License

Apache-2.0; see [LICENSE](LICENSE).
