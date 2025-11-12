

**Thesis.** Catastrophic Forgetting = failure of **RG-persistence**: high-order “ornaments” from a new task overwrite **low-order laws** captured by a prior task. The **Annealing Integrator** preserves laws via **RG-Extraction → Canon (hard constraints)**, then learns the new task under **Cognitive Annealing** to find a composite equilibrium that raises **H*** for Task B **without** violating Task-A laws.

---

## 1) Objects & Measures (operational)

- **Model state.** Parameters θ; representations carry **phase** θᵢ (angles) and **amplitudes** Aᵢ (importance).
    
- **Locks (low-order).** For features/channels a,b, test low-order ratios (p{:}q\in R_L={1{:}1,2{:}1,3{:}2,4{:}3,5{:}4,1{:}2,2{:}3}).  
    Coupling (K_{ab}^{p:q}) (pull), quality (Q=f/Γ), **capture** (\varepsilon_{ab}^{p:q}=[2\pi K-(\Gamma_a+\Gamma_b)]_+).
    
- **Eligibility (Frequency axis).** (|s_f|=\varepsilon_{ab}^{p:q},|pf_a-qf_b|). Eligible if (|s_f|\le 1).
    
- **Harmony & Brittleness.** H* (task score; clarity/accuracy/efficiency composite). ζ = brittleness under small phase/weight perturbations.
    
- **Canon.** Immutable memory of **laws**: minimal set of constraints (\mathcal{C}_{\text{law}}) (locks, symmetries, invariants) that passed RG & E3.
    
- **Ornaments.** High-order, detuned, task-specific parameters allowed to melt/retune.
    

---

## 2) Protocol (high level)

1. **RG-Extraction (Task A).** Detect and validate low-order locks/invariants. Project θ into **law subspace** and **ornament subspace**; **commit laws to Canon**.
    
2. **Cognitive Annealing (enter Task B).** “Heat” the system: raise optimizer temperature/step noise and **soften ornaments only**, while **freezing laws** (hard constraints).
    
3. **Constrained Learning (Task B in presence of A).** Optimize B’s H* under Canon constraints using **Harmony Optimizer** (F→P→A priority) until a **composite equilibrium** is reached.
    
4. **Consolidation & Re-audit.** Cool; re-run RG tests; update Canon only if new candidate laws **beat** existing ones by E3 and survive RG (×2 coarse-grain).
    

---

## 3) Exact Algorithms

### 3.1 RG-Extraction → Canon (Task A)

**Goal.** Identify a **minimal** set of persistent laws; separate θ into (\theta=\theta_{\text{law}}\oplus\theta_{\text{orn}}).

**Steps.**

- **(E1) Vibration scan.** Compute per-pair spectra to find narrowband peaks; estimate ((f,\Gamma,Q)).
    
- **(Lock test)** For (p{:}q\in R_L): compute (K_{ab}^{p:q},\ \varepsilon_{ab}^{p:q}). Keep candidates with (\varepsilon>0) and |order| low.
    
- **(E3 micro-nudge).** Apply tiny phase nudges (±5°) or tiny δω and verify **K, Q, H*** increase vs. null/shuffle.
    
- **(E4 RG-persistence).** Coarse-grain (×2 subsampling / pooling tasks) → retain only locks that persist; **demote** high-order.
    
- **(Canon commit).** Store (\mathcal{C}_{\text{law}}) as constraints:
    
    - **Hard equalities/inequalities.** (g_j(\theta)=0) or (|g_j(\theta)|\le \tau_j) (e.g., phase relations, symmetry, conservation).
        
    - **Projectors.** Linear/nonlinear projector Π_law (onto law subspace) with tolerance band.
        

**MDL guard.** Minimize total (\sum (p+q)) and number of constraints s.t. E3+E4 pass.

### 3.2 Cognitive Annealing (enter Task B)

**Anneal schedule.**

- Temperature (T(t)) for t∈[0,1]: (T(0)=T_\text{cold}), ramp to (T_\text{hot}), cool to (T_\text{cold}).
    
- Learning rate/optimizer noise scale with T; **weight decay↑** on ornaments; **decay=0** on laws.
    

**Constraint handling.**

