# Symbolic Regression and Equation Discovery

## Search space and discovery targets

- **[Expression discovery](https://arxiv.org/abs/2107.14351)** — 2021. Symbolic regression searches mathematical expressions as well as coefficients. SRBench separates predictive accuracy, expression complexity and exact recovery; a compact accurate formula need not be the generating equation.
- **[Grammar and complexity](https://github.com/astroautomata/PySR/blob/master/docs/src/options.md)**. Operators, nesting constraints and expression costs define which equations are searchable. PySR exposes these choices explicitly; changing the grammar changes the problem, not just the optimizer.

## Evolutionary and structured search

- **[Genetic programming / Operon](https://github.com/heal-research/operon)** — 2020. Evolves expression trees and optimizes numerical constants. Operon provides a C++ implementation; combining structural search with coefficient fitting differs from selecting terms in one fixed linear dictionary.
- **[PySR / SymbolicRegression.jl](https://arxiv.org/abs/2305.01582)** — 2023. Uses multiple evolving populations with an evolve–simplify–optimize loop. Searches expression structure while fitting constants and retaining accuracy–complexity alternatives; Python wraps a Julia backend.
- **[AI Feynman](https://arxiv.org/abs/1905.11481)** — 2019. Combines neural fitting with recursive tests for symmetry, separability and other simplifying structure. Udrescu and Tegmark’s search exploits properties of physics formulas rather than treating every expression equally.
- **[AI Feynman 2.0](https://arxiv.org/abs/2006.10782)** — 2020. Uses gradients of a fitted neural model to discover generalized symmetries and graph modularity. Returns accuracy–complexity tradeoffs and extends discovery to probability densities through normalizing flows.

## Probabilistic, exhaustive and shared-structure search

- **[Bayesian machine scientist](https://arxiv.org/abs/2004.12157)** — 2020. Samples equations with MCMC using an approximate model posterior and a prior learned from a corpus of formulas. Retaining alternatives represents uncertainty over expression structure rather than selecting only one best-fitting equation.
- **[Exhaustive symbolic regression](https://arxiv.org/abs/2211.11461)** — 2022. Enumerates expressions within an operator set and size bound, then ranks them by minimum description length. Exhaustive structure search does not ensure a global optimum unless numerical constants are also optimized correctly.
- **[Multi-level symbolic regression](https://proceedings.mlr.press/v238/sen-fong24a.html)** — 2024. Learns a shared expression structure with group-specific coefficients. Parallel searches are merged across groups; MSRBench tests this intermediate setting between one pooled equation and unrelated fits for every group.

## Sparse dynamical-system identification

- **[SINDy](https://arxiv.org/abs/1509.03580)** — 2015. Selects sparse combinations of candidate functions to model dynamics from measurements. Brunton et al. rely on a suitable function library and state representation; sparsity alone cannot recover terms absent from that library.
- **[PDE-FIND](https://arxiv.org/abs/1609.06401)** — 2016. Rudy et al. select nonlinear and spatial-derivative terms by sparse regression. Multiple trajectories can distinguish equations that fit one trajectory; derivative estimation and library choice affect recovery.
- **[Weak SINDy](https://arxiv.org/abs/2005.04339)** — 2020. Uses integrated weak-form equations instead of pointwise derivative estimates. Messenger and Bortz recover dynamics more robustly under white measurement noise in tested systems; test functions and the candidate library remain part of identification.
- **[SINDy-PI](https://arxiv.org/abs/2004.02322)** — 2020. Searches implicit equations and rational dynamics through parallel sparse regressions. It avoids the noise-sensitive null-space approach of earlier implicit SINDy and extends recovery to studied ODEs, PDEs and conservation laws.
- **[PySINDy](https://joss.theoj.org/papers/10.21105/joss.02104)** — 2020. Python implementation of sparse dynamical-system identification. Treat differentiation, candidate-library construction and sparse fitting as parts of the identification procedure, not interchangeable preprocessing details.
- **[Universal differential equations](https://arxiv.org/abs/2001.04385)** — 2020. Combines known dynamics with trainable unknown terms. Rackauckas et al. fit hybrid systems and use symbolic regression to extract missing mechanisms; the equation is constrained by supplied physics and observed trajectories.

## Neural search and pretrained equation models

- **[Deep symbolic regression](https://arxiv.org/abs/1912.04871)** — 2019. An RNN samples expressions; risk-seeking policy gradients emphasize high-reward candidates. Petersen et al. optimize the expression search distribution, rather than using the neural network as the final predictor.
- **[Neural-guided genetic programming](https://arxiv.org/abs/2111.00053)** — 2021. A neural generator seeds repeated genetic-programming searches and learns from their results. Mundhenk et al. find loosely coupled seeding effective in their benchmarks; the method combines search mechanisms.
- **[Neural Symbolic Regression that Scales](https://arxiv.org/abs/2106.06427)** — 2021. Pretrains a transformer on generated equations and sampled input/output pairs, then uses its predictions to guide equation search. The synthetic equation distribution supplies the learned search prior.
- **[End-to-end symbolic regression](https://arxiv.org/abs/2204.10532)** — 2022. A transformer predicts expressions including numerical constants, optionally followed by constant refinement. Kamienny et al. contrast this with predicting only an expression skeleton.
- **[Equation learning networks](https://arxiv.org/abs/1806.07259)** — 2018. Sahoo et al. use a shallow network with mathematical operations, including division, to identify concise equations. Extrapolation succeeds in studied analytical systems; it must be tested beyond the fitting range.
- **[Φ-SO: dimensional constraints](https://arxiv.org/abs/2303.03192)** — 2023. Generates expressions with consistent physical units during neural-guided search. Tenachi et al. reduce the candidate space through dimensional analysis; unit consistency alone does not establish a correct physical law.
- **[LLM-SR](https://arxiv.org/abs/2404.18400)** — 2024. Uses a language model to propose equation programs, fits their constants to data and evolves the candidates using fit feedback. Scientific descriptions provide prior information beyond numeric samples; the evaluation must distinguish discovery from recall.

## Comparative evidence and evaluation

- **[SRBench findings](https://arxiv.org/abs/2107.14351)** — 2021. Across 252 problems, strong real-data methods combine genetic search with parameter fitting or semantic search. Neural and genetic approaches perform similarly on noisy exact-recovery tasks in this study.
- **[SRSD](https://arxiv.org/abs/2206.10540)** — 2022. Rebuilds physics-formula datasets with realistic variable ranges and adds irrelevant inputs. Matsubara et al. show that sampling and evaluation choices change what a symbolic-regression benchmark measures.
- **[LLM-SRBench](https://proceedings.mlr.press/v267/shojaee25a.html)** — 2025. Uses transformed and synthetic equations to probe discovery beyond recall. It contains 239 problems in four domains; the best tested system reaches 31.5% symbolic accuracy on the transformed-equation track.
- **[Expanded SRBench comparison](https://arxiv.org/abs/2505.03977)** — 2025. Adds methods and measures accuracy, expression size and energy. Some accuracy plots use the best test score across 30 runs: these describe an optimistic search envelope, not performance of a model selected without test labels.
- **[Equation equivalence](https://arxiv.org/abs/2206.10540)**. Evaluate prediction, complexity and symbolic recovery separately. Equivalent algebraic forms need not have identical expression trees; SRSD’s edit-distance metric measures structural similarity, not a general equivalence proof.
- **[Discovery protocol](https://arxiv.org/abs/2107.14351)**. Hold out observations and extrapolation regimes; report noise, operator grammar, constant fitting and total search budget. Compare with conventional regression and test recovery separately when the generating law is known.

## Related topics

[Feature selection](https://mlpapers.org/feature-selection/) · [Neurosymbolic learning](https://mlpapers.org/neurosymbolic-learning/) · [Model predictive control](https://mlpapers.org/model-predictive-control/) · [AutoML](https://mlpapers.org/automl/) · [Interpretability](https://mlpapers.org/interpretability/) · [Evaluation](https://mlpapers.org/evaluation/).
