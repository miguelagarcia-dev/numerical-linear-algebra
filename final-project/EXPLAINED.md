# Final project – the ideas, explained

## The big picture
Every cell in your body has the same DNA, but different cells switch different genes on. **Transcription factors (TFs)** are proteins that switch other genes on or off. A **gene regulatory network (GRN)** is the map of "TF → target gene" arrows. Building that map from data is the goal.

**Single-cell RNA-seq (scRNA-seq)** measures how active every gene is in each individual cell. The result is a big table (cells × genes). It's noisy and full of zeros, so it needs careful cleaning before use.

## Milestone 2 – cleaning and exploring the data
Steps the notebook walks through:
- **Quality control (QC):** flag bad cells. Examples are a high share of mitochondrial reads (a sign of a dying cell), very few detected genes, or odd count/gene ratios. "Flagged" means marked for review, not automatically deleted.
- **Normalization / log transform:** make cells comparable, since some were just sequenced more deeply.
- **Highly variable genes:** keep the genes that actually differ between cells (the notebook keeps the top 500 by variance).
- **Dimensionality reduction (PCA, UMAP):** squash thousands of genes down to a few dimensions so the cells can be plotted and clustered.
- **Clustering and marker genes:** group similar cells (Leiden clustering), then check known marker genes to see what cell types the groups are.
- **Cell-cycle phase (S, G2M):** checked as another source of variation.

It's run on four datasets: human liver bud (hHEP), human ES cells (hESC), mouse ES cells (mESC), and mouse blood stem cells (mHSC). The notebook's answers to the assignment questions sit at the top.

## Milestone 3 – IGEGRNS, the GRN model
Based on the paper by Gan et al. The trick is to treat GRN inference as **link prediction**: given a TF and a gene, predict whether an arrow exists between them.

1. **Graph:** genes are nodes; known regulatory links form the edges. A *reference network* (here, HepG2 ChIP-seq) provides the known positives.
2. **GraphSAGE:** gives each gene a 256-number embedding by mixing its own expression profile with the average of its neighbours'.
3. **Top-k pooling:** picks the most influential gene(s) in the whole graph so each prediction has some global context.
4. **CNN scoring:** for a gene pair, stack the two embeddings plus the top-k embedding into a small matrix, run it through 3 convolutional layers, and output a probability that the TF regulates the target.

**Evaluation**
- **5-fold cross-validation:** hide part of the known edges, train on the rest, and test on the hidden ones.
- **AUROC / AUPRC:** ranking-quality scores (1.0 is perfect). AUPRC is the stricter one when real edges are rare, which they are here.
- **Baselines:** simple rules (absolute correlation, TF out-degree, target in-degree) that the model has to beat to be worth it.
