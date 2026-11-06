<div align="center">
  <img src="https://raw.githubusercontent.com/superlexicon/.github/main/assets/header_banner.png" alt="SuperLexicon" width="100%" />

  <h3>Radio-Native Layer-1 Blockchain &amp; Decentralized Mesh Ecosystem</h3>
  <p>
    <strong>Zero Internet Dependency • 2.6 Mbps Semtech LR2021 FLRC • Deterministic TDMA-BFT Consensus • 5–6s Block Finality</strong>
  </p>
</div>

---

## Overview

**SuperLexicon** is an infrastructure-independent Layer-1 blockchain and decentralized application ecosystem built from the ground up to operate directly over **Sub-GHz (915 MHz) and 2.4 GHz radio spectrum** using the **Semtech LR2021** transceiver in **FLRC (Fast Long-Range Communication)** mode.

While traditional blockchains collapse when ISP backbones, submarine cables, BGP routing, or cloud data centers are disrupted or censored, **Lexicon** achieves **225–240 transactions per block** with **5.6-second finality** over pure peer-to-peer RF links—no fiber, no cell towers, and no internet required.

---

## Public Repositories

| Repository | Description | Target / Stack |
| :--- | :--- | :--- |
| **[`superlexicon`](https://github.com/superlexicon/superlexicon)** | **The Super-App** — Unified client & process supervisor featuring the **Blockchain & Network Dashboard** (live consensus metrics, RF link & subnet telemetry, validator/roamer/repeater control), **LexiChat** (on-chain mesh messaging), **LexiDEX** (peer-to-peer liquidity & swaps), **LexiWallet** (`secp256k1` / `Ed25519` vault), and **LexiApps** (`.wasm` dApp runtime). | Linux, macOS, Canaan K230 (`C11` / `C++20` / `LVGL` / `SDL2`) |
| **[`lexicon-hardware`](https://github.com/superlexicon/lexicon-hardware)** | **Unified Radio Firmware, Drivers & Reference Hardware** — Phase-C 2.6 Mbps FLRC burst firmware, SPI radio daemons, 3D enclosures, and turnkey PCB/Gerber/BOM reference designs across all supported radio devices. | `nRF54L15` (Zephyr), `ESP32-S3 AM36-Pico` (ESP-IDF), `K230` (RT-Smart/Linux), KiCad / STEP |
| **[`T-Display-K230_canmv_rt`](https://github.com/superlexicon/T-Display-K230_canmv_rt)** | **K230 Dual-Core RISC-V OS & BSP** — Hardened fork of the LilyGO T-Display K230 SDK (`CPU0` Linux + `CPU1` RT-Smart real-time microkernel) with 6-stage hardware CPU1 DVFS thermal throttling, PM domain power-gating, hardware `/dev/urandom` CSPRNG, `PROT_EXEC` page mapping, and Pocket Standby AMOLED blanking. | Canaan Kendryte K230 (`RISC-V C908`, RT-Smart + Linux) |

---

## Active Testnet & Reference Hardware

| Device | Form Factor | Radio & Compute | Firmware / Driver Location |
| :--- | :--- | :--- | :--- |
| **Seeed Studio LR2021 Eval Kit** | Stationary Validator / Bench Node | Nordic `XIAO nRF54L15` + Semtech `LR2021` (915 MHz / 2.4 GHz) | [`lexicon-hardware/firmware/nrf54l15-lr2021`](https://github.com/superlexicon/lexicon-hardware/tree/main/firmware/nrf54l15-lr2021) |
| **Lierda AM36-Pico (`L-LRMAM36-FANN4-PK02`)** | Plug-and-Play USB-C Radio Dongle | Espressif `ESP32-S3` + Semtech `LR2021` | [`lexicon-hardware/firmware/am36-lr2021`](https://github.com/superlexicon/lexicon-hardware/tree/main/firmware/am36-lr2021) |
| **LilyGO T-Display K230 Kit** | Handheld AMOLED Validator & Roamer Slate | Canaan `K230` Dual RISC-V + `LR2021` + `nRF9151` NTN/LTE | [`lexicon-hardware/drivers/k230-lr2021-radio`](https://github.com/superlexicon/lexicon-hardware/tree/main/drivers/k230-lr2021-radio) |
| **Lexicon Dual-RF USB Dongle** | Turnkey Production Reference Design | `ESP32-S3` + Dual Parallel `LR2021` (`RF0` + `RF1`) | [`lexicon-hardware/designs/lexicon-dual-rf-dongle`](https://github.com/superlexicon/lexicon-hardware/tree/main/designs/lexicon-dual-rf-dongle) |

---

## System Architecture

```text
+-----------------------------------------------------------------------------------+
|                             SUPERLEXICON SUPER-APP                                |
|   [ Blockchain & RF Dashboard ]  [ LexiChat ]  [ LexiDEX ]  [ Wallet ]  [ Apps ]  |
+-----------------------------------------+-----------------------------------------+
                                          | JSON-RPC (8545) / WebSocket Telemetry (8566)
+-----------------------------------------v-----------------------------------------+
|                              LEXICON PROTOCOL NODE                                |
|    • 4-Phase TDMA-BFT Consensus (P1 Propose -> P2 Vote -> P3 Precommit -> P4)     |
|    • Air-First Delta Compression & Compact Index-Mapped Block Certificates        |
|    • Dynamic Roamer Discovery, Validator Probation & Long-Range Repeater Relay    |
+-----------------------------------------+-----------------------------------------+
                                          | Phase-C Binary Serial / SPI Framing
+-----------------------------------------v-----------------------------------------+
|                        SEMTECH LR2021 FLRC RADIO LAYER                            |
|    • 2.6 Mbps Raw FLRC Burst Engine (511B Air Frames / Up to 64 KB Reassembly)    |
|    • Sub-GHz (915 MHz ISM) + 2.4 GHz Dual-Band Operation                          |
+-----------------------------------------------------------------------------------+
```
