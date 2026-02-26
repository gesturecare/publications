
## Core concept: two-stage pipeline

1. **State inference (proximal signals)**: affect / arousal / stress load / agitation / apathy / engagement / social withdrawal
2. **Change detection (distal clinical meaning)**: departures from *that person’s* baseline over weeks–months (prodrome, relapse, progression)

This “baseline + deviation” framing is central because many signals are **person-specific** and drift with age, seasonality, meds, illness, etc. Large passive-sensing studies explicitly emphasize within-person vs between-person markers and temporal scale issues. ([Nature][1])

---

## Sensor modalities → features → what they can (and can’t) tell you

### A) Wearables (watch, ring, patch)

**Signals**

* PPG/ECG: HR, HRV (time/frequency/nonlinear)
* EDA (if available): sympathetic arousal
* Skin temp, respiration (some devices), SpO₂
* IMU: activity, tremor, gait proxy, sleep/wake

**What research supports**

* Stress/anxiety inference often uses HRV + EDA + motion context; systematic reviews summarize common pipelines and model types. ([Frontiers][2])
* Autonomic nervous system monitoring is promising but highly sensitive to motion, device quality, and proprietary algorithms. ([ScienceDirect][3])

**Known failure mode (important for your project)**

* “Stress score” from consumer wearables is frequently **non-specific** (exercise, excitement, pain, fever can look identical). A key research direction is **context disambiguation** (what was the person doing?) rather than better HR alone. ([ScienceDirect][3])

**High-value candidate topics**

* Personal baseline HRV/EDA *plus* context (location/activity) to reduce false alarms
* Longitudinal **change-point detection** for anxiety/depression relapse risk

---

### B) Smartphone (passive “digital phenotyping”)

**Signals**

* Mobility: GPS/accelerometer-derived radius of gyration, routine regularity
* Sociability: call/text metadata counts (not content), Bluetooth proximity
* Device interaction: screen on/off, typing dynamics
* Sleep proxy: inactivity + charging patterns
* App use patterns (privacy-sensitive)

**What research supports**

* Reviews of smartphone sensing show signals can track **stress/anxiety/mild depression patterns**, but reporting quality and bias are recurring issues. ([JMIR mHealth and uHealth][4])
* Large-scale work shows digital markers can have **different temporal utility** (some predict same-day affect; others track slow drift) and may be **person-specific**. ([Nature][1])
* Best practices for maintaining *high-quality passive data* (dropouts, OS restrictions, missingness) are now being formalized. ([Nature][5])

**High-value candidate topics**

* “Minimal-intrusion” phone package (mobility + routine + sleep proxy) for depression/anxiety monitoring
* Methods to handle missingness without over-imputation (quality-aware modeling)

---

### C) Ambient smart-home sensors (PIR motion, door contacts, bed mats, appliance use)

**Signals**

* Room-to-room transitions, time-in-room, night wandering
* Kitchen activity / meal prep proxies
* Bathroom visit patterns
* Sleep fragmentation proxies
* Routine regularity and “entropy” of daily behavior

**What research supports**

* Ambient sensors are widely used for older-adult monitoring because they’re low burden and can capture functional change. ([aging.jmir.org][6])
* Smart-home behavioral deviation indices are being explored for **early neurodegeneration signals** (sleep/activity routine deviations). ([Frontiers][7])

**High-value candidate topics**

* Detecting apathy vs depression vs cognitive decline using **activity diversity + routine deviation**
* Combining ambient “function” signals with mood proxies from phone/wearable

---

### D) Cameras (security cams) and computer vision

**Signals**

* Facial affect (valence proxies), expressivity, micro-expression stats (with caution)
* Head pose, gaze, engagement
* Body posture / psychomotor slowing
* Gait (stride variability, speed) if camera geometry allows

**What research supports**

* In older adults, multimodal approaches using facial expression (often combined with speech) can distinguish depression/anxiety/apathy in clinical populations. ([PubMed][8])
* Reviews and meta-analyses suggest AI-based facial analysis can help detect neurocognitive disorders, but real-world generalization is the hard part (lighting, occlusion, demographics). ([MDPI][9])
* Depression affects emotional processing and expression; there’s a substantial literature on emotion recognition differences. ([Nature][10])

