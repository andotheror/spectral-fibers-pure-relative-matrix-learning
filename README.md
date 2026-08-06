# Spectral Fibers for Pure-Relative Matrix Learning and Hessian Correction

## Abstract

Large curvature matrices can be applied to vectors long before they can be materialized. Given products with $A$ and $A^\top$, we study its best Frobenius approximation from an arbitrary known $q$-dimensional linear matrix family. Classical matrix probing regresses a prescribed dictionary but needs conditioning and high-numerical-rank assumptions. The recent worst-case theory achieves roughly $\sqrt q$ queries, but only a $(3+\varepsilon)$ approximation with an additive error floor, and leaves pure relative error open.

We resolve this problem with a nonadaptive polynomial-time algorithm. It returns $\widehat B$ satisfying

$$\\|A-\widehat B\\|_F^2 \leq (1+\varepsilon)\min_{B\in\mathcal L}\\|A-B\\|_F^2$$

using $\widetilde O(\sqrt{q/\varepsilon})$ products. The mechanism spectrally splits the known family, measures selected row and column fibers exactly, and regresses only the doubly projected residual. We also give an affine-baseline form suited to preconditioning.

On a 5,770-dimensional CIFAR-10 last-layer Hessian over frozen MobileNetV3 features, 48 products recover a historical non-Kronecker correction to 0.38 percent excess over its family oracle. Unprojected probing still has 0.43 percent excess at 128 products. At a matched 48-product budget, the reduction repeats by factors of 2.4 to 4.4 across three independently built dictionaries. The correction lowers median PCG iterations from 186 for K-FAC and 171 for EK-FAC to 152. Finally, an adaptive $\Omega(\sqrt{q/\varepsilon})$ lower bound shows that the query law is minimax sharp up to logarithms for $q\geq C/\varepsilon$.

## Main results

**Theorem (Universal pure relative error).** For every known $q$-dimensional linear matrix family $\mathcal L$, there is a nonadaptive polynomial-time algorithm using

$$\widetilde O\\!\left(\sqrt{q/\varepsilon}\\,\log(1/\delta)\right)$$

products with $A$ and $A^\top$ that returns, with probability at least $1-\delta$, some $\widehat B\in\mathcal L$ with

$$\\|A-\widehat B\\|_F^2 \leq (1+\varepsilon)\min_{B\in\mathcal L}\\|A-B\\|_F^2.$$

The query count is also at most $\min\\{n_1,n_2\\}$ by deterministic recovery. This is pure relative error, with no additive floor and no conditioning or numerical-rank assumption, which is what the previous $(3+\varepsilon)$ worst-case theory left open.

**Theorem (Matching lower bound).** There are universal constants $c,C,\varepsilon_0>0$ such that for every $0<\varepsilon<\varepsilon_0$ and $q\geq C/\varepsilon$, some $q$-dimensional linear family and a distribution on symmetric targets require at least $c\sqrt{q/\varepsilon}$ possibly adaptive products to achieve $(1+\varepsilon)$ relative error with constant probability.

The upper and lower bounds match up to logarithms, so the $\sqrt{q/\varepsilon}$ query law is minimax sharp. The reduction goes through a sharp fixed-sparsity lower bound whose hard pattern is symmetric, so transpose products reveal nothing extra and adaptivity does not help.

**Mechanism: family-side leverage.** For a Frobenius-orthonormal basis $P_1,\ldots,P_q$ of $\mathcal L$, form the partial trace

$$K_L=\sum_{i=1}^q P_iP_i^\top,\qquad \mathrm{tr}\\,K_L=q.$$

Its eigenvalues measure how strongly the whole family concentrates in each direction. The algorithm spectrally splits $\mathcal L$ along this operator, measures the heavy row and column fibers exactly, and applies randomized regression only to the doubly projected residual, where the effective dimension is small.

**Corollary (Affine baseline).** The same machinery applies with a known baseline subtracted, which is the form used for preconditioning: learn a correction to K-FAC or EK-FAC rather than the full curvature matrix.

**Empirical result.** On a 5,770-dimensional CIFAR-10 last-layer Hessian over frozen MobileNetV3 features, 48 products reach 0.38 percent excess over the family oracle, while unprojected probing is still at 0.43 percent with 128 products. The advantage reproduces at a matched 48-product budget across three independently constructed dictionaries, by factors of 2.4 to 4.4. Median PCG iterations drop from 186 (K-FAC) and 171 (EK-FAC) to 152.

## Keywords

matrix-vector products, matrix probing, structured matrix approximation, relative error, query complexity, minimax lower bound, Hessian approximation, K-FAC, preconditioning, curvature estimation

## Files

- `main.pdf`
- `main.tex`
- `references.bib`
- `deep_hessian_study.pdf` figure
- `iclr2027_conference.sty`, `iclr2027_conference.bst`, `natbib.sty`, `fancyhdr.sty`
- `supplement.zip` scripts, seeds, experiment, figure generator, and raw summaries reproducing every reported number
- `main.pdf.ots`, `README.md.ots`, `supplement.zip.ots` OpenTimestamps priority proofs
