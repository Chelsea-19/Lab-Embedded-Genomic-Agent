# Lab-Embedded Genomic Agent

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Model](https://img.shields.io/badge/Model-Evo2-green)
![License](https://img.shields.io/badge/License-MIT-purple)
![Status](https://img.shields.io/badge/Status-Prototype-orange)

**Bridging the gap between High-Performance Computing (HPC) foundation models and resource-constrained wet-lab environments.**

## Overview

The **Lab-Embedded Genomic Agent** is a tiered AI framework designed to deploy large-scale genomic foundation models (specifically **Evo 2**) directly into wet-lab workflows.

While genomic foundation models demonstrate state-of-the-art capabilities, they typically require massive HPC clusters, making them inaccessible for real-time decision-making in standard laboratories. This project solves this by introducing a **"Teacher-Student" architecture**:

1.  **Tier 1 (Cloud):** Heavy computational lifting (Evo 2) to extract genomic language statistics.
2.  **Tier 3 (Edge):** A lightweight, quantized agent running on a single consumer GPU (e.g., RTX 4090) that ranks candidate regions for experimental validation.

This tool does not just output numbers; it provides **actionable decision support** by identifying genomic "anomalies" (potential toxins, virulence factors) and linking them to literature via RAG (Retrieval-Augmented Generation).

## System Architecture

The system operates on a three-tier architecture designed to decouple heavy inference from local decision-making.

![System Architecture](docs/fig.jpg)
*(Fig 1. Tiered Architecture: From HPC Foundation to Edge Deployment)*

* **Tier 1: HPC Foundation (Teacher Model)**
    * Utilizes **Evo 2** (40B+) for long-context genomic modeling.
    * Calculates zero-shot perplexity (PPL) landscapes to identify statistical anomalies in the genome.
* **Tier 2: Distillation Pipeline**
    * Compresses feature representations and optimizes for edge deployment.
* **Tier 3: Lab-Embedded Edge Layer (Student & RAG)**
    * **Hardware:** Runs on a single local workstation (Consumer GPU).
    * **Function:** Aggregates anomaly signals, performs RAG against local knowledge bases, and outputs a ranked list of candidate regions for wet-lab validation.

## Key Features

* **Zero-Shot Anomaly Detection:** Leverages the "genomic language" distribution to identify non-typical sequences (e.g., horizontal gene transfers, toxins) without labeled training data.
* **Resource-Constrained Inference:** Optimized for **4-bit quantized inference** on standard lab workstations.
* **RAG-Enhanced Reporting:** Automatically correlates high-perplexity regions with existing literature and databases (NCBI/UniProt) to suggest potential functions.
* **Actionable Outputs:** Generates structured reports (`.pdf`, `.csv`) prioritizing "Top-K" targets for PCR or functional assay validation.
