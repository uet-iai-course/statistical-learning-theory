# Statistical Learning Theory — Detailed lecture-note blueprint

**Audience:** Master's students. **Format:** 10 theory sessions, 150 minutes each. **Core text:** Shai Shalev-Shwartz and Shai Ben-David, *Understanding Machine Learning: From Theory to Algorithms* (UML), 2014.

This is a structure for writing the lecture notes, with proposed theorem statements, proof plans, examples, original exercise prompts, and teaching schedules. It is not a transcription of UML or a claim that every result below appears there. Lectures 1–6 follow its foundational development; Lectures 7–8 combine that foundation with supplementary analysis; Lectures 9–10 introduce extensions. Result labels below are local to these notes, not UML theorem numbers. Reading references use sections rather than edition-dependent page numbers.

## A. Common structure and editorial conventions

Every lecture note should contain the following components, in this order. Insert worked examples between results rather than placing all applications at the end.

1. **Opening question and motivation.** A concrete phenomenon that the lecture will explain; one tempting but incorrect answer.
2. **Learning outcomes.** Three to five observable abilities: define, derive, prove, compute, diagnose, or compare.
3. **Prerequisites and retrieval questions.** Required earlier results and a five-minute check.
4. **Problem setting.** Data, sampling process, learner, objective, comparator, and resources. State what is random.
5. **Notation and assumptions.** Separate statistical assumptions from optimization assumptions.
6. **Running examples.** One small hand-computable example and one realistic application.
7. **Definitions.** Give a formal definition, plain-language interpretation, example, and non-example.
8. **Results.** Use a lemma for a proof tool, a proposition for a focused fact, a theorem for a principal result, and a corollary for an immediate consequence. Do not invent a separate theorem merely to fill a template.
9. **Proofs.** Start with a roadmap; identify the key inequality; annotate where each assumption enters; close with the implication for learning.
10. **Algorithms.** Inputs, initialization, updates, output rule, and stopping criterion; computational cost when relevant.
11. **Worked examples and counterexamples.** Calculate at least one bound and test an assumption by removing it.
12. **Meaning, impact, and limitations.** Explain what the result guarantees, what it does not, and which practical decisions it can inform.
13. **Exercises.** Conceptual, computational, proof, assumption-checking, and optional experimental tasks.
14. **Exit questions and bridge.** A short diagnostic and the unresolved question motivating the next lecture.
15. **Readings.** Required before class, consolidation after class, and optional extension.

### Proof-depth labels

- **[F] Full:** written completely in the notes and proved in class.
- **[S] Sketch:** complete statement, key steps in class, technical details in an appendix or assigned reading.
- **[O] Optional:** enrichment; not assumed in assessment unless explicitly assigned.

For each formal statement include an **assumption box** and a **guarantee box**: expectation or high probability; empirical or population quantity; dependence on sample size, dimension, iterations, confidence, and norms.

### Shared notation

| Symbol | Meaning |
|---|---|
| $Z=(X,Y)$, or $Z=X$ for density estimation | One observation |
| $D$ | Data-generating distribution |
| $S=(Z_1,\ldots,Z_m)\sim D^m$ | Independent training sample, when this assumption applies |
| $\mathcal H$ | Hypothesis class, fixed independently of the sample unless specified |
| $\ell(h,z)$ | Loss |
| $L_D(h)=\mathbb E_D\ell(h,Z)$ | Population risk |
| $L_S(h)=m^{-1}\sum_i\ell(h,Z_i)$ | Empirical risk |
| $A(S)$, $\hat h$ | Learned predictor |
| $\epsilon,\delta$ | Accuracy and failure-probability parameters |
| $d$ | VC dimension; distinguish from feature dimension $p$ |
| $T,\eta_t$ | Optimization iterations and step sizes |
| $G,\beta,\lambda$ | Lipschitz/gradient bound, smoothness constant, regularization strength |

Assume measurability of relevant losses and suprema, or state the standard measurability qualification when discussing arbitrary hypothesis classes. Distinguish an infimum from a minimum; assume attainment only where a chosen optimizer is used.

### Timing and assessment

Each schedule below has 140 instructional minutes plus a 10-minute break. If the institution means 150 teaching minutes excluding breaks, use the extra 10 minutes for a worked exercise. The four recitations and four exams already planned remain separate from these ten lectures; their duration is not assumed here.

## B. Course map

| Lecture | Central question | Principal mathematical outcome | Original image topics |
|---|---|---|---|
| 1 | What does it mean to learn? | Formal risk/PAC framework and an ERM overfitting counterexample | 1, 2 |
| 2 | How much data is enough for finitely many candidates? | Hoeffding + union bound + finite-class ERM guarantee | 2 |
| 3 | How can an infinite class be learnable? | VC dimension, growth function, and a VC generalization bound | 2, 3 |
| 4 | How should model complexity be chosen? | SRM oracle inequality | 5 |
| 5 | How fast can stochastic optimization reduce an objective? | Projected SGD expected convergence bound | 4 |
| 6 | When does optimization become learning? | Fresh-sample learning guarantee and stability of regularized ERM | 4, 5 |
| 7 | How should neural-network complexity be measured? | Norm-controlled linear Rademacher bound; implications for neural networks | 3, 6 |
| 8 | How does the training algorithm affect generalization? | Coupled-run SGD stability bound; nonconvex limitations | 5, 6 |
| 9 | How do we learn distributions and sequences? | Autoregressive likelihood and the ELBO identity | 7, 9 |
| 10 | What changes with interaction and evolving tasks? | REINFORCE derivation; a formal continual-learning evaluation setting | 10, 11 |

Original image topic 8 is the midterm assessment and is outside these ten theory sessions.

## Lecture 1 — Learning setting: risk, ERM, and PAC

### 1.1 Motivation and learning outcomes

**Opening question:** Two classifiers fit every training example. Why might only one predict new examples correctly?

Use a medical screening example with false positives and false negatives to introduce the distinction between a predictor and the loss used to judge it. Then use a deliberately artificial memorization example to isolate the statistical issue.

Students should be able to specify a learning problem, distinguish sample-dependent from fixed quantities, write realizable and agnostic PAC definitions with the correct quantifiers, and explain the role of inductive bias.

**Prerequisites:** expectations, conditional probability, functions and sets. No concentration inequality is required yet.

### 1.2 Problem setting and definitions

Introduce $\mathcal X,\mathcal Y,D,S,\mathcal H,\ell,A$. Start with binary classification and 0–1 loss, then generalize to other losses.

Define population risk, empirical risk, ERM, an approximate ERM, realizability, agnostic learning, excess risk relative to $\mathcal H$, sample complexity, and distribution-free PAC learning. Make clear that realizability is relative to both $D$ and $\mathcal H$.

Write the agnostic target as

$$
\Pr_{S\sim D^m}\!\left[L_D(A(S))\le\inf_{h\in\mathcal H}L_D(h)+\epsilon\right]\ge1-\delta.
$$

Display the quantifier order: there exists a learner and a sample-complexity function such that for every admissible distribution and every accuracy/confidence pair the guarantee holds for sufficiently large samples. Include learner randomness when present.

