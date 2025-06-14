# Reinforcement Learning-Based Initialization of Evolutionary Concept Learning

This repository contains the implementation accompanying a **research paper** that integrates **Reinforcement Learning (RL)** to generate interpretable explanations for predictions made by **Graph Neural Networks (GNNs)**.

Instead of relying solely on black-box attribution methods, this work focuses on **generating logical class expressions** (e.g., OWL Description Logics) that explain why certain nodes are predicted to belong to specific classes. These expressions are learned by an RL agent performing pathfinding over a knowledge graph trained with TransE embeddings and evaluated using a GNN model.

---

## Key Features

- GNNs trained using **FASTRGCN** on RDF-based knowledge graphs.
- Uses **TransE** embeddings for entity and relation representations.
- RL agent based on **REINFORCE** that generates OWL logical expressions from paths.
- Supports **multiple datasets**: AIFB, MUTAG, and a synthetic MINI dataset.
- Comparison of RL-based explanation paths vs. random and biased walk initializations.
- Explanations rendered in **DL Syntax** via OWLAPI Python bindings (`owlapy`).

---

## Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/talhaamin94/Reinforcement-Learning-Based-Initialization-of-Evolutionary-Concept-Learning.git
```

### 2. Install Packages

```bash
pip install -r requirements.txt
```

Make sure you have Python 3.10+ and CUDA if running on GPU.

## Running experiments

```bash
python run.py --dataset [AIFB|MUTAG|MINI] --num_walks 10 --walk_len 2
```

### Arguments

- `--dataset`: Choose between `AIFB`, `MUTAG`, or `MINI`.
- `--num_walks`: Number of random/baseline/RL walks to compare.
- `--walk_len`: Maximum walk length for RL agent and baselines.

### Examples

Train and evaluate on AIFB

```bash
python run.py --dataset AIFB --num_walks 10 --walk_len 2
```

Train on AIFB without experiments:

```bash
python run.py --dataset AIFB

```

## Dataset Details

You do **not** need to manually download any datasets.

- **AIFB** and **MUTAG** are automatically downloaded when you run the project the first time, using [`torch_geometric.datasets.Entities`](https://pytorch-geometric.readthedocs.io/en/latest/generated/torch_geometric.datasets.Entities.html).
- The `.nt.gz` RDF files are extracted and prepared internally.
- **MINI** is a synthetic RDF dataset generated using a custom graph generator with labeled examples.

---

## Dataset References

- **AIFB**:  
  [Kernel Methods for Mining Instance Data in Ontologies](https://link.springer.com/chapter/10.1007/978-3-540-76298-0_5)

- **MUTAG**:  
  [Toxicity Prediction Using Graph Kernels](https://link.springer.com/chapter/10.1007/3-540-44673-7_34)

## Output

Results of walk-based explanation evaluations are saved in:

results/{DATASET}\_initialization_comparison.json

Each result file includes:

- Best logical expression
- Final reward
- Average reward
- Full list of tested paths