- **Hard freeze:** (\theta_{\text{law}}) clamped by Π_law.
    
- **Barrier/Lagrange:** L(θ) includes (\sum_j \lambda_j,\phi(g_j(\theta))) with (\phi) a quadratic/hinge barrier; (\lambda_j\to\infty) (or large) during heat; relaxed slightly only for **audited** law extensions.
    

### 3.3 Constrained Harmony Optimization (Task B)

**Objective.**  
[  
\max_{\theta}\ \underbrace{H^*_B(\theta)}_{\text{Task B}} ;-; \alpha,\underbrace{|\Pi_{\text{law}}^\perp(\theta-\theta^A)|^2}_{\text{law drift penalty}} ;-; \beta,\underbrace{\mathrm{KL}[\mathcal{D}^A\parallel \mathcal{D}^{A|B}]}_{\text{functional retention}}  
]  
s.t. (g_j(\theta)=0) or (|g_j(\theta)|\le\tau_j).

- **F (eligibility).** Ensure new B-locks don’t violate capture: if (|s_f|>1) w.r.t. an A-law, **break** high-order B behavior or widen ε **only** outside A-law bands.
    
- **P (phase polish).** Within ε, adjust representation phases to reduce detune against A-laws; default (\phi_{tol}=10^\circ).
    
- **A (amplitude reweight).** MWU / projected-gradient on channel weights to raise H*, penalizing steps that raise ζ or drift into Π_law⊥.
    

**Cooling & settle.** Reduce T; stop when:  
(i) (\max |C_i|\le \tau_C), (ii) (\Delta H^*) plateaus, (iii) constraint residuals ≤ tolerances.

---

## 4) Pseudocode (operator view)

```python
def rg_extract_canon(model, dataA):
    stats = measure_vibration(model, dataA)                 # f, Γ, Q
    locks = []
    for (a,b) in feature_pairs(model):
        for (p,q) in R_L:
            K, eps = lock_strength(stats[a], stats[b], p,q)
            if eps > 0: locks.append((a,b,p,q,K,eps))
    laws = rg_filter(locks)                                  # E3 micro-nudge + E4 persistence
    C_law, Pi_law = commit_canon(laws)                       # constraints + projector
    return C_law, Pi_law

def annealing_integrator(model, dataA, dataB):
    C_law, Pi_law = rg_extract_canon(model, dataA)
    theta0 = model.theta.copy()
    # Heat
    for T in schedule(T_cold, T_hot, phase='heat'):
        step = constrained_opt_step(model, dataB, T, C_law, Pi_law,
                                    drift_penalty=alpha, retention_beta=beta)
    # Cool
    for T in schedule(T_hot, T_cold, phase='cool'):
        step = constrained_opt_step(model, dataB, T, C_law, Pi_law,
                                    drift_penalty=alpha, retention_beta=beta)
    thetaB = model.theta
    return thetaB, C_law, Pi_law
```

**Constrained step (inner).**

- Project: (\theta \leftarrow \Pi_{\text{law}}(\theta)) on entry & exit of each step.
    
- Lagrangian: (\mathcal{L} = -H^*_B + \sum_j \lambda_j \phi(g_j(\theta)) + \alpha|\Pi^\perp_{\text{law}}(\theta-\theta^A)|^2 + \beta \mathrm{KL}(\cdot)).
    
- Update: AdamW-like with temperature-scaled noise; reject step if ζ↑ or any (g_j) breaches.
    

---

## 5) Defaults & Tolerances

- **Low-order set** (R_L) as above.
    
- **Phase thresholds:** (\phi_{tol}=10^\circ,\ \phi_{snap}=25^\circ).
    
- **E3 micro-nudge:** ±5° (phase) / tiny δω; ≥240 trials, FDR p<0.01, Z≥3.
    
- **Anneal:** (T_\text{hot} = 2!\times) base LR/noise; linear heat/cool over 20–40% of steps.
    
- **Penalties:** (\alpha) for law drift = 1.0 (scale to unit variance); (\beta=0.1).
    
- **Stop (A-axis):** (\tau_C=0.02), (\tau_A=0.02\sum A), (\tau_T=10^{-3}).
    