### 1.3 Proposed results and proofs

**Proposition 1.1 [F]: Unbiasedness for a fixed hypothesis.** For an integrable loss and fixed $h$ independent of $S$, $\mathbb E_S L_S(h)=L_D(h)$.

**Proof plan:** linearity of expectation and identical marginal distributions. Point out that independence is not required for this expectation identity, although it matters later for concentration.

**Counterexample 1.2 [F]: An ERM can generalize maximally badly.** Let $X$ be uniform on $[0,1]$, $Y=1$, and let the class contain all measurable binary classifiers. Choose the ERM that predicts one only at the finitely many observed inputs. Its training loss is zero and its population loss is one.

**Proof plan:** a finite set has probability zero under this input distribution. Contrast this ERM with the constant-one ERM. The example concerns a bad ERM choice in a very rich class, not all ERMs for this particular distribution.

**Proposition 1.3 [O]: Bayes decision rule for 0–1 loss.** If $\eta(x)=\Pr(Y=1\mid X=x)$, a Bayes classifier predicts one when $\eta(x)\ge1/2$. Prove by comparing the two conditional risks. Its role is to distinguish the best member of $\mathcal H$ from the best measurable predictor.

**Corollary:** A small empirical risk alone is not a learning guarantee; some control of the class or algorithm is needed.

### 1.4 Examples, meaning, and impact

- Threshold screening rule: write its domain, labels, loss, and class explicitly.
- Linear regression: change the output space and loss without changing the risk-based framework.
- A noisy classification problem: show why realizability may fail even if the model family is flexible.
- Emphasize that PAC confidence refers to repeated training samples, not a posterior probability that a particular prediction is correct.

### 1.5 Exercises and assessment

1. Specify the full learning setting for spam filtering and temperature prediction. **Target:** distinguish predictors from losses.
2. Give two distinct ERMs for a small threshold dataset. **Target:** explain tie-breaking.
3. Prove Proposition 1.1 and explain why substituting $h=A(S)$ is invalid. **Hint:** the predictor and evaluation sample are dependent.
4. Construct the memorization classifier and compute both risks. **Target:** rigorous use of probability-zero sets.
5. Write the PAC definitions with all quantifiers; explain the difference between $\epsilon$ and $\delta$.

**Exit question:** Which quantity is random in $L_D(A(S))$, even though $D$ is fixed?

### 1.6 Timing, readings, and bridge

**Timing:** motivation 15; setting 25; ERM and examples 30; break 10; PAC definitions 30; counterexample and interpretation 25; exercises/exit 15.

**Required:** UML §§2.1–2.3 and §§3.1–3.2. **Optional:** §5.1 for a later discussion of No Free Lunch; do not treat the memorization example as the full No-Free-Lunch theorem.

**Bridge:** We now know what a guarantee should say. How can probability theory establish one?

## Lecture 2 — Tail bounds and finite-class sample complexity

### 2.1 Motivation and outcomes

**Opening question:** A classifier makes 5% errors on a validation sample. How confident should we be about its population error, and what changes if we selected it from thousands of candidates using that same sample?

Students should derive a finite-class uniform bound, distinguish realizable and agnostic sample-complexity dependence on $\epsilon$, and identify where independence and boundedness are used.

### 2.2 Setting, definitions, and proof tools

Assume $S\sim D^m$, a fixed finite class $\mathcal H$, and losses in $[0,1]$. Define a tail probability, moment-generating function, a uniform-convergence event, and a confidence bound. Separate a preselected $h$ from a sample-selected $\hat h$.

Introduce Markov and Chebyshev as basic tools. Present the Chernoff method: apply Markov to an exponential, factor the moment-generating function using independence, then optimize its parameter.

### 2.3 Main results and proofs

**Lemma 2.1 [S]: Hoeffding's lemma.** For bounded $X\in[a,b]$,
$\mathbb E e^{t(X-\mathbb EX)}\le e^{t^2(b-a)^2/8}$.
Give the argument outline; put the scalar technical inequality in an appendix.

**Theorem 2.2 [F, using Lemma 2.1]: Hoeffding's inequality.** For independent $X_i\in[0,1]$,

$$
\Pr\!\left(\left|\frac1m\sum_i(X_i-\mathbb EX_i)\right|>\epsilon\right)
\le2e^{-2m\epsilon^2}.
$$

**Theorem 2.3 [F]: Finite-class uniform convergence.** With probability at least $1-\delta$, simultaneously for all $h\in\mathcal H$,

$$
|L_D(h)-L_S(h)|\le r_m,
\qquad r_m=\sqrt{\frac{\log(2|\mathcal H|/\delta)}{2m}}.
$$

**Proof:** apply Theorem 2.2 to each fixed hypothesis and union bound over the class. Independence between the different hypotheses' error events is not needed.

**Corollary 2.4 [F]: Agnostic ERM excess risk.** On that event, an exact ERM satisfies
$L_D(\hat h)-\min_hL_D(h)\le2r_m$.
The proof compares population to empirical risk at $\hat h$, uses ERM, then compares empirical to population risk at the class optimum. A sufficient sample size for excess at most $\epsilon$ is
$m\ge2\log(2|\mathcal H|/\delta)/\epsilon^2$.

**Proposition 2.5 [F]: Realizable finite-class bound.** In binary 0–1 classification, every hypothesis with risk above $\epsilon$ is consistent with $m$ samples with probability at most $e^{-m\epsilon}$. Union bound gives the sufficient condition
$m\ge[\log|\mathcal H|+\log(1/\delta)]/\epsilon$
for a consistent ERM. Explain why this argument uses realizability and zero empirical error.

### 2.4 Examples and interpretation

Work out a finite menu of 100 classifiers at confidence 95%; compare the sample requirements for fixed-hypothesis risk estimation, agnostic excess risk, and realizable consistency. Ask what happens when the number of candidates is multiplied by ten.

**Impact:** model search has a statistical cost; the cost here is logarithmic in class size. **Limit:** the bound can be conservative and does not apply directly to unbounded squared error or negative log-likelihood. A data-dependent candidate class needs extra care.

### 2.5 Exercises

1. Prove Markov and derive Chebyshev. **Target:** recognize their weaker assumptions.
2. Derive a one-sided Hoeffding bound using an exponential moment.
3. Explain the factor two in the ERM excess-risk guarantee. **Hint:** two generalization comparisons.
4. Build a counterexample to a purported union bound that omits the number of candidates.
5. Compare analytic bounds with repeated Bernoulli simulations. **Deliverable:** empirical failure probability, not one lucky run.
6. Extension: replace the finite-class count by weights over a countable class; prepare for SRM.

### 2.6 Timing, readings, bridge

**Timing:** motivation 10; Markov/Chebyshev 20; Chernoff/Hoeffding 40; break 10; uniform convergence and ERM 35; realizable case 20; exercise/exit 15.

**Required:** UML Appendix B.1–B.4 and §§4.1–4.2. **Optional:** B.5 for variance-sensitive concentration; not required for the following lecture.

**Bridge:** Linear classifiers form an infinite class. Why can they still generalize?

