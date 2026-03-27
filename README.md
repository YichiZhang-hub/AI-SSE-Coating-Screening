# AI-Driven High-Throughput Screening of Hydrophobic Coatings for Sulfide Solid-State Electrolytes

## 📖 Overview
Sulfide solid-state electrolytes (SSEs) possess high ionic conductivities but suffer from poor chemical stability and pronounced moisture sensitivity. This repository contains the code, data, and models for an AI-driven high-throughput screening strategy designed to identify optimal hydrophobic surface coating molecules to enhance the air stability of SSEs. 

By overcoming the inefficiency of traditional trial-and-error approaches, this workflow integrates Large Language Models (LLMs) with Graph Neural Networks (GNNs) to efficiently navigate a vast chemical space.

## ✨ Key Features & Workflow
Our screening pipeline consists of the following core modules:
* **Knowledge Mining & Modular Design:** Utilizes LLMs to extract chemically plausible head, linker, and tail functional groups from existing literature. These building blocks are systematically combined to generate a comprehensive library of over 16,000 candidate molecules.
* **Feature Engineering:** Employs RDKit to encode each candidate using graph-based molecular fingerprints.
* **GNN Property Prediction:** Utilizes Graph Neural Network (GNN) models to predict critical electronic attributes related to molecular affinity and hydrophobicity, effectively bypassing the computational bottleneck of extensive DFT calculations.
* **Unsupervised Clustering & Filtering:** Applies clustering algorithms to organize the library into distinct groups, from which representative molecules are prioritized for multidimensional evaluation (including DFT calculations and experimental validation).

## 🏆 Highlighted Results
Through this data-driven workflow, **2-(Perfluorohexyl)ethanethiol (PFHE)** was successfully identified as the top-performing coating candidate. Experimental validation confirmed that the modified PFHE@LPSC electrolyte retained an ionic conductivity of 1.85 mS cm⁻¹ (80% retention) after 24 hours of exposure to humid air. Furthermore, it maintained an 83.3% capacity retention after 600 cycles in a Li0.5In||LiNi0.92Co0.03Mn0.05O2 all-solid-state battery.

---

## ⚙️ Installation

We recommend using [Miniconda](https://docs.conda.io/en/latest/miniconda.html) or [Anaconda](https://www.anaconda.com/) to manage your Python environment. The workflow heavily relies on `PyTorch` for GNN training and `RDKit` for molecular feature engineering.

**1. Clone the repository**
```bash
git clone [https://github.com/YourUsername/AI-SSE-Coating-Screening.git](https://github.com/YourUsername/AI-SSE-Coating-Screening.git)
cd AI-SSE-Coating-Screening
```

**2. Create and activate a new Conda environment**
```bash
conda create -n sse-screening python=3.9
conda activate sse-screening
```

**3. Install dependencies**
You can install all required packages using the provided `requirements.txt` or `environment.yml` file. 

*Option A: Using pip*
```bash
pip install -r requirements.txt
```

*Option B: Using conda (Recommended for RDKit and PyTorch)*
```bash
conda env update --file environment.yml
```
*(Note: Please ensure you install the correct PyTorch version that matches your CUDA toolkit if you are training the GNNs on a GPU.)*

---

## 🚀 Usage

The codebase is organized modularly, following the screening workflow described in our paper. 

### Step 1: Library Generation
Generate the initial library of 16,000+ candidate molecules using the modular head-linker-tail approach based on LLM-extracted functional groups.
```bash
python scripts/01_generate_library.py --output data/candidate_library.csv
```

### Step 2: Feature Engineering & GNN Prediction
Process the SMILES strings using RDKit to extract topological molecular fingerprints and run the trained GNN model to predict electronic attributes (affinity and hydrophobicity).
```bash
# Extract molecular fingerprints
python scripts/02_feature_engineering.py --input data/candidate_library.csv --output data/features.npy

# Run GNN inference
python scripts/03_gnn_predict.py --features data/features.npy --model checkpoints/best_gnn_model.pt --output data/predictions.csv
```

### Step 3: Clustering and Screening
Perform unsupervised clustering on the multi-scale molecular features and apply multidimensional evaluation metrics to identify the top candidates.
```bash
python scripts/04_cluster_and_screen.py --data data/predictions.csv --n_clusters 12 --output results/top_candidates.csv
```

---

## 📂 Data Availability

The datasets necessary to reproduce our findings are provided in the `data/` directory:
* `extracted_groups.json`: The raw functional groups extracted from the literature via LLMs.
* `candidate_library.csv`: The complete library of 16,467 generated unique molecules.
* `dft_validation_set/`: The subset of structures and corresponding target properties calculated via Density Functional Theory (DFT) used to validate the GNN model.

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details. This allows for both academic and commercial use, provided proper attribution is given.

---

## 📖 Citation

If you find this code or our data-driven strategy useful in your research, please consider citing our paper:

```bibtex
@article{YourLastName2026,
  title={AI-Driven High-Throughput Screening of Hydrophobic Coatings for Sulfide Solid-State Electrolytes},
  author={Your Name and Co-authors},
  journal={Target Journal Name},
  year={2026},
  volume={xx},
  pages={xxx-xxx},
  doi={10.xxxx/xxxxx}
}
```
