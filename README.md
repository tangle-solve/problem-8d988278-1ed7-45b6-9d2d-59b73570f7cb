<!-- solve-problem:8d988278-1ed7-45b6-9d2d-59b73570f7cb -->
# A 3/2 approximation for Steiner Forest

A [Tangle Solve problem](https://solve.tangle.tools/problems/8d988278-1ed7-45b6-9d2d-59b73570f7cb).

## What is the problem?

**Steiner Forest.** Given an undirected graph \(G=(V,E)\), edge costs \(c:E\to\mathbb{R}_{\ge 0}\) (arbitrary nonnegative weights; typically general metrics/graph costs, not just tree metrics), and a set of demand pairs \(D=\{(s_1,t_1),\dots,(s_k,t_k)\}\), find a minimum-cost subgraph \(F\subseteq E\) in which every \(s_i\) and \(t_i\) lie in the same connected component. The task: give a polynomial-time algorithm with approximation ratio \(3/2\), i.e., producing \(F\) with \(c(F)\le \tfrac{3}{2}\cdot \mathrm{OPT}\), and a proof of correctness and of the ratio (and polynomial running time). Note that optimal Steiner Forest solutions do have optimal substructure on components (each component is a Steiner tree for its demand pairs), but the pairing of demands into components is the hard combinatorial core.

## Why does it matter?

Steiner Forest generalizes Steiner Tree and models multi-pair network construction where infrastructure (cables, fiber, roads) can be shared — the canonical telecommunications/network-design problem; it is the prize problem in the primal-dual literature. Beating 2 was a ~30-year barrier (AKR/GW 1991–92) only recently broken (see below); pushing toward 3/2 — the ratio long achieved for Steiner Tree in restricted metrics — would likely require fundamentally new LP relaxations or rounding techniques that would transfer to the wider network-design family (prize-collecting, survivable network design).

## What's already known?

- **Factor 2, deterministic, fast:** Agrawal–Klein–Ravi (1992) and Goemans–Williamson (1995) give primal-dual 2-approximations. These were the best for decades; the integrality gap of the natural cut LP is 2, so these methods cannot do better.
- **Better than 2 (2025):** Per the census record, Ahmadi et al. (2025) broke the factor-2 barrier. Details beyond this are not in the record — read the paper before assuming a specific technique; plausibly it is an LP-rounding approach inspired by modern Steiner Tree methods (directional/component-based LPs). (verify)
- **Gupta and Traub (2026):** simplifies the better-than-2 approximation (arXiv:2511.18460). This is your best entry point to the current frontier. (verify the exact ratio achieved; it is presumably \(2-\epsilon\), not 3/2.)
- **Adjacent:** For Steiner Tree, \(\ln 4+\epsilon\approx 1.39\) is known (Byrka–Grandoni–Rothvoß–Sanità, 2010) and 3/2 was recently achieved in \(\ell_1\)/tree metrics; Steiner Forest's demand-component assignment makes these tools harder to lift.

## What would count as solving it?

- **Primary:** A polynomial-time algorithm plus a theorem: for every Steiner Forest instance, output cost \(\le \frac{3}{2}\,\mathrm{OPT}(I)\). A referee needs the ratio proven against OPT (or against an LP with bounded integrality gap).
- **Acceptable variants:** (a) a new LP relaxation with integrality gap \(\le 3/2\) plus a rounding algorithm; (b) \(3/2+\epsilon\) for any constant \(\epsilon>0\); (c) \(3/2\) in restricted settings (e.g., bounded demand pairs per component, graphic metrics).
- **Not solving it:** improvement to \(2-\epsilon\) for vanishing \(\epsilon\), or heuristics without proven guarantees.

## How to start

1. Read Gupta–Traub (arXiv:2511.18460) first — it is the current frontier and presumably streamlined enough to expose the technique; identify exactly where the analysis loses beyond \(3/2\).
2. Then read Ahmadi et al. (2025) for the original breakthrough construction. (verify citation details)
3. Compare against the Steiner Tree toolkit (Byrka et al. randomized rounding of the directed component LP; the recent tree-metric 3/2 results) and pinpoint the obstruction to lifting each ingredient to forest: most likely the unknown partition of demand pairs into components.
4. Candidate direction: a component-based / hypergraphic LP for Steiner Forest with a randomized rounding + alteration scheme, or a primal-dual hybrid that pays \(3/2\) per component tree.

## Key references

- Agrawal, Klein, Ravi (1992), "When trees collide: an approximation algorithm for the generalized Steiner problem on networks," SIAM J. Comput. — the first primal-dual 2-approximation for Steiner Forest.
- Goemans, Williamson (1995), "A general approximation technique for constrained forest problems," SIAM J. Comput. — general primal-dual framework yielding factor 2; the baseline to beat.
- Ahmadi et al. (2025), better-than-two approximation for Steiner Forest — the barrier-breaking result; exact reference per census record. (verify)
- Gupta, Traub (2026), "Steiner Forest: A Simplified Better-Than-2 Approximation," arXiv:2511.18460, DOI: 10.1145/3798129.3800808 — simplified exposition of the sub-2 algorithm; start here.
- Byrka, Grandoni, Rothvoß, Sanità (2010), "An improved LP-based approximation for Steiner tree," STOC — 1.39 for Steiner Tree via directed-component LP; the toolbox source.

## Warnings

- The natural cut-based LP has integrality gap 2 — do not try to round it better.
- The 2025/2026 results are very recent; the census record gives no technique details, so verify everything about them from the arXiv paper directly before building on them.
- Beware confusing Steiner Forest with Steiner Tree results: ratios like 1.39 and 3/2 are for Steiner Tree; lifting them is nontrivial because the optimal component structure (which demands pair up) is unknown a priori.
- Cost model: "general graphs, nonnegative edge costs" is the standard setting; a 3/2 result only for special metrics is a strictly weaker contribution.

---
*`ALGO-000108` · unverified*

## Acceptance guidance

- **Primary:** A polynomial-time algorithm plus a theorem: for every Steiner Forest instance, output cost \(\le \frac{3}{2}\,\mathrm{OPT}(I)\). A referee needs the ratio proven against OPT (or against an LP with bounded integrality gap).
- **Acceptable variants:** (a) a new LP relaxation with integrality gap \(\le 3/2\) plus a rounding algorithm; (b) \(3/2+\epsilon\) for any constant \(\epsilon>0\); (c) \(3/2\) in restricted settings (e.g., bounded demand pairs per component, graphic metrics).
- **Not solving it:** improvement to \(2-\epsilon\) for vanishing \(\epsilon\), or heuristics without proven guarantees.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/8d988278-1ed7-45b6-9d2d-59b73570f7cb?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000108.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000108)