## Lecture 3 — VC theory and linear classifiers

### 3.1 Motivation and outcomes

An infinite number of thresholds can be specified using real-valued parameters, yet a threshold is intuitively simple. Students should compute VC dimensions with both lower and upper arguments, interpret growth functions, and use a VC generalization bound.

### 3.2 Setting and definitions

Binary classification, 0–1 loss, fixed $\mathcal H$, i.i.d. observations. Define the restriction of $\mathcal H$ to a finite input set, shattering, VC dimension, and growth function
$\Pi_{\mathcal H}(m)=\max_{x_1,\ldots,x_m}|\{(h(x_1),\ldots,h(x_m)):h\in\mathcal H\}|$.
Use feature dimension $p$ and VC dimension $d$ as distinct symbols.

### 3.3 Results and proof plans

**Propositions 3.1–3.3 [F]:** Thresholds on the line have VC dimension one; intervals have VC dimension two; affine halfspaces in $\mathbb R^p$ have VC dimension $p+1$.

For thresholds and intervals, draw shattered sets and exhibit impossible label patterns for larger sets. For halfspaces, fully prove the lower bound on $p+1$ affinely independent points; give the upper bound through Radon's theorem as a sketch, or assign the needed convex-geometry lemma. Distinguish affine from homogeneous halfspaces.

**Lemma 3.4 [S]: Sauer–Shelah.** If $d<\infty$,
$\Pi_{\mathcal H}(m)\le\sum_{j=0}^{d}\binom mj$, where terms above $m$ are zero. For $1\le d\le m$, this is at most $(em/d)^d$.
Explain the induction by separating labelings according to whether both last-coordinate labels occur.

**Theorem 3.5 [S]: A VC uniform-convergence bound.** For $1\le d\le m$, with probability at least $1-\delta$,

$$
\sup_{h\in\mathcal H}|L_D(h)-L_S(h)|
\le C\sqrt{\frac{d\log(em/d)+\log(2/\delta)}m}
$$

for a universal constant $C$. The right-hand side may be clipped at one. This is a valid introductory bound, not a claim of the sharpest rate.

**Proof roadmap:** ghost sample; symmetrization; reduction to label patterns on a combined sample; concentration; Sauer–Shelah. Do not simply union bound over the random labelings on the training sample without the symmetrization argument.

**Corollary 3.6 [F]:** ERM has excess risk at most twice the uniform deviation.

**Fundamental theorem [statement only]:** Under standard measurability qualifications, finite VC dimension characterizes distribution-free PAC learnability for binary classification. Discuss realizable/agnostic and uniform-convergence formulations; defer full necessity and sharp-rate proofs.

### 3.4 Examples, impact, limitations

Compare thresholds, intervals, and planar affine separators. Show that a finite dataset being shattered is a lower-bound witness, not a proof that the VC dimension equals its size.

**Impact:** infinite cardinality is compatible with learnability. **Limit:** VC analysis controls an entire class and can be loose for a particular algorithm or distribution; multiclass problems need other dimensions.

### 3.5 Exercises

1. Compute the growth function of thresholds on distinct ordered points.
2. Prove the VC dimension of intervals using both directions.
3. Prove a lower bound for affine halfspaces using simplex vertices.
4. Compare sample requirements for two given VC dimensions at fixed $\epsilon,\delta$.
5. Explain why parameter count alone does not establish a VC dimension.
6. Optional: complete the Sauer–Shelah induction or the halfspace upper-bound argument.

**Exit question:** What is missing from a proposed proof that only draws a shattered set?

### 3.6 Timing, readings, bridge

**Timing:** motivation/definitions 20; examples 35; growth function 15; break 10; Sauer–Shelah 20; VC theorem/proof roadmap 30; applications/exit 20.

**Required:** UML §§6.1–6.5; §9.1 for linear classifiers. **Optional:** Ch. 28 for advanced proofs. Supply a short Radon-theorem appendix if using it.

**Bridge:** A richer class reduces approximation error but worsens the uniform guarantee. How should we choose among classes?

## Lecture 4 — Error decomposition, SRM, and model selection

### 4.1 Motivation and outcomes

Use degree-1, degree-3, and degree-15 polynomial fits. Students should distinguish approximation, estimation, and optimization effects; derive an SRM oracle inequality; and distinguish this framework from bias–variance decomposition.

### 4.2 Setting and definitions

A countable collection $(\mathcal H_k)_{k\ge1}$, fixed before observing data; nestedness is convenient but not required. Define approximation error relative to a reference optimum $L^*$, estimation error, empirical optimization error, nonuniform learning, and penalized selection.

Define $\operatorname{opt}_S(\tilde h)=L_S(\tilde h)-\inf_{h\in\mathcal H}L_S(h)$. Introduce bias and variance separately for squared-loss regression, where repeated training samples induce variation in the estimator.

### 4.3 Results and proofs

**Proposition 4.1 [F]: A useful error upper bound.** If the uniform deviation on $\mathcal H$ is at most $r$,

$$
L_D(\tilde h)-L^*\le
\underbrace{\inf_{h\in\mathcal H}L_D(h)-L^*}_{\text{approximation}}
+2r+\operatorname{opt}_S(\tilde h).
$$

Prove by adding and subtracting empirical risks. Explain that the statistical term here is a bound, not a literal bias–variance identity.

**Proposition 4.2 [F]: Squared-loss bias–variance identity.** At a fixed input $x$, for an independent test response with conditional mean $f^*(x)$ and variance $\sigma^2(x)$,

$$
\mathbb E_{S,Y\mid x}(\hat f_S(x)-Y)^2
=(\mathbb E_S\hat f_S(x)-f^*(x))^2
+\operatorname{Var}_S(\hat f_S(x))+\sigma^2(x).
$$

Assume finite second moments. Prove by centering around both expectations; cross terms vanish. Do not transfer this exact identity to 0–1 loss.

**Lemma 4.3 [F]: Simultaneous classwise control.** Choose $q_k>0$, $\sum_kq_k\le1$, and classwise radii $p_k=p_k(m,\delta q_k)$. Union bound makes all classwise guarantees hold with probability at least $1-\delta$.

**Theorem 4.4 [F]: SRM oracle inequality.** Suppose $(\hat k,\hat h)$ minimizes $L_S(h)+p_k$ over $k,h\in\mathcal H_k$. On the simultaneous event,

$$
L_D(\hat h)\le\inf_k\left[\inf_{h\in\mathcal H_k}L_D(h)+2p_k\right].
$$

Allow an additive $\tau$ if the penalized optimization is only $\tau$-accurate. Proof chain: upper-bound chosen population risk; invoke penalized empirical optimality; compare the competitor's empirical and population risks.

**Corollary [S]: Validation selection.** For $K$ candidate predictors trained independently of a held-out sample of size $n$, bounded-loss validation selection has excess risk relative to the best candidate at most $2\sqrt{\log(2K/\delta)/(2n)}$. Condition on the training data and use Lecture 2. Adaptive reuse of validation is not covered automatically.

### 4.4 Examples and interpretation

