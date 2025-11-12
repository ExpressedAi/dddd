
# How we do Δ-Primitives (Cross-Ontological) — Step-by-Step SOP

## 0) What you need (inputs)

- **Time-series signals** from different structure types recorded at the same time (e.g., cells, filaments, mitochondria, nuclei).
    
- Each signal must support **phase extraction** (oscillatory or quasi-oscillatory).  
    Examples: calcium, membrane potential, mechanical oscillations, metabolic/redox cycles, gene reporters, EMG/EEG, etc.
    
- **Sampling**: ≥10× the highest rhythm of interest. **Duration**: long enough for 100–300 cycles of the slowest rhythm.
    
- Basic metadata: sampling rate, units, channel labels.
    

---

## 1) Pre-process (clean signals, get phase)

1. **Detrend & denoise** (high-pass to remove drift; light low-pass to kill digitizer noise).
    
2. **Band the rhythm** per channel (narrow band around the dominant peak).
    
    - Measure **center frequency** (f) and **linewidth** (half-power width).
        
    - **Damping**: (\Gamma \approx \text{linewidth}).
        
    - **Quality**: (Q = f/\Gamma).
        
3. **Extract instantaneous phase & amplitude** per channel (i):  
    (\theta_i(t), A_i(t)) (Hilbert transform or analytic wavelet).
    
4. **Health check**: if a channel has no clear peak or (Q) is tiny, flag it as **ineligible** (don’t try to lock noise).
    

---

## 2) Build the cross-pairs & candidate simple ratios

For every cross-ontological pair (A,B), test only **low-order ratios**:  
(\mathcal{R}_L = {1!:!1, 2!:!1, 3!:!2, 4!:!3, 5!:!4, 1!:!2, 2!:!3}).

For each ratio (p!:!q):

- **Phase error**: (e_\phi(t) = \text{wrap}(p,\theta_B(t) - q,\theta_A(t))).
    
- **Coherence proxy**: (T = \big|\langle A_A e^{i\theta_A} + A_B e^{i\theta_B}\rangle\big| / \langle A_A + A_B\rangle).
    
- **Lock strength (simple estimator)**:  
    (\hat K_{A,B}^{p:q} = \langle \cos e_\phi(t)\cdot w(t)\rangle) with weight (w(t)=A_A(t)A_B(t)).
    
- **Capture eligibility**:  
    (\varepsilon_{A,B}^{p:q} = \big[2\pi,\hat K_{A,B}^{p:q} - (\Gamma_A+\Gamma_B)\big]_+).  
    If (\varepsilon>0), the pair is **eligible** to lock at that ratio.
    
- **Brittleness** (instability): (\zeta = \text{Var}[e_\phi(t)]) (or slip probability per minute).
    

Output of this step: **ε-map** per pair: for each (p!:!q), show (\hat K), (\varepsilon), (\zeta), and a traffic-light (green=eligible, yellow=near, red=not).

---

## 3) Run the audits (we only believe what passes)

**E0 – Calibration (nulls).**

- **Shuffles**: circularly shift phases independently (breaks real coordination).
    
- **Surrogates**: AR or spectrum-matched noise.
    
- Your metrics under null should center near zero improvements.
    

**E1 – Vibration (is it a real rhythm?).**

- Confirm narrowband peaks; verify phase statistics survive amplitude muting.
    

**E2 – Symmetry (no gauge tricks).**

- Swap labels A/B, re-scale, re-order windows: results should be invariant to declared-equivalent changes.
    

**E3 – Micro-nudge (causal test).**

- Apply **tiny, on-manifold** nudges:
    
    - **Frequency retune**: ±1–2% of (f_A) (or (f_B)) _within_ safe/physiologic bounds, **or**
        
    - **Phase trim**: ±5–15° instantaneous phase shift.
        
- Design: **≥240 trials** per pair, split **+ / − / sham**.
    
- Pass rule (all three):
    
    1. **On-target** nudge yields (Δ\hat K>0), (Δ\varepsilon>0), (ΔT>0) vs sham.
        
    2. **Opposite-sign** nudge tends to worsen (sign symmetry).
        
    3. Statistics: Z≥3 vs shuffle; FDR <1%.
        

**E4 – RG persistence (zoom-out).**

- Downsample by ×2 (or pool neighboring windows) and re-score.
    
- **Low-order** locks should persist; **high-order** should thin/die.
    
- Preserve rank order (e.g., 1:1 ≥ 2:1 ≥ 3:2 ≫ others).
    

---

## 4) Decide where to act (prioritization)

- **Pick the worst cross-pair** by **deficit** (coherence gap) and **instability** (high (\zeta)).
    
