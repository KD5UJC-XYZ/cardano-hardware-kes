# Threat model (draft v0.1)

## Purpose

Make it materially harder for compromised hosts or malicious SPOs to retain, extract, or sell historical Cardano Sum6KES signing secrets. This is a voluntary security improvement, not a network-enforced guarantee.

## Attacker

Assume the attacker fully controls the block-producer machine, including root/kernel, filesystem, local services, and signing requests, and may be the SPO. They can connect to ordinary device interfaces and reset/power-cycle the appliance.

Assume they cannot invasively probe or modify silicon or defeat qualified hardware security mechanisms using laboratory-grade physical attacks.

## Trust boundary

Only the signer appliance's authenticated boot chain, device-local entropy, protected computation/memory, and protected state controls are trusted. The host, daemon, USB transport input, node, request period, storage and network are untrusted.

## Secret-key API

- **Generate:** Generate the complete Sum6KES secret inside the protected device.
- **Public key:** Return public key material only.
- **Sign:** Sign an exact provided message at an authorized current period.
- **Evolve:** Irreversibly move to a later KES period.

Public signature verification may run on the host. No production key import, export, plaintext/encrypted backup, restore, debug secret readout, or host-software signing fallback.

## Required properties

1. Secrets and seed material never enter host RAM.
2. Ordinary host root privileges cannot read device secret memory via memory mappings, DMA, debug, bootloader or update pathways.
3. A committed evolution makes retired periods permanently unsignable, including after reboot or external flash replay.
4. Power interruption yields either a valid current/advanced state or fail-closed key invalidation; never an acknowledged rollback.
5. Firmware authentication and debug closure must be validated on the actual hardware revision.
6. A compromised host may still request authorized signatures, evolve prematurely, or deny service; signing policy cannot eliminate all misuse.

## Out of scope

Invasive die probing, sophisticated side channels, lab fault injection, preventing an SPO from using another signer, and public proof of device use. Attestation/CIP proposals may be researched later.

## Open security questions

- Does the exact existing Red Pitaya Zynq model support a production-enforceable trusted boot and memory boundary?
- Can protected persistent state prevent replay without making insecure assumptions about flash?
- What firmware/signing policies should restrict requests without incorrectly claiming consensus-level safety?

This document is a proposed security contract, not evidence of qualified protection.