**High-value candidate topics**

* “Passive video” psychomotor slowing index (movement energy, gait speed) as a depression/cognitive-change marker
* Bias/robustness auditing for older-adult facial affect models (glasses, masks, lighting, skin tone)

---

### E) Audio / voice (Alexa, smart speakers, phone calls—ideally on-device)

**Signals**

* Prosody: speech rate, pause length/variability, intensity, pitch dynamics
* Voice quality: jitter/shimmer, harmonics-to-noise ratio
* Linguistics: lexical diversity, syntactic complexity, semantic coherence
* Conversational interaction patterns (turn-taking, latency)

**What research supports**

* Depression: multiple reviews/meta-analyses support speech feature differences and clinically meaningful classification—though heterogeneity and overfitting remain concerns. ([PMC][11])
* Cognitive impairment: systematic reviews find speech has diagnostic utility for MCI vs unimpaired; recent work reports strong AUCs in research settings. ([PMC][12])

**High-value candidate topics**

* Voice + language “digital biomarker” for early cognitive change using scripted and natural speech
* On-device feature extraction + privacy-preserving learning (no raw audio leaving the home)

---

### F) Thermostats / environmental preferences (your specific ask)

This is underexplored compared with phone/wearable/speech, but it’s a good niche.

**Signals (hypotheses to test)**

* Preferred setpoint drift (e.g., gradually warmer/cooler)
* Variability of adjustments (restlessness/agitation proxy)
* Time-of-day pattern changes (sleep/circadian disruption)
* Coupling with occupancy sensors (is person home but not adjusting when they used to?)

**Why it’s plausible**

* Depression/anxiety/cognitive decline frequently correlate with **sleep/circadian disruption** and changes in routine; thermostats are a coarse but continuous proxy of comfort-seeking behavior and routine regularity.
* The novelty is in tying environmental control behavior to mental-state change *with strong confound control* (season, HVAC performance, cost concerns, caregiver overrides).

**High-value candidate topics**

* Thermostat-behavior anomaly detection as an early “routine drift” signal (paired with indoor motion/sleep proxies)
* Differentiating “comfort change” from “cognitive forgetfulness” via cross-sensor evidence

---

## Modeling approaches teams can choose from

### 1) Multimodal fusion (best for specificity)

* **Early fusion**: concatenate features (needs careful missingness handling)
* **Late fusion**: per-modality models + ensemble
* **Hybrid**: shared latent state model with modality-specific encoders

Passive-sensing reviews consistently report better performance with **multimodal data** and **personalized models**. ([PMC][13])

### 2) Personalized baselines + deviation scoring (best for longitudinal change)

* Seasonal decomposition (weekday/weekend)
* Bayesian change-point detection
* Control charts / CUSUM on latent affect score
* “Digital phenotype drift” metrics (entropy, regularity)

### 3) Context disambiguation (required to avoid false alarms)

* Activity recognition (sleep/exercise/social outing) before interpreting HRV/EDA or voice arousal
* Home/away segmentation (phone + Wi-Fi/Bluetooth)
* Illness confounds (fever elevates HR; respiratory illness changes voice)

### 4) Ground truth strategy (the hardest problem)

* EMA “micro-surveys” (low burden, 1–2 questions/day)
* Periodic validated scales (PHQ-9, GAD-7, MoCA-like cognitive tasks)
* Event-based labels (clinician diagnosis change, med change)

Large studies emphasize that associations can differ **within-person vs between-person**, so your labeling must match your intended use (detect *your* change vs compare people). ([Nature][1])

---

## Candidate research topics (teams can “claim” one)

1. **Voice + language for early MCI detection** using smart-speaker interactions (privacy-preserving pipeline) ([PMC][12])
2. **Depression relapse early-warning** via phone mobility + sleep regularity + wearable HRV, personalized change-point detection ([Nature][1])
3. **Agitation/paranoia risk** via ambient night wandering + door events + sleep fragmentation + voice prosody shifts (case-series design) ([PMC][14])
4. **Apathy vs depression discrimination** from activity diversity + social proximity + speech rate/pause features ([PubMed][8])
5. **Thermostat behavior as routine drift biomarker** paired with occupancy/motion sensors (novel feature engineering + confound control) ([aging.jmir.org][6])
6. **Camera-based psychomotor slowing** + gait variability as a cross-condition marker (depression vs neurocognitive decline) ([MDPI][9])
7. **Data-quality and missingness framework** for real-world passive sensing (OS constraints, device churn, imputation risks) ([Nature][5])

