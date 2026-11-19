# Math 391 – Class Work

Notebooks from my Math 391 course (numerical linear algebra and its use in data analysis), plus a final project on inferring gene regulatory networks from single-cell data.

## Homework

Each assignment has its own folder with one notebook, plus a short "notes" file explaining the topic.

| # | Notebook | What it's about |
|---|----------|-----------------|
| 1 | [hw1](homework/hw1/hw1.ipynb) ([notes](homework/hw1/EXPLAINED.md)) | Gaussian elimination solver (with optional step-by-step printing) |
| 2 | [hw2](homework/hw2/hw2.ipynb) ([notes](homework/hw2/EXPLAINED.md)) | Finite-difference solution of an ODE with an LU solver, grid refinement, and a check against the exact solution (extra credit) |
| 3 | [hw3](homework/hw3/hw3.ipynb) ([notes](homework/hw3/EXPLAINED.md)) | Jacobi vs. Gauss-Seidel iteration: error vs. iteration count and how run time scales with system size |
| 4 | [hw4](homework/hw4/hw4.ipynb) ([notes](homework/hw4/EXPLAINED.md)) | Eigendecomposition: random-matrix eigenvalues, Gram-Schmidt accuracy, and QR iteration with shifts |
| 5 | [hw5](homework/hw5/hw5.ipynb) ([notes](homework/hw5/EXPLAINED.md)) | SVD: low-rank approximation of a correlated matrix, plus structure in the MovieLens 100K ratings |
| 6 | [hw6](homework/hw6/hw6.ipynb) ([notes](homework/hw6/EXPLAINED.md)) | PCA via the SVD (full vs. `svds`), conditioning, and what centering and outliers do to the components |

## Final project

**Inferring gene regulatory networks (GRNs) from single-cell RNA-seq.** It's done in three milestones:

1. [Milestone 1](final-project/milestone1.pdf): one-page summary of the IGEGRNS paper (Gan et al., *Bioinformatics*), which frames GRN inference as link prediction using GraphSAGE embeddings and a small CNN.
2. [Milestone 2](final-project/milestone2/milestone2.ipynb): quality control and exploration of scRNA-seq data (filtering, clustering, marker genes) across four datasets: human liver bud (hHEP), human ES cells (hESC), mouse ES cells (mESC), and mouse blood stem cells (mHSC). Pre-run copies for three of the datasets are in [`executed/`](final-project/milestone2/executed).
3. [Milestone 3](final-project/milestone3/milestone3.ipynb): a step-by-step re-implementation of IGEGRNS, trained and evaluated (5-fold CV, AUROC/AUPRC) against simple baselines on the hHEP data with the HepG2 ChIP-seq reference network.

New to the topic? [The ideas, explained](final-project/EXPLAINED.md) covers GRNs, scRNA-seq cleanup, and the IGEGRNS model in plain language.

### How to run it

You'll need Python 3.9+ and Jupyter.

**Milestone 2**

```bash
cd final-project/milestone2
pip install -r requirements.txt
jupyter notebook milestone2.ipynb
```

Pick the dataset by changing `DATASET` in the "Dataset settings" cell (`"hHEP"`, `"hESC"`, `"mESC"`, or `"mHSC"`). The data files are already in `data/`, and the notebook downloads anything that's missing from GEO.

**Milestone 3**

```bash
cd final-project/milestone3
pip install -r requirements.txt
jupyter notebook milestone3.ipynb
```

It needs internet on the first run: it clones the [IGEGRNS repo](https://github.com/DHUDBlab/IGEGRNS) and downloads the hHEP expression data from GEO. A GPU helps but isn't required.

## Notes

- Homework 5 uses the [MovieLens 100K dataset](https://grouplens.org/datasets/movielens/100k/), which the notebook downloads itself.
- The two papers the final project builds on aren't included here (copyright). Find them by title: *Inferring gene regulatory networks from single-cell transcriptomics based on graph embedding* (Gan et al.) and *Tutorial: guidelines for the computational analysis of single-cell RNA sequencing data*.
