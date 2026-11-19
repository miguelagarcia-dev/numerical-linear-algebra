# HW1 – Gaussian elimination, explained

**The problem:** solve a linear system `Ax = b`.

**The idea:** stack `b` onto `A` to make an *augmented matrix*, then use row operations to turn `A` into the identity. Whatever ends up in the last column is the answer `x`.

**What the code does (Gauss-Jordan style):**
1. Divide the pivot row so the diagonal entry is 1.
2. Subtract multiples of that row from *every other row* (above and below) to zero out the rest of the column.
3. Repeat for each column.

**Things worth knowing**
- Cost is roughly O(n³), which is why the later homeworks look at cheaper/iterative methods.
- Dividing by the pivot fails if it's 0. Real solvers swap rows first (*partial pivoting*), which also keeps rounding errors small.
- `LOUD=True` just prints each step so you can follow along. It's off by default so timing runs aren't slowed by printing.
