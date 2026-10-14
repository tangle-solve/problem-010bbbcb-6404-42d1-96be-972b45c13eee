<!-- solve-problem:010bbbcb-6404-42d1-96be-972b45c13eee -->
# Exact random 3-SAT threshold

A [Tangle Solve problem](https://solve.tangle.tools/problems/010bbbcb-6404-42d1-96be-972b45c13eee).

## What is the problem?

Consider a random 3-SAT instance: $n$ Boolean variables and $m = \lfloor \alpha n \rfloor$ clauses, each clause consisting of 3 literals chosen uniformly at random (with replacement, or without — the two conventions are asymptotically equivalent). Define $r_n(\alpha) = \Pr[\text{the instance is satisfiable}]$. The problem is to determine the **satisfiability threshold** $\alpha_c$: prove (or disprove) that there exists a constant $\alpha_c$ such that for all $\varepsilon > 0$:
- if $\alpha \le \alpha_c - \varepsilon$, then $r_n(\alpha) \to 1$,
- if $\alpha \ge \alpha_c + \varepsilon$, then $r_n(\alpha) \to 0$,

and then identify $\alpha_c$ exactly for $k=3$. The statistical-physics 1RSB (one-step replica symmetry breaking) cavity method predicts $\alpha_c \approx 4.2667$. Friedgut's theorem gives a threshold at some $n$-dependent sequence $\alpha_c(n)$ but not its concentration on a constant. Note a subtlety: proving a sharp constant threshold at $k=3$ is itself part of the problem; Ding–Sly–Sun proved the physics prediction for $k \ge k_0$ (large but effectively unspecified constant, astronomically large in their analysis).

## Why does it matter?

Random 3-SAT is the canonical benchmark for phase transitions in random constraint satisfaction problems, underlying the empirical hardness of instances near threshold and the design of SAT solvers. An exact resolution would validate (or refute) the 1RSB cavity methodology of statistical physics on its most famous test case, and would likely require techniques transferring to random graph coloring, regular 3-SAT, NAE-SAT, and spin glasses. It is also the flagship open question in average-case complexity at the interface of rigorous probability and non-rigorous physics.

## What's already known?

- **Friedgut (1999):** a sharp threshold exists at some $\alpha_c(n)$ possibly depending on $n$; coarse bounds give roughly $3.52 < \alpha_c < 4.49$ (best current: lower $\approx 3.86$ via algorithmic local lemma methods (verify), upper $\approx 4.4898$ via careful first-moment/cover arguments, Díaz, Kirousis, Mitsche, Pérez-Giménez (verify)).
- **Mézard–Parisi–Zecchina (2002):** non-rigorous 1RSB cavity computation predicting $\alpha_c \approx 4.2667$ via survey propagation.
- **Ding–Sly–Sun (2015/2022, Annals):** rigorous proof of the $k$-SAT satisfiability conjecture for all $k \ge k_0$: the threshold equals the 1RSB prediction $s_k$, with $s_k \to 2k\ln 2$. Their proof requires $k$ large because it needs (i) pointwise convergence of the survey recursion to its fixed point with quantitative error bounds and (ii) a second-moment/overlap analysis where error terms are exponentially small in $k$. At $k=3$ the 1RSB fixed point must be computed on a complicated continuous distribution over $\mathbb{R}^{\pm 1}$-valued messages, and errors don't decay.
- **Panchenko, Bayati–Gamarnik–Tetali and others:** rigorous spin-glass and overlap-structure results for related models (regular $k$-SAT, diluted Mean-field spin glasses) that formalize parts of RSB but don't cover Poisson random 3-SAT.
- **Why it falls short:** all known approaches need either $k \to \infty$ (message recursion contraction) or symmetric ensembles (regularity) to control the second moment.

## What would count as solving it?

1. **Full solution:** a proof that for $k=3$ the threshold exists, is a constant, and equals $\alpha_c \approx 4.2667$ (equivalently, the 1RSB condensation threshold $s_3$); i.e., $\Pr[\text{SAT}] \to 1$ below and $\to 0$ above, matching Ding–Sly–Sun at $k=3$.
2. **Partial/strong results:** (a) existence of a constant threshold at $k=3$ (sharpening Friedgut); (b) matching upper and lower bounds within $o(1)$ (currently gap ≈ 0.63); (c) proving the threshold equals *any* explicit constant, even if not proven equal to $s_3$.
3. **Negative result:** demonstrating the threshold doesn't concentrate on a constant (widely believed impossible after Friedgut, but technically open for fixed $k$).

## How to start

1. **Read Ding–Sly–Sun carefully**, especially Section 4 (second moment with survey-guided tilting) and the enumeration of where the analysis uses $k \ge k_0$ — this is your checklist of obstacles. Each inequality with a $2^{-\Theta(k)}$ slack is a target for $k=3$.
2. **Understand the 1RSB formalism:** read Mézard–Montanari, *Information, Physics, and Computation*, Chapters 14–19 for survey propagation and the definition of $s_k$, so you can define $s_3$ rigorously (via the fixed point of the survey distribution recursion).
3. **Consider easier intermediate targets:** random regular 3-SAT, or $k=4,5$, where Panchenko-style rigorous treatments of 1RSB overlap structure (multi-overlay Ghirlända–Guerra identities for diluted systems) may already nearly suffice. A rigorous Aizenman–Sims–Starr / Panchenko coupling argument for Poisson 3-SAT would be a major milestone.
4. **Main obstacle:** controlling the second moment — the naive second moment fails; the DSS tilting works only when the survey recursion contracts uniformly, which it does not at $k=3$ where the fixed point distribution is genuinely continuous and complex.

## Key references

- M. Mézard, G. Parisi, R. Zecchina (2002), "Analytic and Algorithmic Solution of Random Satisfiability Problems," *Science* 297, 812. Non-rigorous 1RSB/survey-propagation computation of the threshold and the SP algorithm; source of the 4.2667 prediction.
- J. Ding, A. Sly, N. Sun (2015), "Proof of the Satisfiability Conjecture for Large k," arXiv:1411.0650 (Annals of Mathematics, 2022). Proves the $k$-SAT threshold equals the 1RSB prediction for all $k \ge k_0$; the definitive rigorous technique to adapt. https://arxiv.org/abs/1411.0650
- E. Friedgut (1999), "Sharp thresholds of graph properties, and the $k$-SAT problem," *J. AMS* 12(4). Establishes a (possibly $n$-dependent) sharp threshold for satisfiability.
- M. Mézard, A. Montanari (2009), *Information, Physics, and Computation*, Oxford. Textbook treatment of replica symmetry breaking, survey propagation, and the definition of the 1RSB prediction $s_k$.
- D. Panchenko (2013), *The Sherrington–Kirkpatrick Model*, Springer. Rigorous RG methods; see also his subsequent work on diluted/regular CSPs for rigorous 1RSB overlap structures. (verify exact applicability to Poisson 3-SAT)

## Warnings

- The Friedgut theorem does **not** give a constant threshold at $k=3$; do not assume threshold concentration as given.
- Naive second-moment methods provably fail at any $k$; don't rederive them — read DSS first.
- Different ensembles (clauses with/without replacement, literals allowing repeats) change finite-$n$ but not asymptotics; state your convention.
- "Exact" here means the limit constant, not finite-$n$ window behavior (the scaling window is a separate, harder question).
- The predicted 4.2667 is itself only defined via an implicitly computed fixed point; a rigorous self-contained definition of $s_3$ is part of a complete solution.
- Belief that $k_0$ in DSS is astronomically large is folklore from the error analysis; the paper proves existence of some $k_0$. (verify current improvements)

---
*`ALGO-000144` · unverified*

## Acceptance guidance

1. **Full solution:** a proof that for $k=3$ the threshold exists, is a constant, and equals $\alpha_c \approx 4.2667$ (equivalently, the 1RSB condensation threshold $s_3$); i.e., $\Pr[\text{SAT}] \to 1$ below and $\to 0$ above, matching Ding–Sly–Sun at $k=3$.
2. **Partial/strong results:** (a) existence of a constant threshold at $k=3$ (sharpening Friedgut); (b) matching upper and lower bounds within $o(1)$ (currently gap ≈ 0.63); (c) proving the threshold equals *any* explicit constant, even if not proven equal to $s_3$.
3. **Negative result:** demonstrating the threshold doesn't concentrate on a constant (widely believed impossible after Friedgut, but technically open for fixed $k$).

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/010bbbcb-6404-42d1-96be-972b45c13eee?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000144.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000144)
