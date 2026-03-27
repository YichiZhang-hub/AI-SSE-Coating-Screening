# AI-Driven High-Throughput Screening of Hydrophobic Coatings for Sulfide Solid-State Electrolytes

## 📖 Overview
[cite_start]Sulfide solid-state electrolytes (SSEs) possess high ionic conductivities but suffer from poor chemical stability and pronounced moisture sensitivity[cite: 14, 15]. [cite_start]This repository contains the code, data, and models for an AI-driven high-throughput screening strategy designed to identify optimal hydrophobic surface coating molecules to enhance the air stability of SSEs[cite: 2, 4]. 

[cite_start]By overcoming the inefficiency of traditional trial-and-error approaches, this workflow integrates Large Language Models (LLMs) with Graph Neural Networks (GNNs) to efficiently navigate a vast chemical space[cite: 3, 43].

## ✨ Key Features & Workflow
Our screening pipeline consists of the following core modules:
* [cite_start]**Knowledge Mining & Modular Design:** Utilizes LLMs to extract chemically plausible head, linker, and tail functional groups from existing literature[cite: 5]. [cite_start]These building blocks are systematically combined to generate a comprehensive library of over 16,000 candidate molecules[cite: 5, 62].
* [cite_start]**Feature Engineering:** Employs RDKit to encode each candidate using graph-based molecular fingerprints[cite: 6, 45].
* [cite_start]**GNN Property Prediction:** Utilizes Graph Neural Network (GNN) models to predict critical electronic attributes related to molecular affinity and hydrophobicity, effectively bypassing the computational bottleneck of extensive DFT calculations[cite: 6, 68].
* [cite_start]**Unsupervised Clustering & Filtering:** Applies clustering algorithms to organize the library into distinct groups, from which representative molecules are prioritized for multidimensional evaluation (including DFT calculations and experimental validation)[cite: 7, 46].

## 🏆 Highlighted Results
[cite_start]Through this data-driven workflow, **2-(Perfluorohexyl)ethanethiol (PFHE)** was successfully identified as the top-performing coating candidate[cite: 8]. [cite_start]Experimental validation confirmed that the modified PFHE@LPSC electrolyte retained an ionic conductivity of 1.85 mS cm⁻¹ (80% retention) after 24 hours of exposure to humid air[cite: 9, 47]. [cite_start]Furthermore, it maintained an 83.3% capacity retention after 600 cycles in a Li0.5In||LiNi0.92Co0.03Mn0.05O2 all-solid-state battery[cite: 10].
