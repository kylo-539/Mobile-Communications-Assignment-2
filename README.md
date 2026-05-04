# Assessment 2 – OFDM and OFDMA Systems
# Grade: 95%
**Author:** Kyle Sheehy  
**Date:** November 2025  

Simulation of an OFDM single-user system and an OFDMA two-user system with BER performance analysis over an AWGN channel using QPSK modulation.

---

## ⚠️ Source Code Availability

To preserve academic integrity, full source code is not publicly available.

This repository instead provides:

- Processed datasets (CSV)  
- High-resolution visualisations  
- Simulation structure and methodology  
- Analysis outputs and key findings  

Full implementation details are available upon request for professional or academic review.

---

## Files

| File | Description |
|------|-------------|
| `OFDM.py` | Single-user OFDM system: transmitter, AWGN channel, receiver, and BER vs SNR analysis |
| `OFDMA.py` | Two-user OFDMA system: subcarrier partitioning per user, shared IFFT/FFT chain, and per-user BER vs SNR analysis |

## System Parameters

| Parameter | Value |
|-----------|-------|
| Total bandwidth | 10 MHz |
| FFT size | 512 |
| Active subcarriers | 480 (93.75% utilisation) |
| Null subcarriers | 32 (DC + guard bands) |
| Subcarrier spacing | 15 kHz |
| Sampling rate | 7.68 MHz |
| Cyclic prefix ratio | 1/8 (12.5%) |
| CP length (samples) | 64 |
| Useful symbol duration $T_u$ | 66.67 μs |
| CP duration $T_{CP}$ | 8.33 μs |
| Total symbol duration $T_s$ | 75 μs |
| Modulation | QPSK (2 bits/symbol) |
| Signal amplitude | 5 |
| Number of bits (per user) | 100,000 |
| SNR range | 0 – 20 dB |

## Transmit / Receive Chain

```
Tx: bits → QPSK mapping → S/P → subcarrier mapping → IFFT → add CP → P/S → AWGN
Rx: → S/P → remove CP → FFT → extract subcarriers → QPSK decision → P/S → bits
```

## OFDM (Single User)

480 active subcarriers carry all user data. The simulation steps and their saved plots are:

| Step | Description | Output Image |
|------|-------------|--------------|
| 1 | Original bit sequence (first 100 bits) | `Step-1-Original-Sequence.png` |
| 2 | QPSK constellation mapping | `Step-2-QPSK-Mapping.png` |
| 3 | Frequency-domain subcarrier allocation | `Step-3-Frequency-Domain-Subcarrier-Allocation.png` |
| 4a | Time-domain signal after IFFT | `Step-4a-Time-Domain-OFDM-Signal-After-IFFT.png` |
| 4b | Time-domain signal after IFFT with CP | `Step-4b-Time-Domain-OFDM-Signal-After-IFFT-With-64-CP-Samples.png` |
| 5 | Frequency-domain received signal | `Step-5-Frequency-Domain-Received-Signal.png` |
| 6 | Tx vs Rx constellation diagrams | `Step-6-Tx-Vs-Rx-Constellation-Diagrams.png` |
| 7 | BER curve (simulated only) | `Step-7-OFDM-BER-Just-Simulated.png` |
| 7 | BER curve (simulated vs theoretical) | `Step-7-OFDM-BER-Sim-Theoretical.png` |

## OFDMA (Two Users)

480 active subcarriers are split equally: User 1 occupies the lower 240, User 2 the upper 240. Each user has an independent bit stream and BER curve.

| Step | Description | Output Image |
|------|-------------|--------------|
| 1 | Original bit sequences (both users) | `OFDMA-Step-1-Original-Sequence.png` |
| 2 | QPSK mapping for both users | `OFDMA-Step-2-QPSK-Mapping.png` |
| 3 | Frequency-domain subcarrier allocation | `OFDMA-Step-3-Frequency-Domain-Subcarrier-Allocation.png` |
| 4a | Time-domain signal after IFFT (symbol 1) | `OFDMA-Step-4a-Time-Domain-OFDM-Signal-After-IFFT-First-Symbol.png` |
| 4b | Time-domain signal after IFFT (symbol 2) | `OFDMA-Step-4b-Time-Domain-OFDM-Signal-After-IFFT-Second-Symbol.png` |
| 5a | Received signal time-domain (symbol 1, per SNR) | `OFDMA-Step-5c-Received-Signal-Time-Domain-First-Symbol-SNR{x}dB.png` |
| 5b | Received signal time-domain (symbol 2, per SNR) | `OFDMA-Step-5d-Received-Signal-Time-Domain-Second-Symbol-SNR{x}dB.png` |
| 6 | Frequency-domain received signal | `OFDMA-Step-6-Frequency-Domain-Received-Signal.png` |
| 7 | Tx vs Rx constellations (User 1 vs User 2) | `OFDMA-Step-7-Tx-Vs-Rx-Constellation-Diagrams-User1-vs-User2.png` |
| 8 | BER curve (simulated only) | `OFDMA-Step-8-OFDM-BER-Just-Simulated.png` |
| 9 | BER curve (simulated vs theoretical, per user) | `OFDMA-Step-9-OFDM-BER-Sim-Theoretical-User1-vs-User2.png` |

## Dependencies

```
numpy
scipy
matplotlib
```

Install with:
```bash
pip install numpy scipy matplotlib
```

## Running the Simulations

```bash
python OFDM.py
python OFDMA.py
```

Output images are saved to the working directory. Generated plots are also stored in `../Assessment 2 Images/OFDM Images/` and `../Assessment 2 Images/OFDMA Images/`.

