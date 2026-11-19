# HW4 – Eigendecomposition and QR, explained

**Eigenvalues/eigenvectors:** `Ax = λx`. The vector `x` keeps its direction under `A` and is only scaled by `λ`.

**HW4-1: random matrices.** Eigenvalues of a big random matrix are complex and spread out in a disk (the *circular law*), with radius growing like √n. Plotting many of them makes the circle visible.

**HW4-2: Gram-Schmidt accuracy.** Gram-Schmidt builds an orthonormal basis `Q` from the columns of `A` (that's QR factorization). With nearly parallel columns, classical Gram-Schmidt loses orthogonality to rounding error, so `QᵀQ` isn't quite the identity. Comparing against NumPy's Householder-based `qr` shows how much better a stable algorithm does.

**HW4-3: QR with shifts.** The basic QR algorithm repeatedly factors `A = QR` and forms `RQ`; the matrix slowly converges toward triangular form with the eigenvalues on the diagonal. It's very slow. *Shifting* (factor `A − μI`, then add `μI` back, with `μ` chosen near an eigenvalue) speeds convergence dramatically. This is the idea behind real eigenvalue solvers.