Use a numerical table of empirical risks and penalties to choose a model. Use bounded-loss classification for the formal SRM calculation. If polynomial regression is the motivating example, explicitly add bounded-domain/prediction assumptions or treat it as an illustration rather than an application of the bounded-loss theorem.

**Impact:** a penalty can be derived from a statistical guarantee. **Limit:** an oracle inequality compares with a penalized benchmark, not an omniscient optimum at no cost. Regularization and SRM are related but not identical procedures.

### 4.5 Exercises

1. Prove Proposition 4.1 for an approximate ERM.
2. Derive the bias–variance identity and identify the independent test draw.
3. Use $q_k=6/(\pi^2k^2)$ to obtain the confidence term for each class.
4. Compute an SRM choice from a supplied risk/complexity table.
5. Explain why repeated adaptive tuning on the same validation set is not covered by the simple fixed-menu guarantee.
6. Optional experiment: compare degree selection by training error, a penalty, and held-out validation across repeated samples.

### 4.6 Timing, readings, bridge

**Timing:** motivation 10; error decomposition 25; bias–variance 20; classwise control 15; break 10; SRM proof 30; validation/example 25; exit 15.

**Required:** UML §5.2, §§7.1–7.2, §§11.1–11.2. The pointwise bias–variance derivation is a supplementary explanatory insert. **Optional:** §7.3 on description-length penalties.

**Bridge:** ERM is a statistical principle. How do we approximately optimize it, and what does that cost?

## Lecture 5 — Gradient descent, SGD, and optimization bounds

### 5.1 Motivation and outcomes

A dataset is too large for one full gradient per update. Can one random example still guide progress? Students should derive the projected-SGD bound, explain conditional unbiasedness, and choose a step size from the bound.

### 5.2 Setting and definitions

Minimize a convex function $F$ on a nonempty closed convex set $W$. Assume a minimizer $w^*$ exists and $\|w_1-w^*\|\le R$. At time $t$, the stochastic oracle returns $g_t$ with conditional mean in $\partial F(w_t)$ and conditional second moment at most $G^2$, given the history up to that update.

Define convexity, strong convexity, subgradient, Lipschitz continuity, smoothness, projection, filtration/history, and averaged iterate. Strong convexity and smoothness are extensions, not assumptions for the basic theorem.

### 5.3 Algorithm and mathematical development

Write projected SGD as
$w_{t+1}=\Pi_W(w_t-\eta g_t)$, and output
$\bar w_T=T^{-1}\sum_{t=1}^Tw_t$.
Make the output choice explicit; an averaged-iterate guarantee is not automatically a last-iterate guarantee.

**Lemma 5.1 [S]: Projection inequality.** For $u\in W$, $\|\Pi_W(v)-u\|\le\|v-u\|$. Give the geometric characterization of Euclidean projection.

**Proposition 5.2 [F]: One-step progress.** Expansion of the squared distance gives

$$
\langle g_t,w_t-w^*\rangle\le
\frac{\|w_t-w^*\|^2-\|w_{t+1}-w^*\|^2}{2\eta}
+\frac\eta2\|g_t\|^2.
$$

**Theorem 5.3 [F]: Expected SGD convergence.** Under the stated assumptions,

$$
\mathbb E[F(\bar w_T)-F(w^*)]\le\frac{R^2}{2\eta T}+\frac{\eta G^2}{2}.
$$

**Proof roadmap:** condition on the history; use the subgradient inequality; telescope distances; average; apply Jensen. Mark the role of each assumption in the corresponding step.

**Corollary 5.4 [F]:** With $\eta=R/(G\sqrt T)$, expected suboptimality is at most $RG/\sqrt T$. Therefore $T\ge R^2G^2/\epsilon^2$ suffices for this expected optimization target.

**Proposition 5.5 [O]: Mini-batch variance.** An average of $b$ conditionally independent unbiased gradient estimates has conditional variance divided by $b$, assuming finite variance. Explain why correlated samples need not have this reduction.

### 5.4 Worked example and limits

For bounded-data linear regression, compute a single-example squared-loss gradient and two SGD steps. To invoke the basic theorem, restrict $w$ to a bounded set and bound inputs and targets, or verify an appropriate second-moment condition explicitly. Do not claim squared loss is globally Lipschitz in unconstrained parameters.

**Meaning:** this theorem concerns the objective supplied to the oracle. **Impact:** scalability and a principled step-size trade-off. **Limit:** convexity is essential to the proof of global suboptimality; no population guarantee has yet been established for reuse of a fixed dataset.

### 5.5 Exercises

1. Verify convexity and compute a subgradient of hinge loss.
2. Derive the one-step inequality and identify the projection step.
3. Complete the conditional-expectation part of the SGD proof.
4. Optimize $a/\eta+b\eta$ and interpret the resulting step size.
5. Compare full-batch and mini-batch gradients by both update count and number of examples processed.
6. Optional: demonstrate that a fixed step size can leave an error floor under gradient noise.

### 5.6 Timing, readings, bridge

**Timing:** regression example 15; prerequisites 25; one-step inequality 30; break 10; SGD proof 35; step size/mini-batch 20; exercises/exit 15.

**Required:** UML §9.2, §§12.1–12.2, §§14.1–14.3. **Optional:** §14.4 and §12.3 for variants and surrogate losses.

**Bridge:** What is the stochastic oracle estimating: the empirical objective or the population objective?

## Lecture 6 — From stochastic optimization to learning: regularization and stability

### 6.1 Motivation and outcomes

Compare two programs: one draws a fresh training observation at every step; the other performs many epochs over one stored sample. Their updates may look alike, but their immediate mathematical targets differ.

Students should derive a fresh-sample population-risk guarantee, distinguish it from fixed-sample optimization, and explain how regularization can stabilize a learning rule.

### 6.2 Setting and definitions

Setting A: $F(w)=\mathbb E_Z\ell(w,Z)$, with independent fresh observations; impose conditions allowing the stochastic subgradient to have the required conditional mean.

Setting B: $F_S(w)=L_S(w)$, with indices sampled from a fixed training set. Conditional on $S$, the stochastic oracle is unbiased for the empirical objective.

Define regularized ERM, neighboring samples differing in one observation, uniform stability, expected generalization gap, and the difference between expected and high-probability guarantees. UML's stability development includes its own stability formulations; the uniform-stability formulation below is a convenient course convention for connecting Lectures 6 and 8.

### 6.3 Results and proof plans

**Corollary 6.1 [F]: Fresh-sample learning via SGD.** Apply Theorem 5.3 to $F=L_D$. Under the same convexity and gradient assumptions,
$\mathbb E[L_D(\bar w_T)]-\inf_{w\in W}L_D(w)\le RG/\sqrt T$.
Explain that sample usage here is $T$ fresh observations; the rate does not automatically describe $T$ updates on $m$ reused examples.

**Proposition 6.2 [F]: Fixed-sample optimization is not itself learning.** Add and subtract empirical risks to expose a generalization term, optimization term, and comparator term. Use an independent test expectation when discussing population performance.