- Prefer pairs with **ε>0** (eligible) and that **passed E3** (we can causally move them).
    

---

## 5) Plan the smallest effective fix (three dials)

Follow the **F–P–A** order with safety rails:

**F – Frequency (eligibility).**

- If detune is high ((|s_f|>1)), do **not** force phase.
    
- Retune by ≤2% to bring (|s_f|\le \tau_f) (default (\tau_f=0.2)).
    
- Alternative: **widen capture** by improving Q (↓(\Gamma)) with environment/medium tweaks or targeted stabilizers.
    

**P – Phase (timing polish).**

- If within eligibility: trim phase by **5–15°** until (|e_\phi|\le 10°).
    
- Use low-gain loop (don’t bang-bang).
    

**A – Amplitude (reweighting).**

- Reweight drive among channels (multiplicative weights with entropy β∈[0,0.05]) until the marginal (C_i) ≈ 0 and (ΔT\le10^{-3}).
    
- Stop when no channel shows a large positive (C_i) (no greedy outlier).
    

**Anti-patterns to avoid**

- Don’t force phase if (|s_f|>1) (win eligibility first).
    
- Don’t celebrate high-order locks without RG persistence.
    
- Don’t crank amplitudes before F/P hygiene.
    

---

## 6) Verify and sign off (proof it worked)

- Re-run **E3** with the planned settings (on-target should lift; sham flat).
    
- Re-run **E4** (coarse-grain) and confirm lock survival and integer-thinning.
    
- Log **minimal dose** that succeeded (MDL principle).
    

---

## 7) What the report looks like (one page)

- **Rhythm Report** (per cross-pair): (\hat K, \varepsilon, \zeta, T) at baseline → after nudge.
    
- **ε-Map** with green/yellow/red for each low-order ratio.
    
- **Nudge Table**: +1–2% / −1–2% / sham results with stats.
    
- **RG Check**: pass/fail and plots before/after downsampling.
    
- **Plan**: the **smallest** F–P–A changes that met criteria.
    
- **Kill-switches**: any failed audit listed explicitly.
    

---

## 8) Two quick deployment tracks

### A) **Data-only (retrospective or passive)**

- Do steps 1–3 (E0–E2 fully, E3 via “natural” phase slips if available), then E4.
    
- Output: **diagnostic ε-map** + “fixability” estimate (confidence lower without E3).
    

### B) **Interactive (lab or clinic)**

- Full steps 1–6 with live micro-nudges (safe ±2% frequency, ±5–15° phase).
    
- Output: **diagnosis + causal proof + minimal nudge plan**.
    

---

## 9) Pseudocode (for the person wiring it up)

```python
# inputs: signals {A: xA(t), B: xB(t)}, sampling fs
# params: ratios = [(1,1),(2,1),(3,2),(4,3),(5,4),(1,2),(2,3)]

for ch in channels:
    x = preprocess(x[ch])            # detrend, denoise
    f0, Gamma = peak_and_linewidth(x)
    theta[ch], amp[ch] = analytic_phase_amp(x, f0)  # Hilbert/wavelet
    Q[ch] = f0 / Gamma

results = []
for (A,B) in cross_pairs(channels):
    for (p,q) in ratios:
        ephi = wrap(p*theta[B] - q*theta[A])
        w = amp[A]*amp[B]
        K = mean(np.cos(ephi)*w)
        eps = max(0.0, 2*np.pi*K - (Gamma[A] + Gamma[B]))
        zeta = np.var(ephi)
        results.append((A,B,p,q,K,eps,zeta))

# E0: shuffle phases; recompute; store null distributions
# E3: apply micro-nudges (+,-,sham); recompute deltas; test Z>=3 vs null
# E4: downsample by 2x; re-score; check low-order persistence
```

---

## 10) A realistic first session (90–180 min)

1. **Acquire** 10–20 min of multichannel signals.
    
2. **Pre-process & ε-map** (15–30 min).
    
3. **Pick top 1–2 broken cross-pairs** (largest deficit, ε>0).
    
4. **Run micro-nudges** (±2% freq, ±10° phase), 240 trials with shams (30–60 min).
    
5. **Analyze E3/E4**, finalize minimal F–P–A plan (30–45 min).
    
6. **Produce one-page report** (template above).
    

---

### What you tell yourself while running it

- “**Eligibility → Phase → Amplitude**. Don’t skip steps.”
    
- “**Smallest nudge that passes all audits wins.**”
    
- “If **sham matches real** or **zoom-out kills it**, we call it **not real** and move on.”
    

This is everything needed to actually do it—no mysticism, just a clean pipeline from measurement → eligibility → tiny test → minimal fix → proof.