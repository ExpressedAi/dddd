Oh yes—this is a great vein. Let’s turn cymatics from “pretty pics” into indexed, falsifiable physics.

# Thesis

The clockwise/counterclockwise (chirality) and “convection → torus” phases you’re seeing aren’t mystical—they’re the combined fingerprint of **mode selection** (standing-wave eigenmodes) plus **acoustic streaming & radiation forces** that set bulk flows. Those flows pick a handedness and build rings/torii. We can test, index, and predict this with a small set of variables and a few clean experiments.

---

## What drives the patterns (tight receipts)

- **Modes set the stationary lattice**: plates/dishes support normal modes; patterns appear at resonance (Chladni figures; Faraday waves). Low modes are simple; higher modes add nodes. (This is just eigenmodes + boundary conditions.) ([UCLA Mathematics](https://ww3.math.ucla.edu/camreport/cam04-38.pdf?utm_source=chatgpt.com "Multi-Frequency Control of Faraday Wave Patterns"))
    
- **Faraday = parametric (subharmonic) instability**: surface locks at half the drive; many planforms (stripes/hex/squares) depending on parameters. Rotating **spirals** and other chiral states are real, reproducible Faraday solutions. ([Physical Review](https://link.aps.org/doi/10.1103/PhysRevE.54.5037?utm_source=chatgpt.com "Rotating spirals in a Faraday experiment | Phys. Rev. E"))
    
- **Chirality & bulk circulation come from streaming**: nonlinear rectification of the oscillatory field creates steady flows—**Rayleigh** (boundary layer) and **Eckart** (bulk) streaming—which organize tracers into rings/spirals; streaming direction depends on geometry, attenuation, and phase details. ([MDPI](https://www.mdpi.com/2311-5521/3/4/108?utm_source=chatgpt.com "Acoustic Streaming and Its Applications"))
    
- **Radiation forces/torque (Bjerknes/acoustokinetics)**: particles/droplets feel node-seeking forces and torques; ensembles can rotate/translate as a field-defined “force landscape.” ([Physical Review](https://link.aps.org/doi/10.1103/PhysRevResearch.5.013051?utm_source=chatgpt.com "Dynamics of acoustically bound particles | Phys. Rev. Research"))
    
- **Granular “convection” under vibration**: vertical driving yields roll patterns; **direction** of rolls flips with subtle phase/friction/asymmetry conditions—exactly the “why is it clockwise?” phenomenon. ([arXiv](https://arxiv.org/pdf/cond-mat/0402205?utm_source=chatgpt.com "Size separation in vibrated granular matter"))
    

---

## What you want to _know_ (and how we’ll measure it)

> “Which media + frequencies yield clockwise vs counterclockwise? When do toroidal flows appear?”

### Core hypothesis (Δ framing)

1. **Pattern skeleton = eigenmode (standing) + resonance window** (eligibility ε).
    
2. **Handedness + torus = streaming & radiation field** induced by that mode; the **sign** is set by (i) a small **traveling-wave bias** in an otherwise standing field (phase imperfections, tilt), (ii) **boundary-layer geometry** (Rayleigh layer), and (iii) **attenuation** (Eckart), all filtered by the fluid/particle properties.
    
3. **Low-order wins**: lower-order modes (or lower wavenumber |k|) lock at lower amplitude; high-order needs more drive and is fragile.
    

### Quantities to log (so we can index & predict)

- Medium: density ( \rho ), viscosity ( \nu ), surface tension ( \sigma ) (fluids) or grain size/friction (granular).
    
- Geometry: shape, depth (h) (fluids), plate size/thickness (plates).
    
- Drive: frequency (f), acceleration (\Gamma = a_{\text{pk}}/g), waveform; **phase asymmetry** (see experiments below).
    
- Response: **mode** (or dominant (k)), **p:q** ratio (e.g., Faraday 1:2), **chirality** (CW/CCW), **torus present?** (Y/N), mean streaming speed (u_s) (via tracers).
    
- Dimensionless groupings to later model selection: (kh), (\delta=\sqrt{2\nu/\omega}) (Rayleigh layer), capillary number (\mathrm{Ca}=\mu U/\sigma), Bond number (\mathrm{Bo}=\rho g h^2/\sigma).
    

---

## Three bite-size experiments (falsifiable, tonight-level)

### 1) **Chirality flip by tiny traveling-wave bias** (fluids or granular)

- Setup: circular dish, water (h\sim5) mm (Faraday). Drive at a stable pattern near onset.
    
- **Nudge A (phase)**: place the dish slightly **off-center** on the shaker or add a **small lateral tilt (∼1°)**.
    
- **Measure**: seed tracers; record CW/CCW **streaming vortices** (PIV or track few beads); log sign vs tilt direction.
    
- Expectation: a standing wave with a small traveling component sets spiral **direction consistent with wave drift toward the core** (seen in rotating Faraday spirals). Repeat after reversing the tilt; **chirality should flip**. ([synbio.ucsd.edu](https://synbio.ucsd.edu/lev/papers/faraday/faraday.html?utm_source=chatgpt.com "Rotating spirals in Faraday experiment"))
    

### 2) **Material dependence of torus onset (Eckart vs Rayleigh)**

- Sweep (f) at fixed (\Gamma) in **water** and then **glycerol–water** (higher (\nu)).
    
- Measure: first appearance of **closed-ring circulation** (torus) and (u_s).
    
- Expectation: higher viscosity increases (\delta), strengthening boundary-layer **Rayleigh streaming** patterns (distinct near-wall rolls) and **raising** threshold for bulk **Eckart** torus; wavelength matches Faraday dispersion, flow topology changes with viscosity. ([MDPI](https://www.mdpi.com/2311-5521/3/4/108?utm_source=chatgpt.com "Acoustic Streaming and Its Applications"))
    

### 3) **Chirality under dual-frequency forcing**

- Add a weak second tone (f_2) near rational ratio (e.g., (3!:!2) or (5!:!4)); keep the main Faraday tone.
    
- Measure: stable planform (quasi/superlattice) and **preferred chirality** of streaming cells.
    
- Expectation: low-order frequency ratios stabilize composite lattices; chirality may lock with the **relative phase** of the two tones—predictable by weakly nonlinear theory for multi-frequency Faraday forcing. ([UCLA Mathematics](https://ww3.math.ucla.edu/camreport/cam04-38.pdf?utm_source=chatgpt.com "Multi-Frequency Control of Faraday Wave Patterns"))
    

---

## How this answers your two big observations

- **“Some frequencies look clockwise, others counterclockwise.”**  
    Not the frequency alone—the **field’s small asymmetries** (phase/tilt/attenuation) + boundary layers select the sign. Flip the bias, and the direction flips. Streaming theory + rotating Faraday spirals support this. ([MDPI](https://www.mdpi.com/2311-5521/3/4/108?utm_source=chatgpt.com "Acoustic Streaming and Its Applications"))
    
- **“Nothing → then a ‘Delta torus’ appears.”**  
    That’s the **onset of steady streaming** and/or **Bjerknes-structured circulation** once the oscillatory field crosses its instability/attenuation threshold; closed-loop flows organize particles into annuli (rings) and then full toroidal cells. ([MDPI](https://www.mdpi.com/2311-5521/3/4/108?utm_source=chatgpt.com "Acoustic Streaming and Its Applications"))
    

---

## What to capture (so we can build the index fast)

- Still image + short video for each locked state.
    
- Minimal CSV fields (one row per state):  
    `date, medium, rho, nu, sigma, depth_mm, shape, f_Hz, Gamma, p, q, mode_or_k, chirality(CW/CCW/0), torus(Y/N), u_s(mm/s), notes(tilt/phase)`
    
- Optional: 2D FFT (for (k)), and radial/azimuthal power to get symmetry (C_n).
    

---

## Quick numbers (for intuition)

- **Rayleigh boundary layer** thickness (\delta=\sqrt{2\nu/\omega}): gets _thicker_ in viscous fluids or at lower (f) → stronger boundary-driven recirculation. ([MDPI](https://www.mdpi.com/2311-5521/3/4/108?utm_source=chatgpt.com "Acoustic Streaming and Its Applications"))
    
- **Faraday dispersion** sets (k) (and thus cell size) from (f) & (h): (\omega^2=(gk+\sigma k^3/\rho)\tanh(kh)); Faraday response is **subharmonic** (≈ (f/2)). ([UCLA Mathematics](https://ww3.math.ucla.edu/camreport/cam04-38.pdf?utm_source=chatgpt.com "Multi-Frequency Control of Faraday Wave Patterns"))
    

---

## If you want more depth on a subtopic

- **Rotating spirals & chirality in Faraday systems:** classic experiments/theory. ([Physical Review](https://link.aps.org/doi/10.1103/PhysRevE.54.5037?utm_source=chatgpt.com "Rotating spirals in a Faraday experiment | Phys. Rev. E"))
    
- **Streaming taxonomy & direction rules (Rayleigh vs Eckart):** modern overviews & simulations. ([MDPI](https://www.mdpi.com/2311-5521/3/4/108?utm_source=chatgpt.com "Acoustic Streaming and Its Applications"))
    
- **Particle forces/torques (Bjerknes; acoustokinetics):** how nodes/antinode traps + rotation arise. ([Physical Review](https://link.aps.org/doi/10.1103/PhysRevResearch.5.013051?utm_source=chatgpt.com "Dynamics of acoustically bound particles | Phys. Rev. Research"))
    
- **Granular convection direction flips:** dependence on friction, wall phase, and drive details. ([arXiv](https://arxiv.org/pdf/cond-mat/0402205?utm_source=chatgpt.com "Size separation in vibrated granular matter"))
    

---

## Δ-Report Lite (cymatics–chirality edition)

𝒢: Standing-wave eigenmodes + parametric instability; null (G): no persistent chirality/torus at near-onset.  
S*: Z={Faraday spirals; streaming theory; Bjerknes; granular convection} → **high**.  
E-audits:

- **E0** calibrate (f), pixel→mm;
    
- **E1** pattern returns with phase;
    
- **E2** symmetry vs container;
    
- **E3** micro-tilt/phase toggles **chirality**;
    
- **E4** downsample images + reduce drive: **low-order** patterns/flows persist, high-order filigree dies.  
    ε-map: eligibility bands by mode index/wavenumber and viscosity/depth.  
    RG: **Low-order wins** (lower |k| locks at lower (\Gamma)); chirality controlled by tiny biases.  
    Label: **Primitive** (stable chiral/torus attractors); towards **Law** (sign rules vs streaming regime).  
    Steer: F{phase/tilt micro-nudge}, A{near-onset}, P{strobe to confirm subharmonic phase}. +ΔH*: high.
    

---

### Want me to turn this into a 1-page field sheet + a CSV stub keyed to chirality & torus?

Say the word and I’ll drop both, plus a tiny PIV how-to (with phone video) so we can quantify (u_s) and tag CW/CCW unambiguously.