**Theorem 6.3 [F]: Stability controls expected generalization.** If replacing one observation changes the algorithm's expected test loss by at most $\beta_m$, uniformly over neighboring samples and test observations, then
$|\mathbb E_{S,A}[L_D(A(S))-L_S(A(S))]|\le\beta_m$, assuming integrability.

**Proof roadmap:** introduce an independent replacement observation; exchange its role with a training observation; compare the two neighboring-sample outputs; average over indices. Do not misstate this as a bound on the expected absolute gap.

**Proposition 6.4 [S]: Stability of strongly convex regularized ERM.** Let the per-example loss be convex and $G$-Lipschitz on a convex domain. For

$$
\hat w_S=\arg\min_{w\in W}\left[L_S(w)+\frac\lambda2\|w\|^2\right],\quad\lambda>0,
$$

the difference between neighboring solutions is at most $2G/(\lambda m)$, and uniform loss stability is at most $2G^2/(\lambda m)$, assuming minimizers exist.

**Proof plan:** write strong-convexity inequalities for the two empirical objectives, add them, cancel unchanged terms, and apply Lipschitzness twice.

**Corollary 6.5 [S]: Comparator trade-off.** For any $u\in W$,

$$
\mathbb E L_D(\hat w_S)-L_D(u)
\le\frac{2G^2}{\lambda m}+\frac\lambda2\|u\|^2.
$$

Use empirical regularized optimality, the stability theorem, and unbiasedness at fixed $u$. This explains a regularization trade-off; it does not imply that more regularization always helps.

### 6.4 Examples and impact

Use ridge regression to visualize changes after replacing one point. State boundedness/domain restrictions before invoking a global Lipschitz constant. Compare two-dimensional contours for small and large $\lambda$.

**Impact:** generalization can depend on the learning procedure rather than only the cardinality of the hypothesis class. **Limit:** the guarantee above is in expectation, requires its assumptions, and does not directly explain every deep-network training procedure.

### 6.5 Exercises

1. Identify the conditional target of the gradient in fresh-sample and fixed-sample SGD.
2. Complete the replace-one proof of expected generalization.
3. Derive the solution-distance bound for regularized ERM.
4. Minimize the comparator upper bound over $\lambda$ for a known $\|u\|\le B$.
5. Explain why ridge regression with arbitrary unbounded data needs additional analysis.
6. Experiment: replace one observation and measure changes in predictions as regularization varies; report both sensitivity and error.

### 6.6 Timing, readings, bridge

**Timing:** two sampling settings 25; fresh-sample corollary 20; regularization example 25; break 10; stability definition/theorem 30; regularized-ERM analysis 25; interpretation/exit 15.

**Required:** UML §14.5 and §§13.1–13.3. **Optional:** §13.4. A course appendix should spell out the chosen uniform-stability convention and its relation to the text's formulation.

**Bridge:** Large neural networks can fit arbitrary training labels. Which complexity measures remain informative?

## Lecture 7 — Neural networks, capacity, and overparameterization

### 7.1 Motivation and outcomes

Show two training curves with near-zero training error: one network uses genuine labels; another uses randomly permuted labels. Ask why the test behavior differs even when architecture and parameter count match.

Students should distinguish expressivity, statistical capacity, and optimization; compute a simple Rademacher complexity; and explain why norm and margin control can convey information beyond parameter count.

### 7.2 Setting and definitions

Define a feedforward network, depth, width, activation, score function, classification margin, and overparameterization relative to a specified sample/task. Separate architecture-level classes from norm-constrained subclasses and the particular model selected by training.

For $\mathcal F$ and fixed inputs $x_{1:m}$, define

$$
\widehat{\mathfrak R}_S(\mathcal F)
=\mathbb E_\sigma\sup_{f\in\mathcal F}\frac1m\sum_{i=1}^m\sigma_i f(x_i),
$$

where independent Rademacher signs take values $\pm1$ with equal probability. Also define population Rademacher complexity as expectation over the sample. Clarify that a generalization theorem applies to the loss class, not automatically to raw network scores.

### 7.3 Results and proof plans

**Example/proposition 7.1 [F]: A ReLU network represents XOR on the four Boolean inputs.** Use the score $\operatorname{ReLU}(x_1+x_2)-2\operatorname{ReLU}(x_1+x_2-1)$ on $\{0,1\}^2$, thresholded at $1/2$. Verify all four values. This establishes a small expressivity fact, not a generalization theorem.

**Theorem 7.2 [S]: Empirical Rademacher generalization bound.** For a fixed measurable class $\mathcal G$ of losses taking values in $[0,1]$, with probability at least $1-\delta$, simultaneously for $g\in\mathcal G$,

$$
\mathbb E g(Z)\le\frac1m\sum_i g(Z_i)
+2\widehat{\mathfrak R}_S(\mathcal G)
+3\sqrt{\frac{\log(2/\delta)}{2m}}.
$$

**Proof roadmap:** ghost sample; symmetrization with random signs; bounded-difference concentration. Supply the bounded-difference lemma in an appendix, rather than claiming the result follows directly from fixed-function Hoeffding.

**Proposition 7.3 [F]: Linear norm-bounded complexity.** If $\mathcal F_B=\{x\mapsto\langle w,x\rangle:\|w\|_2\le B\}$ and $\|x_i\|_2\le R_x$, then

$$
\widehat{\mathfrak R}_S(\mathcal F_B)
\le\frac{B}{m}\sqrt{\sum_i\|x_i\|_2^2}
\le\frac{BR_x}{\sqrt m}.
$$

**Proof:** dual norm; Jensen/Cauchy–Schwarz; cancellation of cross terms under the random signs.

**Corollary 7.4 [S]: Margin-control interpretation.** A bounded ramp loss with margin scale $\gamma>0$ is $1/\gamma$-Lipschitz. A contraction argument connects its complexity to score complexity, yielding a penalty of order $BR_x/(\gamma\sqrt m)$ in the linear case. State the contraction lemma and any centering convention before using it.

**Supplement [statement and discussion]:** A neural-network norm–margin bound can be presented as an advanced example. Do not replace its architecture-, depth-, and norm-dependent terms by the linear bound above.

### 7.4 Meaning, impact, and counterexamples

Universal approximation is a statement about existence of representations, not sample complexity or successful training. A vacuous bound is an uninformative certificate, not evidence that the model necessarily fails to generalize.

Discuss how rescaling adjacent layers in a positively homogeneous network can preserve the represented function while changing some parameter norms. Complexity measures require careful interpretation.

### 7.5 Exercises

1. Verify the XOR construction and compare with an affine classifier.
2. Compute empirical Rademacher complexity for a singleton class and interpret its expectation over signs.
3. Prove the linear norm bound.
4. Explain why $p\gg m$ alone does not determine the observed test error.
5. Show that an approximation theorem cannot establish that SGD finds a good network.
6. Experiment: genuine versus random labels; measure train/test error and normalized margins across seeds. Treat this as evidence, not proof.

### 7.6 Timing, readings, bridge

**Timing:** motivation 15; network/expressivity 25; capacity limitations 20; Rademacher definition 10; break 10; linear proof 30; generalization/margin interpretation 25; exit 15.

