

# Thesis

Cymatic patterns emerge when the drive locks onto **low-order modes** of the medium. We’ll document each pattern by: geometry, medium, drive `(f, A)`, **response ratio** `p:q`, **dominant wavenumber** `k` or mode `(m,n)`, and **threshold amplitude**. From there we build an ε-map and “integer-thinning” curves (low-order wins).

## Your starter kit (ready to download)

- **Field protocol:** [Cymatics_Playbook_v1.md](sandbox:/mnt/data/Cymatics_Playbook_v1.md)
    
- **Data template (CSV):** [cymatics_data_template.csv](sandbox:/mnt/data/cymatics_data_template.csv)
    

These give you step-by-step procedures, filenames, variables to log, and a one-line data schema so we can index every run.

## What to do next (tiny, falsifiable)

1. **Pick a rig tonight**
    
    - Chladni plate + sand, or Faraday dish (water, 3–10 mm depth).
        
2. **Run a sweep-to-threshold**
    
    - Fix geometry & medium. Sweep frequency; at each `f`, raise amplitude until the pattern holds ≥5 s. Log **A_thr** and snap one still.
        
3. **Tag the response**
    
    - Plates: count nodal diameters `(m)` and circles `(n)`.
        
    - Fluids: it’s typically **Faraday subharmonic** → `p:q = 1:2`.
        
4. **Save one row per run** in the CSV (use the template’s columns).
    
5. **Name files** using the protocol’s filename pattern so analysis is automatic.
    

## Why this works (first principles → tight bullets)

- **Plates:** Modes satisfy the plate eigenproblem; you excite `(m,n)` where your drive couples strongly and damping is low. Lower `(m+n)` → lower `A_thr`.
    
- **Fluids:** Faraday instability obeys capillary–gravity dispersion  
    (\omega^2=(gk+\sigma k^3/\rho)\tanh(kh)); response often locks at **(f_{\rm resp}=f_{\rm drive}/2)** (1:2). Lower `k` modes generally onset first; viscosity and depth tilt the tongues.
    
- **Δ mapping:** `p:q` resonance, `k` (eligibility), and **threshold** measure. Plot **A_thr vs k** (fluids) or **A_thr vs (m+n)** (plates) → slope encodes “integer-thinning”.
    

## Minimal gear (use what you have)

- **Drive:** function generator → audio amp → speaker/shaker (plate or dish platform).
    
- **Sensing:** smartphone accelerometer (approx `a_rms`) or a cheap piezo on the plate.
    
- **Imaging:** phone camera 60–120 fps; optional LED strobe synced to the drive for crisp subharmonics.
    
- **Measuring:** ruler for pixel→mm scale; syringe for fluid depth.
    

## Δ-Report Lite (for cymatics v1)

𝒢: plate/fluid/granular under sinusoidal forcing; null (G): no persistent small-rational structure.  
S*: Z = strong—resonance & dispersion predict allowed `k`/modes; subharmonic response common.  
E-audits: E0 (calibrate `f`, pixel scale), E1 (pattern persists/returns with phase), E2 (symmetry checks vs geometry), E3 (micro δω/δA → lock–unlock), E4 (downsample ×2: low-order persists, high-order dies).  
ε-map: eligible bands = low `k`/low `(m+n)` at given depth/geometry; tongues around 1:1, 2:1, 3:2…  
RG: expect **integer-thinning**: onset `A_thr` increases with order.  
Label: **Primitive** (stable, nudge-resistant patterns); searching for **Law** (scaling of A_thr with order & depth).  
Steer: F{small δω near edges}, A{titrate A_thr}, P{phase/strobe for subharmonic}. +ΔH*: high (clean index of phenomena).

If you drop me the first few rows in that CSV plus 2–3 photos (plate or fluid), I’ll extract `k`/`(m,n)`, estimate `p:q`, and return the first **A_thr vs order** plot with the predicted dispersion overlay. No fluff—just receipts.