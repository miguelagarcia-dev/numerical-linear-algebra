# HW5 – SVD, explained

**The SVD:** any matrix factors as `A = UΣVᵀ`, where `U` and `V` have orthonormal columns and `Σ` holds the singular values (largest first).

**Low-rank approximation:** keeping only the top `k` singular values gives the best rank-`k` approximation of `A` (Eckart-Young). Since `‖A‖²_F = Σσᵢ²`, the share of the matrix you capture is `Σᵢ≤k σᵢ² / Σσᵢ²`.

**HW5-1:** build a 100×100 random matrix whose entries are correlated with their neighbours (so it's smooth, not noise). Smooth data is nearly low-rank, so a handful of singular vectors capture almost all of the norm. For pure noise you'd need nearly all of them.

**HW5-2: MovieLens 100K.** Put the ratings in a 1682 (movies) × 943 (users) matrix. The top singular vectors act like "latent factors": groups of movies and groups of users that tend to go together (e.g. taste/genre). The notebook downloads the dataset itself.
