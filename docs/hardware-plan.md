# Hardware evaluation plan

**Initial platforms are exclusively the already-owned Red Pitaya and ZimaBoard 832. No additional hardware purchase is required for the initial work.** Any secure MCU comparison is deferred until funding or data from these platforms justifies procurement.

## ZimaBoard 832

Run Linux host tooling and benchmark harness, compare native Rust/Scala KES implementations, measure local transport, and serve as the untrusted block-producer side of an eventual Scarab integration. A regular Linux process on ZimaBoard is *not* a non-extractable key vault.

## Red Pitaya

Identify exact board revision, Zynq silicon, RAM, flash, available debug interfaces, boot configuration, cryptographic isolation and FPGA resources before making security claims.

1. Benchmark software Sum6KES on Zynq Cortex-A9 cores.
2. Evaluate whether FPGA BRAM and programmable logic can own all key material without exposing it to PS/AXI/DMA/host memory.
3. Explore Curve25519 field arithmetic acceleration in RTL, beginning with simulation and reproducible synthesis.
4. Evaluate secure boot/bitstream authentication, provisioning, hardware entropy and powered-off state protection.
5. Implement local-only signing interface once isolation constraints are understood.

An FPGA bitstream and BRAM alone do **not** establish non-extractability. No real production key may be used before security qualification.

## Future candidates (not initial scope)

RP2350, STM32H5 and NXP LPC55-series secure MCUs may be compared after initial performance/security measurements; no funding-dependent purchases are assumed.

## Exit criteria

Reproducible performance baseline on owned boards; feasibility determination for hardware key isolation and state evolution; documented unresolved threats; Scarab adapter design.
