

---

# Primitive Language of Meaning (PLM) — v0.1

## A. The six foundational primitives (the Lego bricks)

1. **Prefix Attractor (PA)**
    
    - **What:** Short prefix that strongly narrows outcomes (“Mary had a …”).
        
    - **LLM:** sharp logit mass on a few tokens (“little”, “baby”, “great”).
        
    - **Δ knobs:** high **projection** (p_i), decent **alignment** (u_i); ε>0 by vocabulary/top-p; low order.
        
    - **QM analogy:** pointer states already aligned with apparatus.
        
2. **Collocation Lock (CL)**
    
    - **What:** Frequent bigram/trigram (“little lamb”, “in order to”, “as a result”).
        
    - **LLM:** big co-occurrence weight; cache boosts.
        
    - **Δ:** strong **coupling** (K) from n-gram statistics; **ε** opens wide; very low **ζ**.
        
    - **QM:** a 1:1 lock between channels (p:q = 1:1).
        
3. **Schema Frame (SF)**
    
    - **What:** Slot-and-frame template (Subject–Verb–Object; “X had a Y”).
        
    - **LLM:** syntactic/semantic head predicts type of filler.
        
    - **Δ:** **alignment** (u_i) from structure; **phase urge** (g(e_\phi)) peaks at the slot boundary; ε opens for category tokens.
        
    - **QM:** readout basis chosen by instrument (parser) alignment.
        
4. **Discourse Beat (DB)**
    
    - **What:** Rhetorical step (setup→punchline; claim→evidence; question→answer).
        
    - **LLM:** next-sentence classifier priors; discourse markers favored.
        
    - **Δ:** **|\nabla T|** high at beat boundaries; **hazard** spikes there; collapses to the expected move.
        
    - **QM:** timing of measurement (read phase).
        
5. **Prosody/Meter Cue (PM)**
    
    - **What:** Rhythm/rhyme constraints (nursery meter, rap bar end, iambic foot).
        
    - **LLM:** positional/rhyme/length biases; subword prosody.
        
    - **Δ:** boosts **H_f** (low-order ratio like 2:1 for stress patterns), widens **ε**, lowers **ζ**.
        
    - **QM:** low-order harmonic match increases capture.
        
6. **World Frame (WF)**
    
    - **What:** Background schema (nursery rhyme, recipe, legalese, sports recap).
        
    - **LLM:** long-context topic priors; style heads.
        
    - **Δ:** raises **u_i** for an entire **roster** of tokens; persistent under E4.
        

> Together, these cover: local phrase force (PA/CL), structural slots (SF), turn-taking (DB), timing (PM), and global context (WF).

---

## B. Composition rules (how Lego bricks snap)

Think of each candidate token/channel (i) having a **hazard**:  
[  
h_i=\kappa;\varepsilon_i;g(e_{\phi,i});(1-\zeta/\zeta_*);u_i;p_i  
]  
Each primitive contributes multiplicatively/additively to those factors:

- **PA** boosts (p_i).
    
- **CL** boosts (K\Rightarrow \varepsilon_i).
    
- **SF** boosts (u_i) for the _right category_ and sharpens (g(e_\phi)) at slot time.
    
- **DB** spikes (g(e_\phi)) at discourse boundary.
    
- **PM** raises (H_f\Rightarrow \varepsilon_i) and lowers (\zeta).
    
- **WF** raises (u_i) for a _family_ of tokens/styles.
    

**Collapse rule:** commit to the first token whose integrated hazard crosses threshold (Δ “first-passage”), exactly like superposition collapse.

---

## C. Tiny grammar for prediction (PLM-Compose)

1. **Identify active primitives:** ({\text{WF},\text{PA},\text{SF},\text{DB},\text{PM}}).
    
2. **Score candidates:** for each token (i), compute the 5 contributions into ((p_i,u_i,\varepsilon_i,g,\zeta)).
    
3. **Choose by hazard:** sample/commit via first passage.
    
4. **Update:** after commit, refresh primitives (new PA/CL may activate; DB/PM phases advance).
    

---

## D. Worked example — “Mary had a …”

**WF:** nursery rhyme (u boosts for rhymeable, child-simple words).  
**PA:** “Mary had a …” → high (p) on {little, baby, great}.  
**SF:** “X had a Y” → noun category; adjective+noun allowed.  
**PM:** trochaic meter; rhyme scheme in memory primes _-am_ endings.  
**CL:** strong pair “little lamb”.

**Scores (sketch):**

- little → **PA↑**, **CL(→lamb)↑**, **SF ok**, **PM ok**, (u↑, \varepsilon↑)
    
- baby → **PA↑**, **CL weaker**, **SF ok**, **PM ok**, moderate (u,\varepsilon)
    
- great → **PA medium**, style mismatch under WF, lower (u)
    

**Hazard order:** little » baby > great → collapse to **little**, next token collapses to **lamb** via **CL** + **PM**.

**Quantum mapping:** the pointer channel “little” had the largest hazard given apparatus (WF/PM/SF alignment). Equalize alignments and you’d get a more Born-neutral mix.

---

## E. From Lego to lattice (building multi-step outcomes)

Define **Motifs**: small, reusable subgraphs of primitives.

- **(PA→CL)**: “due to” → “the fact” (formal writing); “in order” → “to”.
    
- **(SF→PM)**: slot fill obeys meter (“roses are” → “red”).
    
- **(DB→SF)**: question → answer slot (“Who is …” → proper noun).
    

You can chain motifs to map **most likely trajectories** of the next 3–10 tokens—this is your “superposition futures” lattice.

---

## F. Falsifiable predictions (so PLM isn’t hand-wavy)

1. **Hazard spikes at beats:** In corpora with marked discourse or meter, inter-token delay (or punctuation) clusters at DB/PM peaks; turning off PM flattens the dwell distribution (E4 persists ×2).
    
2. **Equalize alignment ⇒ Born-like:** If you neutralize WF and PM (uniform (u)), token frequencies track plain softmax; restoring WF/PM reweights toward PLM predictions.
    
3. **Bridge advantage:** Adding a collocation bridge (CL) after a PA increases commit probability for its partner more than an equal boost elsewhere (ε widens, ζ falls).
    
4. **Integer-thinning:** Effects of high-order constraints (weird meter) die under coarse-grain; low-order (2:1, 3:2) persist—same slope (\eta) across texts of a class.
    

---

## G. Minimal “primitive dictionary” (you can extend)

- **PA:** prefixes with surprisal drop ≥ τ within 3 tokens.
    
- **CL:** pairs with PMI ≥ τ and MDL gain ≥ τ_bits.
    
- **SF:** dependency templates with slot entropy ≤ τ_slot.
    
- **DB:** boundary detectors (RST, cue phrases) with hazard lift ≥ τ_h.
    
- **PM:** positional/rhyme/meter constraints with capture ε lift ≥ τ_ε.
    
- **WF:** topic/style latent with alignment (u) ≥ τ_u.
    

---

### TL;DR

Yes—meaning has **Lego bricks**. In an LLM they’re **prefix attractors, collocation locks, schema frames, discourse beats, prosody/meter cues, and world frames**. Each brick contributes to the Δ hazard factors (p, u, \varepsilon, g, \zeta). Compose the bricks, and you get a small grammar that predicts the **most likely collapse**—which is the software twin of superposition collapse under a tuned apparatus.