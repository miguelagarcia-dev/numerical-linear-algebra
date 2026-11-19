# HW3 – Jacobi and Gauss-Seidel, explained

**The problem:** solve a big linear system `Ax = b` without doing Gaussian elimination.

**Iterative methods** start from a guess and keep improving it:
- **Jacobi:** compute every new entry using only the *old* iterate.
- **Gauss-Seidel:** same, but use new values as soon as they're computed. It usually converges about twice as fast.

Both split `A` into diagonal / lower / upper parts and repeat `x ← M⁻¹(N x + b)`. They converge when the iteration matrix has spectral radius < 1 (e.g. for diagonally dominant matrices).

**Why bother?** For huge *sparse* systems (like finite-difference matrices), each iteration costs only O(n), whereas direct elimination is far more expensive. For small systems, direct methods win.

**What the homework looks at**
- The L2 norm of the error vs. iteration number (it drops roughly geometrically).
- How run time grows with system size `n`: faster than linearly. Each iteration is O(n), but the number of iterations also grows (~n²), because as the grid spacing `h` shrinks the convergence factor creeps toward 1.
