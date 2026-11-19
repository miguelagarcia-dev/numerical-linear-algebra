# HW2 – Finite differences for an ODE, explained

**The problem:** solve the boundary value problem `y'' + 4y = 4x` on `[0, π/2]` with `y(0) = 0` and `y'(π/2) = 0`.

**The idea:** chop the interval into `n` pieces of width `h`, and replace derivatives with differences of neighbouring values:
`y'' ≈ (y[i-1] − 2y[i] + y[i+1]) / h²`.
Each grid point then gives one linear equation, so the whole ODE becomes a linear system `Ay = b` (a *tridiagonal* matrix, since each equation only touches its neighbours).

**How it's solved:** with an LU factorization: `A = LU`, then forward substitution (`Lz = b`) and back substitution (`Ux = z`).

**What the results show**
- Doubling `n` (halving `h`) cuts the error by about 4×, so the method is **second-order accurate** (error ∝ h²), matching the Taylor-series error terms.
- Extra credit: the exact solution is `y = x + ½ sin 2x`.
  - Homogeneous part: `C₁cos 2x + C₂sin 2x`.
  - Particular part: `x`.
  - The boundary conditions fix `C₁ = 0` and `C₂ = ½`.
  - Comparing to this confirms the h² convergence on a log-log plot (slope 2).