---

## Ethics, privacy, and “don’t create a surveillance product by accident”

This domain has well-documented concerns: consent, secondary use, bystander privacy (cameras/mics), bias, and accountability. A commonly cited ethical treatment of digital phenotyping highlights privacy, consent, bias, and governance challenges. ([PMC][15])

Practical safeguards teams can build into proposals:

* **On-device processing** (store only features, not raw audio/video)
* **Bystander filtering** (only when enrolled person is present; face/voice gating)
* **User control + transparency** (what’s collected, when, why)
* **Least-privilege sensing** (start with non-audio/non-video if possible)
* **Clinical escalation policy** (what happens when the system flags risk?)

---

## What I’d treat as “known hard problems” (good thesis material)

* **Specificity**: stress/arousal ≠ anxiety; low activity ≠ depression (could be pain, weather, caregiving burden)
* **Generalization**: models trained on young adults often fail in older adults
* **Ground truth**: labels are sparse/noisy; clinical states don’t change on a tidy schedule
* **Equity/bias**: voice, face, and behavior baselines differ across demographics and health conditions

---

[1]: https://www.nature.com/articles/s44184-023-00041-y?utm_source=chatgpt.com "Differential temporal utility of passively sensed smartphone ..."
[2]: https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2024.1478851/full?utm_source=chatgpt.com "Detection and monitoring of stress using wearables"
[3]: https://www.sciencedirect.com/science/article/pii/S1566070225001262?utm_source=chatgpt.com "Wearable ANS monitoring in real life: A critical review of ..."
[4]: https://mhealth.jmir.org/2024/1/e40689?utm_source=chatgpt.com "Digital Phenotyping for Stress, Anxiety, and Mild Depression"
[5]: https://www.nature.com/articles/s41598-026-41435-0?utm_source=chatgpt.com "LINC: a framework for maintaining high-quality passive ..."
[6]: https://aging.jmir.org/2024/1/e57320/?utm_source=chatgpt.com "In-Home Positioning for Remote Home Health Monitoring in ..."
[7]: https://www.frontiersin.org/journals/neuroscience/articles/10.3389/fnins.2025.1617758/full?utm_source=chatgpt.com "DNA: detecting early signs of neurodegenerative diseases ..."
[8]: https://pubmed.ncbi.nlm.nih.gov/37531702/?utm_source=chatgpt.com "Developing a machine learning model for detecting ..."
[9]: https://www.mdpi.com/1999-5903/17/12/541?utm_source=chatgpt.com "Artificial Intelligence-Enabled Facial Expression Analysis ..."
[10]: https://www.nature.com/articles/s41598-023-31277-5?utm_source=chatgpt.com "Facial emotion recognition in patients with depression ..."
[11]: https://pmc.ncbi.nlm.nih.gov/articles/PMC11559157/?utm_source=chatgpt.com "The voice of depression: speech features as biomarkers for ..."
[12]: https://pmc.ncbi.nlm.nih.gov/articles/PMC12560767/?utm_source=chatgpt.com "Diagnostic utility of speech-based biomarkers in mild cognitive ..."
[13]: https://pmc.ncbi.nlm.nih.gov/articles/PMC12411791/?utm_source=chatgpt.com "Use of Mobile Sensing Data for Longitudinal Monitoring and ..."
[14]: https://pmc.ncbi.nlm.nih.gov/articles/PMC12431156/?utm_source=chatgpt.com "Stage-Wise IoT Solutions for Alzheimer's Disease - PMC - NIH"
[15]: https://pmc.ncbi.nlm.nih.gov/articles/PMC8367187/?utm_source=chatgpt.com "Ethical Development of Digital Phenotyping Tools for Mental ..."