**Required:** UML §§20.1–20.5 and §§26.1–26.2, selectively. **Optional:** §26.3 for the margin connection; Bartlett, Foster, and Telgarsky (2017), *Spectrally-normalized margin bounds for neural networks*, theorem statement and discussion only.

**Bridge:** A class-based measure does not fully describe which predictor training selects. Can the trajectory of SGD help?

## Lecture 8 — SGD stability and generalization in deep learning

### 8.1 Motivation and outcomes

Train the same architecture for different numbers of steps. Training error may decrease while a generalization bound worsens. Students should derive a coupled-run stability estimate in a smooth convex setting and distinguish its implications from nonconvex optimization and empirical deep-learning behavior.

### 8.2 Setting and definitions

Use fixed-sample SGD with indices sampled independently and uniformly with replacement from $\{1,\ldots,m\}$. Couple two runs on neighboring datasets using the same initialization and index sequence. Define $\Delta_t=\|w_t-w'_t\|$, smoothness $\beta$, loss Lipschitz constant $G$, and the cumulative step-size budget.

The core proof assumes convex, differentiable, $\beta$-smooth, $G$-Lipschitz per-example losses on a domain where the updates and required gradient-map property are valid. State an unconstrained version for simplicity; constrained extensions need appropriate projection/domain conditions.

### 8.3 Main results and proofs

**Lemma 8.1 [S]: Nonexpansive gradient step.** For a convex $\beta$-smooth function and $0\le\eta\le2/\beta$, the map $w\mapsto w-\eta\nabla\ell(w,z)$ is nonexpansive. Derive from gradient co-coercivity; place its proof in the appendix.

**Proposition 8.2 [F]: Coupled-run recurrence.** Since the differing observation is selected with probability $1/m$,

$$
\mathbb E\Delta_{t+1}\le\mathbb E\Delta_t+\frac{2G\eta_t}{m}.
$$

**Proof:** condition on whether the selected index is the differing one. For a shared observation use Lemma 8.1; for the differing observation insert an intermediate gradient step and bound the extra displacement.

**Theorem 8.3 [F]: A smooth-convex SGD stability bound.** With $\Delta_0=0$,

$$
\epsilon_{\mathrm{stab}}\le\frac{2G^2}{m}\sum_{t=0}^{T-1}\eta_t.
$$

Use Lipschitzness of test loss and Lecture 6 to obtain the expected-generalization consequence. This is an algorithm-dependent bound for a stated SGD sampling rule, not a universal statement about all optimizers or epochs.

**Corollary [F]:** Constant step size gives a bound proportional to $\eta T/m$. Compare its trend with the optimization error from earlier lectures. This motivates a trade-off; it does not prove that earlier stopping always improves actual test error.

**Nonconvex extension [S]:** Without convexity, a smooth gradient step can expand distances by a factor up to $1+\beta\eta_t$. Explain how products of these factors complicate the coupling argument. Refer to supplementary results for refined rates rather than reusing the convex formula.

**Optional optimization appendix [O]:** For a lower-bounded $\beta$-smooth nonconvex $F$, unbiased gradients with variance at most $\sigma^2$, and $\eta\le1/\beta$, derive
$T^{-1}\sum_t\mathbb E\|\nabla F(w_t)\|^2\le2(F(w_0)-F_*)/(\eta T)+\beta\eta\sigma^2$.
This controls stationarity, not global excess risk or generalization.

### 8.4 Practical meaning and scope

Discuss early stopping, step sizes, and algorithmic sensitivity. Introduce implicit regularization as selection behavior induced by training, and distinguish it from explicit regularization and from a proved theorem.

Standard ReLU networks are not globally smooth in their parameters, and unrestricted networks do not automatically have uniform Lipschitz constants. Applying the smooth-convex theorem literally to them is invalid. The deep-learning discussion should separate rigorous special cases, supplementary nonconvex theory, and empirical hypotheses.

### 8.5 Exercises

1. Prove the coupled-run recurrence and identify the factor $1/m$.
2. Compare the cumulative step-size budgets of constant and $1/t$ schedules.
3. Identify the exact failed step if convexity is removed.
4. Explain the difference between small gradient norm, small empirical loss, and small population risk.
5. Audit a theorem's assumptions for a supplied ReLU training setup.
6. Experiment: compare runs on neighboring datasets over time; report prediction sensitivity and test error without equating either curve to a theorem bound.

### 8.6 Timing, readings, bridge

**Timing:** motivation/coupling 20; nonexpansiveness 20; recurrence 30; break 10; stability theorem/interpretation 30; nonconvex limitations 25; exit 15.

**Required:** UML Ch. 13 and §20.6 as background; Hardt, Recht, and Singer (2016), smooth-convex argument and selected discussion. **Optional:** its nonconvex analysis; the stationarity appendix above; UML Ch. 31 as a separate future route, not part of this lecture's required proofs.

**Bridge:** The same risk language can describe probability models. What changes when an example is a sequence or the loss is log-likelihood?

## Lecture 9 — Sequence learning and generative models

### 9.1 Motivation and outcomes

Predicting a label and learning to generate a sentence appear different. Connect them through conditional distributions and expected loss.

Students should factor a sequence distribution, derive the maximum-likelihood objective, distinguish sequence-level independence from token-level dependence, and derive an ELBO. Architectures are examples; full Transformer, GAN, and diffusion training are outside scope.

### 9.2 Settings and definitions

**Setting A:** Independent sequences $X^{(1)}_{1:T_1},\ldots,X^{(m)}_{1:T_m}$, with dependence allowed inside a sequence. The i.i.d. observation is the sequence.

**Setting B:** A single time series, from which overlapping windows are extracted. The windows are generally dependent. Earlier i.i.d. bounds do not apply unchanged; formal dependent-data guarantees require additional assumptions and tools.

Define autoregressive factorization, conditional likelihood, negative log-likelihood, teacher forcing, latent-variable model $p_\theta(x,z)$, variational distribution $q_\phi(z\mid x)$, KL divergence, and evidence lower bound. Distinguish total sequence loss from length-normalized loss; they weight variable-length sequences differently.

### 9.3 Results and proofs

**Proposition 9.1 [F]: Chain-rule factorization.**
$p_\theta(x_{1:T})=\prod_{t=1}^T p_\theta(x_t\mid x_{<t})$.
Taking negative logs gives the tokenwise training objective. Explain that this is a probability identity; choosing a finite context or a particular architecture is an additional modeling restriction.

**Proposition 9.2 [F]: Population log-loss and KL.** For a discrete true distribution $p$ and model $q$, with suitable support and finite terms,
$\mathbb E_p[-\log q(X)]=H(p)+D_{\mathrm{KL}}(p\|q)$.
Give the algebraic proof. For continuous models, use densities and state the integrability requirements; differential entropy differs from discrete entropy.

**Corollary:** Population maximum likelihood minimizes forward KL within the model class. This is not a finite-sample generalization guarantee, nor a guarantee that perceptual sample quality is optimized.

**Theorem 9.3 [F]: ELBO identity.** When the densities and expectations are well defined,

