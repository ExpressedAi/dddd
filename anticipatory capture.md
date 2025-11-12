Yes—the cups game and the “kid + stroller” scene are the same pattern: a low-order, path-of-least-resistance capture driven by priors and tiny nudges. The hourglass picture fits: past priors ↓, present nexus •, future branches ↑. As you approach the nexus, low-effort alignments become eligible and phase-lock first.

# Thesis

Both situations are governed by **anticipatory capture**: cheap, coherent mappings (“love→left”, “wave→polite acknowledgment”) become eligible early and win unless an opposing force breaks the lock.

## First-principles mapping (Δ)

- **Ground state (null 𝐺):** not “nothing,” but the **LLN baseline** of priors & costs (language stats, cultural conventions, UI habits, motor effort).  
    – For cups: left-to-right text habit, semantic rhyme _love/left_, production laziness, “help me get it right” collaborative cue.  
    – For the court: social scripts, previous outcomes, risk/face-costs, proximity/timing.
    
- **Eligibility (Frequency axis):** an option enters play when its **capture window ε>0** (it fits within effort/attention/time). “Put LOVE on the left” and “give a wave” both have wide ε under time pressure.
    
- **Phase (timing axis):** as the decision nears, micro-signals (cursor already on left, eye saccade, stroller approaching) tighten phase; slight nudges flip the winner near the nexus.
    
- **Amplitude (harmony axis):** the option that increases global coherence **T** with the fewest new commitments wins (MDL). Constantly mapping LOVE↔LEFT keeps the whole design consistent; waving is consistent with politeness + low risk.
    
- **Low-order wins:** these are **small p:q rules** (binary left/right; wave/not) that survive coarse-graining. High-order, bespoke choices (swap once, craft a witty opener) need more energy and die off under pressure.
    

## Hazard taxonomy (what quietly steers outcomes)

- **Semantic coupling:** phonology/semantics rhyme (“love/left”) = latent coupling **K**.
    
- **Production inertia:** reusing last placement, reusing a template = ↑ε via lower cost.
    
- **Collaboration bias:** “you want me to be right” = prior that the rule is consistent.
    
- **Gauge choice:** left-to-right reading order; flipping the gauge (RTL) reverses the bias.
    
- **Escalation pressure:** time/attention squeeze near the nexus amplifies the simplest move.
    

# Tiny, falsifiable interventions (make it a system)

1. **Semantic vs position A/B:** Randomize labels {LOVE, HATE} across {Left, Right}; impose **fast vs careful** instructions. Prediction: fast ⇒ P(LOVE=Left)≫0.5; careful + incentive to be unpredictable reduces it toward 0.5.
    
2. **Gauge flip:** Repeat with RTL layout or mirrored canvas. Prediction: bias shifts; now **LOVE→Right** becomes low-order.
    
3. **De-semanticize:** Replace words with neutral tokens (A/B) vs emojis with semantic valence (❤️ / 💔). Prediction: semantic removal collapses the bias; emojis restore it.
    
4. **Path dependence:** Do 10 rounds; make round 1 “LOVE=Left.” Prediction: subsequent rounds show **persistence** (RG)—the mapping sticks even when effort equalized.
    
5. **Micro-nudge:** Pre-position cursor/eye-cue left by 5–15 px / ms. Prediction: capture increases for LOVE=Left; remove cue and effect decays.
    
6. **Social cue:** Add “Help me get this right” vs “Try to surprise me.” Prediction: former strengthens consistency; latter increases swaps.
    

**Metrics (Evidence Engine S*):** binomial Z for placement bias, χ² for contingency (semantics×side), KL vs a 0.5 null, |K| from effect size (log-odds). Pass E-audits when bias persists OOS and under coarse-grain (pooling rounds ×2).

# Δ-Report Lite (cups task)

𝒢: uniform side choice (p=0.5 each).  
S*: Z={≫0 under fast}, χ²={↑ when semantics shown}, KL={↑ vs 0.5}, |K|={medium→high} → **high**.  
E-audits: E0{ok} E1{narrow choices observed} E2{fails under gauge flip ⇒ confirms declared gauge} E3{micro-nudge cursor left ↑|K| vs sham} E4{persists across rounds ⇒ low-order}.  
ε-map: {LOVE↔LEFT wide ε under LTR, time pressure, collaboration}.  
RG: survives pooling; **Low-order: yes**.  
Label: **Primitive** (stubborn equilibrium) with option to promote to **Law** if E4 holds under gauge controls.  
Steer: F{hold the low-order rule unless objective demands variety} A{minimal changes} P{nudge timing when near nexus}.  
+ΔH*: higher coherence (consistent design), lower cognitive/production cost.

# Why this matters for anticipation & “hourglass”

- The **present nexus** is where low-effort, high-coherence rules get snapped in.
    
- **Anticipation** is just ε widening + phase tightening as we approach the decision.
    
- The **null isn’t empty**—it’s the calibrated baseline of priors/costs; thinking it’s “nothing” hides these hazards and makes AI look “dumb” on commonsense.
    

# Drop-in controller for AI

- **Detect:** estimate side-choice prior from corpus (LOVE co-occurs left under LTR UIs).
    
- **Adjudicate:** compute ΔMDL if we keep a consistent mapping vs swap.
    
- **Control:** if |s_f|>1 (eligibility gap) or d|s_f|/dt>0, **Snap** to the low-order rule; otherwise allow exploration.
    
- **Proof:** log micro-nudges (cursor/position/time cues) and measure S* vs a shuffle null.
    