- **Fail-safes:** If eligibility fails (|s_f|>1) vs a Canon law, **break** that B behavior (reduce its amplitude) or **route** it to ornaments.
    

---

## 6) E-Audits (E0–E4) — **Retention-centric E3**

**Nulls.**  
N₁: **Standard fine-tuning** on B (no Canon, no anneal).  
N₂: **Regularization-only** (penalties without RG-Extraction).  
N₃: **Frozen model** (no learning on B).

**E0 Calibration.** Phase/gauge invariance; p-value calibration on lock detectors; law projector idempotence.

**E1 Vibration.** Show narrowband locks for A-laws survive amplitude mute and time reversal flips directed measures.

**E2 Symmetry.** Swapping equivalent features or global phase shifts does not change Canon verdicts; constraints commute with declared symmetries.

**E3 Micro-Nudge — Retention test (primary).**  
Design: randomized 3-arm (A/B/C) across ≥240 A→B sequences. Metrics on held-out A and B:

- **Arms:**  
    A: **Annealing Integrator (proposed)**.  
    B: N₁ standard fine-tune.  
    C: N₂ reg-only.
    
- **Interventions:** On A-laws during B-learning, apply ±5° phase nudge or ±5% amplitude nudge for 3 windows (pre-registered sign).  
    **Expected signs:** Proposed shows **A-retention↓ much less** vs B; nulls show larger A-drop and no monotone response.
    
- **Pass criteria:**
    
    - **Retention gain:** (\Delta \mathrm{Perf}_A = \mathrm{Perf}_A^{\text{post}}-\mathrm{Perf}_A^{\text{pre}}). Require  
        (|\Delta \mathrm{Perf}_A|_\text{proposed} \ll |\Delta \mathrm{Perf}_A|_\text{fine-tune}) with FDR p<0.01.
        
    - **B-task quality:** (\mathrm{Perf}_B) not worse than fine-tune (±ε margin).
        
    - **Monotone micro-nudge:** small signed nudges increase K,Q,H* within tolerance.
        
    - **Token/compute churn:** not higher than fine-tune for matched (\mathrm{Perf}_B).
        

**E4 RG-Persistence.** Coarse-grain (×2) sequences and multi-domain pooling; Canon laws persist; high-order ornaments die first; retention edge remains.

---

## 7) Anti-Patterns (hard warnings)

- Don’t optimize amplitudes before **eligibility/phase** checks.
    
- Don’t **force phase** when (|s_f|>1): widen ε or demote that path.
    
- Don’t expand Canon without E3+E4; demote effects reproducible by surrogates.
    
- Don’t confuse **coupling K** (pull) with **capture ε** (window).
    
- Don’t rely on correlation to switch leaders; require E3 (+ hysteresis).
    

---

## 8) Δ-Report Lite (per A→B run)

Δ-Report Lite  
𝒢: {N₁,N₂,N₃ benchmarks}  
S*: Z={..}, χ²={..}, KL={..}, |K|={..} → {low/med/high}  
E-audits: E0{ok} E1{ok} E2{ok} E3{Retention edge vs fine-tune; B quality ≥; p<0.01 FDR; Z≥3} E4{persists}  
ε-map: {A-law margins; B locks eligible?}  
RG: {survives}; Low-order: {yes (Canon)}  
Label: **Law** (low-order filter + annealed integration) — Reason: null-beating + micro-nudges + RG  
Steer: F{check |s_f|} A{drift penalty α, masks} P{phase polish within ε}  
+ΔH*: {observed (B)}; Retention: {ΔPerf_A vs fine-tune}  
Refs: {run ids; Canon v#}

---

## 9) Operator Checklist (tight)

- **Before B:** run **RG-Extraction** on A; commit Canon.
    
- **Heat:** raise T; freeze Canon; soften ornaments.
    
- **Learn B:** F→P→A with constraint penalties; reject steps if ζ rises or constraints breach.
    
- **Cool & audit:** compare to fine-tune; run E3 retention nudges; update Canon **only** if new laws beat nulls and persist.
    

**Outcome.** A continual learner that **filters by low-order**, integrates specifics via annealing, and **provably** mitigates catastrophic forgetting by **retaining A** while **achieving B**—a Δ-consistent, MDL-lean upgrade over naive fine-tuning.