$$
\log p_\theta(x)=\mathcal L(\theta,\phi;x)
+D_{\mathrm{KL}}(q_\phi(z\mid x)\|p_\theta(z\mid x)),
$$

where
$\mathcal L=\mathbb E_q[\log p_\theta(x,z)-\log q_\phi(z\mid x)]$.

**Proof:** expand the KL using Bayes' rule and rearrange. Nonnegativity yields the lower bound; equality holds when the approximate posterior equals the true posterior almost everywhere.

**Proposition 9.4 [S]: Reparameterized gradient.** For Gaussian $q_\phi$, write $z=\mu_\phi(x)+\sigma_\phi(x)\odot\varepsilon$, $\varepsilon\sim N(0,I)$. Under conditions allowing differentiation through the expectation, derive a pathwise gradient estimator. Do not claim unbiasedness without those conditions.

### 9.4 Examples, meaning, and impact

Compute likelihood for a three-token sequence using a small conditional-probability table. Work a Bernoulli maximum-likelihood example. Use a one-dimensional latent Gaussian example to identify reconstruction and KL terms in an ELBO.

**Impact:** connects ERM, probabilistic modeling, representation learning, and stochastic optimization. **Limits:** log-loss is generally unbounded; nearby tokens are not automatically independent examples; high likelihood and visually convincing samples measure different properties. Mention GANs and diffusion only as alternative objectives/models in a brief optional comparison.

### 9.5 Exercises

1. Compute sequence likelihood and average token NLL from a table.
2. Explain why random splitting of overlapping windows can leak information.
3. Derive the cross-entropy/KL identity and state support assumptions.
4. Derive the ELBO and its equality condition.
5. Compare token-weighted and sequence-weighted objectives for two different sequence lengths.
6. Optional: train a tiny bigram model; compare held-out NLL with generated samples. Avoid requiring large-model training.

### 9.6 Timing, readings, bridge

**Timing:** settings 20; autoregression/example 30; likelihood/KL 20; break 10; latent variables/ELBO 35; reparameterization/model comparison 20; limits/exit 15.

**Required:** UML §24.1 and selected parts of §24.4 for likelihood and latent variables. **Supplement:** Kingma and Welling, *Auto-Encoding Variational Bayes*, for the variational objective and reparameterization. RNN/Transformer and modern generative-model material is supplementary, not attributed to UML's latent-variable chapter.

**Bridge:** What if the learner controls how data are collected, or the distribution changes as learning proceeds?

## Lecture 10 — Policy-gradient reinforcement learning and continual learning

### 10.1 Motivation and outcomes

Use two examples: a robot whose actions determine its future observations; and a classifier trained successively on different environments. Both challenge the fixed-distribution supervised-learning setup, for different reasons.

Students should derive a basic REINFORCE estimator, justify an action-independent baseline, specify a continual-learning protocol, and identify why a static supervised guarantee does not directly settle these problems.

### 10.2 Part A: Policy-gradient setting and definitions

Use a finite-horizon MDP with horizon $H$, fixed initial-state distribution and transition law independent of $\theta$, differentiable stochastic policy $\pi_\theta(a\mid s)$, trajectory $\tau$, and return $R(\tau)=\sum_{t=0}^{H-1}r_t$. The objective is $J(\theta)=\mathbb E_{\tau\sim p_\theta}R(\tau)$.

State sufficient support/differentiability/integrability conditions for exchanging derivative and expectation. Start with undiscounted finite horizon to avoid silently mixing incompatible discounted-return conventions.

### 10.3 RL results and proof plans

**Lemma 10.1 [F]: Score identity.** $\nabla_\theta p_\theta(\tau)=p_\theta(\tau)\nabla_\theta\log p_\theta(\tau)$ on the relevant support, and the expected score is zero under regularity conditions.

**Theorem 10.2 [F]: Trajectory REINFORCE identity.**

$$
\nabla J(\theta)=\mathbb E\left[R(\tau)\sum_{t=0}^{H-1}\nabla_\theta\log\pi_\theta(A_t\mid S_t)\right].
$$

**Proof:** differentiate the trajectory expectation; use the score identity; factor the trajectory probability; initial-state and transition terms have zero parameter derivative under the setting above.

**Proposition 10.3 [S]: Reward-to-go.** Earlier rewards make zero expected contribution to a later action's score. Replace total return in the term at time $t$ by $G_t=\sum_{u=t}^{H-1}r_u$. Prove by conditioning on the history before action $t$.

**Corollary 10.4 [F]: Baseline invariance.** Subtracting a baseline $b_t(S_t)$ independent of the sampled action conditional on the state preserves the gradient expectation. Prove using $\sum_a\pi_\theta(a\mid s)\nabla\log\pi_\theta(a\mid s)=0$.

Explain that an arbitrary baseline need not reduce variance; a well-chosen one can. If a parameterized baseline shares parameters, the policy-gradient estimator must treat it appropriately rather than differentiating the whole product as though it were the original objective.

**Worked example:** two-action bandit, sigmoid policy, fixed action rewards. Compute the exact derivative of expected reward and match it to the score-function estimator.

### 10.4 Part B: Continual-learning setting and definitions

Specify a sequence of tasks/distributions $D_1,\ldots,D_K$, model parameters $w_k$, memory budget, access to old data, and whether task identity is available at inference. Define catastrophic forgetting, forward/backward transfer, replay, parameter regularization, and the stability–plasticity trade-off.

Separate three concepts: online learning concerns sequential decisions/updates and often regret; continual learning concerns accumulating competence across changing tasks; distribution shift concerns a mismatch between data-generating distributions. They overlap but are not synonyms.

Define an evaluation matrix $a_{t,i}$: test performance on task $i$ after training through task $t$. Report final average accuracy $K^{-1}\sum_i a_{K,i}$, backward transfer relative to $a_{i,i}$, and a nonnegative peak-to-final forgetting measure using $\max_{i\le t\le K}a_{t,i}-a_{K,i}$ for past tasks. State the convention because papers use different metrics.

### 10.5 Continual-learning propositions and meaning

**Proposition 10.5 [F]: Conflicting tasks can force a trade-off.** Let $L_A(w)=w^2/2$ and $L_B(w)=(w-1)^2/2$. Task A is minimized at zero, task B at one. Optimizing only B raises A's loss from zero to one half.

With the illustrative objective $L_B(w)+\lambda w^2/2$, the minimizer is $w=1/(1+\lambda)$. Derive the solution and interpret the trade-off. This is a transparent toy calculation, not a theorem that a particular neural continual-learning method always prevents forgetting.

Introduce EWC as an optional, parameter-importance-weighted quadratic penalty motivated by an approximation, and replay as training on a mixture including retained past examples. Finite replay approximates a chosen historical mixture; it is not identical to having all past data.

**Important conclusion:** static regret against one fixed comparator need not guarantee low forgetting on every earlier task. Do not invent a universal continual-learning theorem for this introductory session.

### 10.6 Exercises, impact, and limitations

