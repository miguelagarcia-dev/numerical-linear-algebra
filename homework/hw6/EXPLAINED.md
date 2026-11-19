# HW6 – PCA via the SVD, explained

**PCA:** find the directions along which the data varies most. Center the data (subtract the mean), take the SVD `X = UΣVᵀ`, and the columns of `V` are the principal components. The variance along each is `σᵢ²/(n−1)`.

**HW6-1**
1. Project onto the top `k` components with the full SVD.
2. Do it again with `scipy.sparse.linalg.svds`, which only computes the `k` singular vectors you ask for (much cheaper for big matrices).
3. Conditioning: `cond(XᵀX) = cond(X)²`, so forming `XᵀX` (the "covariance route") squares the numerical trouble. Going through the SVD directly is more accurate.
4. The singular-value plot shows how many components matter.

**HW6-2: experiments on 2-D data near a line**
- PC1 lines up with the line; the reconstruction from PC1 alone is the best 1-D fit.
- **Skip centering:** PC1 then tends to point toward the mean instead of along the spread, so it's wrong.
- **Add one outlier:** a single far-off point can tilt PC1 a lot, since PCA is driven by squared distances.

*(The first half of this notebook is lecture material reviewing the SVD and random projections.)*
