# Phân tích nguồn UML — Bài 01 (báo cáo của tác tử phân tích nguồn, 2026-10-30)

Tệp nội bộ. Báo cáo gốc bằng tiếng Anh; điều phối viên đã chấp nhận với các quyết định ghi trong `review-log.md`. Số trang là trang của tệp PDF UML.

## 1. Blueprint items against UML

| Blueprint item | Where UML covers it | How UML states it | Differences from blueprint / delicate points |
|---|---|---|---|
| Setting $\mathcal X,\mathcal Y,D,S,\mathcal H,\ell,A$ | §2.1, pp. 33–35; joint $D$ only in §3.2.1, p. 45 | Ch. 2: $D$ over $\mathcal X$ plus unknown labelling $f$, $y_i=f(x_i)$; binary labels only. Training data is a *sequence* (fn. 1, p. 34). $A(S)$ introduced p. 34. | Blueprint starts with joint $D$ on $\mathcal X\times\mathcal Y$; UML switches $L_{(D,f)}\to L_D$ in Ch. 3 — the note can avoid that. "Fixed vs random" only briefly (p. 38: $L(h_S)$ is a random variable). |
| i.i.d. | §2.3.1, p. 38 | $S\sim D^m$, an explicit assumption | same |
| Population risk | Eq. (2.1) p. 34 (0–1, realizable); Eq. (3.1) p. 45 (joint $D$); general loss Eq. (3.3) p. 48 | $\ell:\mathcal H\times Z\to\mathbb R_+$, nonnegative, **not bounded**, no integrability condition | Note must add integrability (e.g. squared loss). Measurability: fn. 2 p. 34, Remark 3.1 p. 49 assume each $\ell(h,\cdot)$ measurable. **UML does not discuss measurability of $S\mapsto L_D(A(S))$**, which the event in $\Pr_S[\cdot]$ needs. |
| Empirical risk | Eq. (2.2) p. 35; Eq. (3.4) p. 48 | $L_S(h)$ is the risk under the uniform distribution on $S$ (p. 46) | same |
| ERM | §2.2 p. 35 (unrestricted); $\mathrm{ERM}_{\mathcal H}(S)\in\arg\min$, §2.3 pp. 36–37 | "$\in$" = a selection; tie-breaking implicit ("may be chosen by an ERM", p. 36); Cor. 2.3 "for every ERM hypothesis" (p. 41) | UML never discusses tie-breaking or nonemptiness of argmin. **For 0–1 loss $L_S\in\{0,1/m,\dots,1\}$, so argmin is non-empty for every $\mathcal H$**; for squared loss it can be empty → motivates approximate ERM. |
| Approximate ERM | **Not in UML Ch. 2–3** (phrase first appears p. 152, §11.3) | — | Course addition. Suggested: $L_S(A(S))\le\inf_{\mathcal H}L_S+\epsilon_{\rm opt}$ for every $S$ (or w.p. over $S$ and internal randomness). |
| Realizability | Def. 2.1 p. 38: $\exists h^\star\in\mathcal H$, $L_{(D,f)}(h^\star)=0$; Def. 3.1 p. 43 "with respect to $\mathcal H,D,f$"; restated p. 45 | fn. 3 p. 38: then $L_S(h^\star)=0$ with probability 1 | **Property of the pair $(D,\mathcal H)$**. Joint-$D$ form: $\exists h^\star\in\mathcal H$ with $L_D(h^\star)=0$ (forces deterministic labels $D$-a.s.). Attained $\min=0$ ≠ $\inf=0$: e.g. $D_X=U[0,1]$, $f=1[x>1/2]$, $\mathcal H=\{1[x\ge 1/2+1/n]\}$ has risks $1/n$, infimum 0 never attained. The manual's Ex. 3.6 solution silently uses the inf version. |
| Agnostic learning | §3.2.1 pp. 45–47; Def. 3.3 p. 46 (0–1); Def. 3.4 p. 49 (general loss) | Target $L_D(h)\le\min_{h'\in\mathcal H}L_D(h')+\epsilon$; Def. 3.4 requires output in $\mathcal H$; Remark 3.2 p. 49 improper learning | **UML writes min, blueprint writes inf**: keep inf and explain. Fix the convention $A(S)\in\mathcal H$ (proper) or not. |
| Excess risk relative to $\mathcal H$ | Not named in Ch. 2–3; implicit in Defs 3.3/3.4; §5.2 p. 64 calls $L_D(h_S)-\min_{\mathcal H}L_D$ "estimation error"; fn. 1 p. 64 on Bayes-relative usage | — | Course definition. Separate from excess over Bayes (Prop. 1.3's purpose). Avoid "estimation error" until Lecture 4. |
| Sample complexity | p. 44 | $m_{\mathcal H}:(0,1)^2\to\mathbb N$, the *minimal* function; guarantee for **all** $m\ge m_{\mathcal H}$ | Separate learner's $m_A$ from class's $m_{\mathcal H}$; for an arbitrary learner a guarantee at one $m$ need not hold at larger $m$, hence "for all $m\ge$". Ex. 3.1 uses minimality. |
| Distribution-free PAC; quantifier order | Def. 3.1 p. 43; Def. 3.3 p. 46; Def. 3.4 p. 49 | $\exists m_{\mathcal H}\ \exists A\ \forall\epsilon,\delta\in(0,1)\ \forall D$ ($\forall f$ realizable) $\forall m\ge m_{\mathcal H}(\epsilon,\delta)$: $\Pr_S[\cdot]\ge1-\delta$; $m_{\mathcal H}$ independent of $D$ | Matches blueprint. **Learner randomness absent** (only Ex. 3.9 p. 53 "nondeterministic decisions") → course adds $\Pr_{S,\xi}$. Valiant's polynomial requirements only in §3.4 p. 50. |
| Confidence is over samples, not a posterior | pp. 38–39; p. 43 ("over the choice of the examples") | — | UML never contrasts with a posterior. Course addition. |
| Prop. 1.1 (unbiasedness) | **Ex. 2.2** p. 41 | binary $\mathcal H$, realizable, expectation over $S\vert_x$ | Blueprint more general (any integrable loss, $h$ fixed independently of $S$; identical marginals suffice, independence not needed — not in UML). Ex. 3.5 p. 51 shows the non-identical case $\bar D_m$. Duplicates original prompt 3. |
| Counterexample 1.2 (memorizer) | §2.2.1 pp. 35–36, Eq. (2.3); §2.3 remark p. 37; polynomial form Ex. 2.1 | 2-D: grey square area 2, label 1 on inner square area 1; memorizer → $L_D=1/2$ | Blueprint's 1-D version ($X\sim U[0,1]$, $Y\equiv1$, $L_D=1$) is cleaner. Both need $D_X$ giving mass 0 to finite sets. UML lacks the contrast with the good ERM (constant 1, $L_D=0$). $(S,x)\mapsto1[x\in\{x_1..x_m\}]$ jointly Borel. **One bad ERM selection, not all ERMs**; not NFL (Thm 5.1/Cor. 5.2 pp. 61–64). |
| Prop. 1.3 (Bayes rule) [O] | §3.2.1 p. 46 ("Bayes Optimal Predictor"); proof is Ex. 3.7 (*) p. 52; probabilistic predictors Ex. 3.8(1) | $f_D(x)=1$ iff $\Pr[y=1\vert x]\ge1/2$; optimal among all classifiers | Tie at 1/2 → 1. UML silent on measurability of $\eta$, non-uniqueness, Bayes risk $\mathbb E\min(\eta,1-\eta)$. **0–1 loss only: with asymmetric screening costs the threshold is $c_{FP}/(c_{FP}+c_{FN})$.** Manual's Ex. 3.7 last display has a typo. |
| Corollary (small $L_S$ is not a guarantee) | informal message of §2.2.1–2.3, pp. 35–37 | no formal statement | Suggested: in the setting of 1.2 the memorizer ERM has $L_S=0$, $L_D=1$ for every $S$, so no bound $L_D(\hat h)\le L_S(\hat h)+\varepsilon(m,\delta)$ with $\varepsilon\to0$ holds for every ERM selection over that class. |
| Examples §1.4 | squared loss Eq. (3.2) p. 48 (birth weight); temperature p. 45; noisy labels p. 45; multiclass documents p. 47 | — | Threshold rule and medical screening not in UML. If $\eta\in(0,1)$ on a positive-mass set, Bayes risk $>0$ and realizability fails for every $\mathcal H$. Squared loss is unbounded → Lecture 2 tools don't apply. |
| No-Free-Lunch (optional) | §5.1 pp. 61–64, Thm 5.1, Cor. 5.2 | $m<\vert\mathcal X\vert/2$ → prob ≥ 1/7 of $L_D\ge1/8$ | forward pointer only |

## 2. UML's motivation and order; what to borrow

UML order: papaya tasting → setting checklist (incl. what the learner does not see) → ERM → overfitting via memorizer → inductive bias (choose $\mathcal H$ before data; rectangles; restriction vs bias) → finite classes, realizability, i.i.d., $\delta$ as chance of a nonrepresentative sample, $\epsilon$, misleading samples, union bound, Cor. 2.3 → PAC + sample complexity → drop realizability via joint $D$ → Bayes predictor → agnostic PAC → multiclass/regression, general losses → measurability, proper/improper.

Borrow (structure only): the setting checklist incl. "what the learner does not see"; failure → remedy → guarantee; $\delta$ as chance of an unrepresentative sample before defining PAC; realizable first then agnostic motivated by noise; Bayes right before agnostic PAC (why the comparator is the best in $\mathcal H$); measurability and proper/improper as short remarks. Leave §2.3.1's union-bound proof to Lecture 2 (preview in the bridge only).

Blueprint examples fit better: medical screening opening (cost-weighted 0–1 loss separates predictor from loss); 1-D memorizer; threshold rule as the hand-computable running example (becomes the VC example in Lecture 3); spam; temperature for regression. Use joint $D$ from the start with deterministic $f$, $h^\star\in\mathcal H$ as the realizable special case.

## 3. UML exercises (§2.4 pp. 41–42, §3.5 pp. 50–53; all have manual solutions)

| Ex. | Summary | Relevance | Difficulty | Extra prerequisites | Note |
|---|---|---|---|---|---|
| 2.1 | memorizer is a thresholded polynomial → ERM over thresholded polynomials overfits | high | easy–medium | none | complements prompt 4 |
| 2.2 | $\mathbb E L_S(h)=L_{(D,f)}(h)$ | high | easy | none | duplicates prompt 3 / Prop. 1.1 |
| 2.3 | tightest rectangle ERM; $m\ge4\log(4/\delta)/\epsilon$; $\mathbb R^d$; runtime | medium | medium–hard | union bound, $1-x\le e^{-x}$ | strips of mass exactly $\epsilon/4$ fail with atoms; Lecture 2 |
| 3.1 | $m_{\mathcal H}$ non-increasing in $\epsilon,\delta$ | high | easy | none | |
| 3.2 | singletons: design ERM; PAC with $\lceil\log(1/\delta)/\epsilon\rceil$ | high (ERM design, ties) | medium | $(1-\epsilon)^m\le e^{-\epsilon m}$ | handle "positive point mass ≤ ε"; slight overlap with prompt 2 |
| 3.3 | concentric circles PAC with $\lceil\log(1/\delta)/\epsilon\rceil$ | medium (threshold on $\Vert x\Vert$) | medium | as 3.2 | manual's radius of mass exactly ε fails with atoms |
| 3.4 | Boolean conjunctions | low–medium | medium | finite-class Cor. 2.3 | Lecture 2 |
| 3.5 | non-identical independent samples, $\bar D_m$ | medium | medium | union bound, AM–GM | Lecture 2 |
| 3.6 | agnostic PAC ⇒ PAC, same learner | high (inf vs min) | easy | none | |
| 3.7 (*) | Bayes predictor optimal | Prop. 1.3 | easy–medium | conditional expectation | duplicates Prop. 1.3 proof |
| 3.8 (*) | (1) Bayes optimal among probabilistic predictors, loss $\vert h-y\vert$; (2) per-$D$ best algorithm; (3) every $A$ beaten by some $B$ on some $D$ | high | medium | none | manual incomplete in (1) and (3) (fix with point masses and "for all samples") |
| 3.9 (*,**) | two-oracle PAC model | low | hard | Chernoff | omit |

Recommended: 2.1, 3.1, 3.2, 3.3, 3.6, 3.8 (challenge). Omit 2.2, 3.7; defer 2.3, 3.4, 3.5; omit 3.9.

## 4. Running example (all numbers verified exactly by the source agent and by the master)

Setting: $\mathcal X=\{1,\dots,5\}$, $D_X$ uniform (0.2 each), $Y=1$ diseased, 0–1 loss, $\mathcal H=\{h_t=1[x\ge t]\}$, effectively $t\in\{1,\dots,6\}$.

(a) Agnostic: $\eta=(0,\tfrac14,\tfrac34,\tfrac25,1)$. $L_D(h_t)$ for $t=1..6$: 0.52, 0.32, **0.22**, 0.32, 0.28, 0.48. Bayes rule predicts 1 on $\{3,5\}$, Bayes risk 0.18; gap 0.04. Sample $S=((1,0),(2,0),(2,1),(3,1),(4,0),(5,1))$: $L_S(h_t)$ = 1/2, **1/3, 1/3**, 1/2, **1/3**, 1/2; ERM set $\{2,3,5\}$ with $L_D$ 0.32, 0.22, 0.28 (excess 0.10, 0, 0.06). $L_S(h_3)=1/3\ne0.22=L_D(h_3)=\mathbb E_SL_S(h_3)$. Over all 32 functions the smallest training error is 1/6 (x=2 has both labels).

(b) Realizable: $f=1[x\ge3]$. ERMs $A_{\max}$ ($\hat t$ = smallest positive in $S$, 6 if none; $L_D=0.2(\hat t-3)$) and $A_{\min}$ ($\hat t$ = largest negative + 1, 1 if none; $L_D=0.2(3-\hat t)$). $\Pr[L_D(A_{\max})>0]=0.8^m$ (≤0.05 iff $m\ge14$: $0.8^{13}=0.0550$, $0.8^{14}=0.0440$); same for $A_{\min}$ ($2\notin S$); $\Pr[L_D(A_{\max})>0.25]=0.6^m$ ($m\ge6$: $0.6^5=0.0778$, $0.6^6=0.0467$). $\mathbb E L_D(A_{\max})=0.2(0.8^m+0.6^m+0.4^m)\approx0.0227$ at $m=10$. These sample sizes are for this $D$; distribution-free needs the worst case → Lecture 2.

(c) Memorizer: $U[0,1]$, $Y\equiv1$; memorizer $L_S=0$, $L_D=1$ for every $S$; constant-1 ERM $L_D=0$.

## 5. Pages consulted

UML: 33–53 (§2.1–2.4, §3.1–3.5), 60–64 (Ch. 5 intro, §5.1, start of §5.2); keyword search pp. 1–130. Solution manual: pp. 1–8 (only to check difficulty and gaps).