1. Derive REINFORCE for the two-action bandit and compare with direct differentiation.
2. Prove baseline invariance; give an action-dependent baseline for which the simple cancellation fails.
3. Identify why Lecture 5's convex convergence theorem cannot be applied directly to arbitrary policy optimization.
4. Compute average accuracy, backward transfer, and forgetting from a supplied evaluation matrix.
5. Solve the two-task quadratic example for three regularization strengths.
6. Design a task-order and memory-controlled comparison of fine-tuning and replay; specify held-out tests and leakage controls.

**Impact:** extends the statistical-learning vocabulary to interaction and evolving data. **Limits:** policy gradients can have high variance and nonconvex objectives; continual-learning performance depends on task protocol, resources, and evaluation. Neither is fully covered by UML's online-learning chapter.

### 10.7 Timing, readings, and closing synthesis

**Timing:** RL setting 15; REINFORCE proof 30; baseline/bandit 25; break 10; continual setting 20; quadratic example and methods 25; evaluation/synthesis 25.

**Required supplementary reading:** Sutton and Barto, *Reinforcement Learning: An Introduction*, 2nd edition, Chapter 13, selectively. **UML bridge:** §§21.1–21.3 for online learning terminology and regret. **Optional:** Kirkpatrick et al. (2017), *Overcoming catastrophic forgetting in neural networks*, for EWC's motivation and method.

**Closing exercise:** For supervised classification, density estimation, policy optimization, and continual learning, list the data-generating process, objective, comparator, random quantities, and the assumption from Lectures 1–8 that needs to be changed.

## C. Recitation and assessment alignment

| Separate session | Core tasks | Proof standard | Assessment focus |
|---|---|---|---|
| Recitation 1, after Lectures 1–2 | Specify settings; concentration calculations; finite-class ERM proof | Reconstruct short proofs without notes | Correct quantifiers, independence, boundedness, and sample complexity |
| Exam 1 | Learning setting and tail bounds | One short proof plus an application | Distinguish fixed and data-selected hypotheses |
| Recitation 2, after Lectures 3–4 | VC lower/upper bounds; SRM penalty and model choice | Proof plus assumption checking | Both directions of VC calculations and valid classwise confidence allocation |
| Exam 2 / midterm | VC theory and SRM, using earlier concentration tools | One VC argument and one SRM derivation | Separate approximation, estimation, and optimization |
| Recitation 3, after Lectures 5–6 | Telescope the SGD inequality; fresh versus reused data; stability | Complete the main expected-value arguments | Name the objective and the expectation in every guarantee |
| Exam 3 | SGD convergence and learning guarantees | Derivation, parameter choice, and diagnosis | Do not confuse optimization with generalization |
| Recitation 4, after Lectures 7–8 | Linear Rademacher proof; coupled SGD; neural-network assumption audit | Reproduce basic proof, interpret advanced statements | Capacity-based versus algorithm-dependent reasoning |
| Exam 4 | Deep-learning theory synthesis | Open-book statement interpretation is suitable | Identify missing assumptions and distinguish theorem from experiment |

For Lectures 9–10, use short derivations and reading responses unless the course assessment policy requires an additional test. Do not silently add another exam to the agreed structure.

## D. Required proof spine and optional appendices

**Core proofs students should be able to reconstruct:** fixed-hypothesis unbiasedness; finite-class concentration/ERM; threshold and interval VC dimensions; SRM oracle inequality; the SGD telescoping proof; expected generalization from stability; linear Rademacher complexity; smooth-convex coupled SGD recurrence; autoregressive/KL/ELBO identities; REINFORCE and baseline invariance.

**Proofs for sketches or appendices:** Hoeffding's scalar lemma; Radon's theorem; Sauer–Shelah induction; full VC symmetrization; bounded differences for Rademacher analysis; contraction; smooth-gradient co-coercivity; detailed nonconvex SGD stability; sharp neural-network capacity/margin bounds.

**Optional technical appendices:** measure-theoretic qualifications; differentiation under an expectation; strongly convex SGD variants; high-probability versus expected stability bounds; nonconvex stationarity; dependent-data concentration; online-to-batch conversion; PAC-Bayes. Keep these out of mandatory exams unless explicitly taught.

## E. Authoring and quality checklist

- Use one notation table across all ten notes. Avoid reusing $d$ for feature dimension and VC dimension in the same calculation.
- Each theorem names the sampling scheme, loss assumptions, comparator, source of randomness, and type of guarantee.
- Every proof annotation points to the assumption being used; include at least one failure example per lecture.
- Label results as course formulations; cite UML by verified section and avoid unverified theorem numbers.
- Distinguish a model-class guarantee from a guarantee for one training algorithm.
- State whether the guarantee controls risk, excess risk, optimization gap, expected generalization, stationarity, regret, or forgetting.
- Do not transfer bounded-loss results to squared loss or log-loss without checking assumptions.
- Do not transfer convex optimization bounds to neural networks or RL without an appropriate new argument.
- Include one numerical worked example and one exit question in each note.
- Separate original exercise prompts from exercises selected from the textbook; do not invent UML exercise numbers.
- Keep long technical proofs in appendices so the 150-minute teaching plan remains feasible.
- Every empirical illustration uses a held-out protocol and multiple runs where randomness matters; empirical curves are not proofs.

## F. Reading register

1. **UML:** Shai Shalev-Shwartz and Shai Ben-David, *Understanding Machine Learning: From Theory to Algorithms* (2014). [Author's book page](https://www.cs.huji.ac.il/~shais/UnderstandingMachineLearning/). [Publisher's table of contents](https://assets.cambridge.org/97811070/57135/toc/9781107057135_toc.pdf). Use the section-level assignments above; page numbers can differ across versions.
2. **SGD stability:** Moritz Hardt, Ben Recht, and Yoram Singer (2016), [*Train faster, generalize better: Stability of stochastic gradient descent*](https://proceedings.mlr.press/v48/hardt16.html). Lecture 8 supplement.
3. **Neural margin bounds:** Peter L. Bartlett, Dylan J. Foster, and Matus Telgarsky (2017), [*Spectrally-normalized margin bounds for neural networks*](https://proceedings.neurips.cc/paper_files/paper/2017/hash/b22b257ad0519d4500539da3c8bcf4dd-Abstract.html). Optional Lecture 7 statement-level reading.
4. **Variational generative modeling:** Diederik P. Kingma and Max Welling, [*Auto-Encoding Variational Bayes*](https://arxiv.org/abs/1312.6114). Lecture 9 supplement.
5. **Policy gradients:** Richard S. Sutton and Andrew G. Barto (2018), *Reinforcement Learning: An Introduction*, 2nd edition, Chapter 13. [Author-hosted book draft](https://www.incompleteideas.net/book/bookdraft2018mar21.pdf). Lecture 10 supplement.
6. **Continual learning:** James Kirkpatrick et al. (2017), [*Overcoming catastrophic forgetting in neural networks*](https://doi.org/10.1073/pnas.1611835114). Optional Lecture 10 method discussion.

The course organization, examples, local result numbering, exercise prompts, teaching schedules, and proof-depth decisions in this blueprint are instructional proposals. Supplementary topics should retain their explicit source labels when the full lecture notes are written.
