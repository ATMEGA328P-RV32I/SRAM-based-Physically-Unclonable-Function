# 64-Bit SRAM Physically Unclonable Function (PUF)

## Overview
This repository contains the design, schematic entry, and Monte Carlo simulation of a 64-bit SRAM-based Physically Unclonable Function (PUF). Designed in Cadence Virtuoso using the GPDK 45nm technology node, this project exploits inherent, random manufacturing variations (mismatch) in cross-coupled inverters to generate unique, unclonable cryptographic keys for hardware security.

## Architecture & Test Setup
* **Core Cell:** Standard 6-Transistor (6T) SRAM cell.
* **Array Size:** 8x8 grid generating a 64-bit response.
* **Technology Node:** Generic Process Design Kit (GPDK) 45nm.
* **Operation Principle:** The Wordlines (WL) are grounded to lock the cells, and Bitlines (BL/BLB) are left floating. The array is forced into a metastable state by applying a transient voltage ramp (0V to 1.1V with a 1ns rise time) to the VDD pins.

## Simulation & Results
The design was verified using Monte Carlo mismatch analysis in the Analog Design Environment (ADE XL) to simulate process variations across different physical chips.

### 1. Metastability & The "Spark"
During the VDD power-up ramp, the perfectly symmetrical inverters in each cell fight for dominance. The simulation successfully captures this metastability, showing internal nodes pulling to approximately 380mV (transistor threshold) before resolving to a stable Logic 1 (1.1V) or Logic 0 (0V) based purely on microscopic mismatch.

### 2. Output Waveforms
The repository contains the transient output waveforms for all 64 individual cells during the power-up phase. 
* 📂 You can view all 64 individual bit resolutions in the `/waveforms` directory.

### 3. Inter-Chip Variation & Uniqueness
By running the Monte Carlo simulation with different random seeds (simulating different physical chips off the manufacturing line), the PUF successfully yielded different 64-bit responses (e.g., shifting bit patterns like `00100011.....` to `11000001.....`). This confirms the uniqueness and viability of the hardware fingerprint.

## Tools Used
* Cadence Virtuoso Schematic Editor
* Analog Design Environment (ADE XL)
* Spectre Circuit Simulator

## About the Author
**Atul Kumar** B.Tech in Electronics and Communication Engineering (ECE), IIT Patna
