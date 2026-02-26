
---

## Repository name options

Pick one (all are defensible and descriptive):

* `defensive-publication-wearable-anxiety-dementia`
* `prior-art-wearable-emotion-anxiety-dementia`
* `open-defensive-disclosure-mentalhealth-sensing`
* `defpub-affect-anxiety-neurocog-wearables`

---

## Recommended repo structure

```
/
  README.md
  DISCLAIMER.md
  DISCLOSURE.md
  PRIOR_ART_MATRIX.md
  THREAT_MODEL.md
  DATA_GOVERNANCE.md
  VALIDATION_PROTOCOLS.md
  REFERENCES.md
  LICENSE
  CITATION.cff
  CONTRIBUTING.md
  CODE_OF_CONDUCT.md
  SECURITY.md
  /docs
    00_abstract.md
    01_system_architecture.md
    02_wearable_signals.md
    03_anxiety_models.md
    04_dementia_memorycare.md
    05_change_detection.md
    06_multimodal_fusion.md
    07_privacy_ondevice.md
    08_failure_modes_bias.md
    09_glossary.md
  /schemas
    event.schema.json
    feature_vector.schema.json
    risk_score.schema.json
  /examples
    feature_catalog_template.csv
    baseline_model_pseudocode.md
    change_point_pseudocode.md
    on_device_pipeline_pseudocode.md
  /release
    RELEASE_CHECKLIST.md
    VERSION.md
```

---

## File contents (copy/paste)

### `README.md`

```markdown
# Defensive Publication: Wearable Emotion/Affect, Anxiety, and Dementia-Related Neuropsychiatric Change

This repository is a **defensive publication (prior-art disclosure)** covering methods and system architectures for using
**wearables** (and optionally multimodal sensing) to infer **emotional arousal/state**, detect **anxiety (acute & chronic)**,
track **mood change**, and detect **neuropsychiatric change patterns** often observed in **dementia and memory care**
(e.g., agitation, sundowning-associated arousal, wandering risk proxies).

## Purpose
1. Establish public prior art to reduce patent litigation risk for researchers and implementers.
2. Provide a structured technical basis for research teams to select, implement, and evaluate approaches.
3. Encourage privacy-preserving and clinically responsible implementations.

## What is disclosed
- Wearable signals (HR/HRV, EDA, temp, respiration proxies, IMU, sleep proxies)
- Feature extraction approaches and catalogs
- Context disambiguation and confound controls
- Personalized baselines and longitudinal change detection (drift, change-points, anomalies)
- Anxiety episode detection and forecasting variants
- Dementia/memory-care specific variants (agitation, sleep fragmentation, evening arousal patterns)
- Multimodal fusion variants (optional): phone, ambient sensors, speech, environment

## What this is NOT
- Not medical advice
- Not a diagnostic device by itself
- Not a claim of clinical efficacy

## How to use
- Read `DISCLOSURE.md` first.
- Use `PRIOR_ART_MATRIX.md` to find specific claims/variants.
- Use `VALIDATION_PROTOCOLS.md` for study design suggestions.
- Use `DATA_GOVERNANCE.md` and `THREAT_MODEL.md` for privacy and safety.

## License
This repository is dedicated to the public domain under **CC0 1.0** (see `LICENSE`), intended to maximize freedom to operate.

## Citation
If you use this disclosure in academic work, please cite via `CITATION.cff`.

---
Version: see `/release/VERSION.md`
```

---

### `LICENSE` (CC0 1.0 Universal)

```text
CC0 1.0 Universal

Statement of Purpose
The laws of most jurisdictions throughout the world automatically confer exclusive Copyright and Related Rights
(upon the creator and subsequent owner(s)) in a copyrighted work of authorship and/or a database (each, a "Work").

Certain owners wish to permanently relinquish those rights to a Work for the purpose of contributing to a commons
of creative, cultural and scientific works (“Commons”) that the public can reliably and without fear of later claims
of infringement build upon, modify, incorporate in other works, reuse and redistribute as freely as possible in any
form whatsoever and for any purposes, including without limitation commercial purposes.

The person(s) who associated a Work with this deed has dedicated the Work to the public domain by waiving all of their
Copyright and Related Rights in the Work worldwide under copyright law, including all related and neighboring rights,
to the extent allowed by law.

You can copy, modify, distribute and perform the Work, even for commercial purposes, all without asking permission.

Full text: https://creativecommons.org/publicdomain/zero/1.0/legalcode
```

---

### `DISCLAIMER.md`

```markdown
# Disclaimer

This repository is provided for research and defensive publication purposes only.

- Nothing here constitutes medical advice, diagnosis, or treatment.
- Implementations derived from this repository may be regulated as medical devices depending on jurisdiction and use.
- Physiological signals are non-specific; interpretation requires context and careful validation.
- Users and deployers are responsible for informed consent, privacy compliance, and safety governance.

If you build systems based on these concepts, you should involve clinical expertise, IRB/ethics review where relevant,
and robust privacy engineering.
```

---

### `DISCLOSURE.md` (the core defensive publication)

```markdown
# Patent Defense Disclosure (Prior Art)
## Wearable-Based Emotional State, Anxiety, Mood Change, and Dementia-Related Neuropsychiatric Monitoring

**Defensive Publication Date:** 2026-02-25 (or update to your actual publish date)  
**License:** CC0 1.0 Universal  
**Status:** Public domain dedication; intended as prior art / defensive publication.

### 1. Overview
This disclosure describes systems and methods for:
- inferring emotional arousal and regulation state from wearable physiology,
- detecting anxiety (acute episodes, chronic anxiety trends),
- tracking mood change over time,
- detecting neuropsychiatric change patterns relevant to dementia and memory care (agitation, sundowning-associated arousal, wandering proxies).

### 2. Core Architecture (all variants)
A. Continuous sensing via wearable sensors  
B. Signal conditioning and artifact detection  
C. Feature extraction (time windows + circadian aggregation)  
D. Context disambiguation (exercise, illness, environment)  
E. State inference (momentary)  
F. Change detection / trend inference (longitudinal)  
G. Risk scoring and notification/escalation  
H. Governance: privacy, consent, retention, human-in-the-loop

### 3. Wearable Signals (non-exhaustive)
- Cardiovascular: HR, HRV (RMSSD, SDNN, LF/HF where appropriate), PPG morphology
- Electrodermal activity: tonic/phasic EDA, peak rate
- Respiration proxies: respiratory rate, variability (from PPG/IMU if not dedicated)
- Skin temperature: peripheral temp, circadian thermal drift
- Motion: IMU activity, restlessness indices, gait proxies
- Sleep proxies: latency, fragmentation, timing drift, stability

### 4. Feature Families (non-exhaustive)
- Autonomic load indices (sympathetic activation + vagal withdrawal)
- Recovery metrics: return-to-baseline half-life after arousal
- Instability metrics: variance/entropy of HRV, sleep timing, activity routines
- Behavioral coupling: physiology conditioned on activity class (rest vs walk vs sleep)
- Circadian measures: phase shift, amplitude dampening, intradaily variability

### 5. Emotional State Inference (momentary)
Disclose all variants:
- Rule-based thresholds with context gating
- Supervised ML classifiers for states (calm/activated/stressed/dysregulated)
- Regression models for arousal intensity
- Self-supervised representation learning for latent state embeddings
- Bayesian latent-state models (e.g., HMM) with wearable observations

### 6. Anxiety Detection
Disclose all variants:
- Acute episode detection (anomaly detection on resting HR/HRV/EDA + respiration)
- Chronic anxiety trend detection (baseline shift in HRV suppression, sleep fragmentation)
- Panic forecasting variants (pattern match to prior episodes; early sympathetic surge)
- Personalized adaptive thresholds and per-user calibration
- Multi-time-scale modeling: minute-level detection + weekly baseline drift

### 7. Dementia / Memory Care Variants
Disclose all variants:
- Agitation detection from restlessness + autonomic arousal at rest
- Sundowning-associated arousal patterns: evening risk windows with circadian drift
- Wandering risk proxies: motion + arousal coupling + sleep disruption
- Care context integration: caregiver interventions as labels/feedback
- Differentiation of anxiety vs pain/illness via multi-sensor confounds and trend context

### 8. Context Disambiguation (confound control)
Disclose all variants:
- Activity classification and exertion gating (exercise vs anxiety)
- Illness detection proxies (fever: temp + HR; respiratory infection: respiration changes)
- Medication timing modeling (sedatives, stimulants) as covariates
- Environment conditioning (heat/cold, noise, light) where available
- Event flags (care events, visitor presence, appointments) as priors

### 9. Change Detection / Longitudinal Monitoring
Disclose all variants:
- Control charts (CUSUM/EWMA) over latent state scores
- Bayesian change-point detection on baseline HRV/sleep/activity entropy
- Drift scoring and “behavioral entropy” measures
- Cohort-normalized + individualized baselines (prefer individualized for detection)
- Missingness-aware modeling (quality flags, sensor dropout handling)

### 10. Multimodal Fusion (optional extension)
Disclose all fusion variants:
- Wearable-only systems
- Wearable + phone mobility/routine
- Wearable + ambient sensors (PIR/doors/bed mats)
- Wearable + speech prosody (on-device features)
- Early fusion, late fusion, hierarchical fusion, mixture-of-experts

### 11. Alerting & Intervention Frameworks
Disclose all variants:
- User-facing notifications and coping prompts
- Caregiver dashboards for memory care
- Clinical escalation protocols (human review)
- Adaptive notification suppression to reduce alarm fatigue
- Confidence scoring and “why” explanations (feature attribution)

### 12. Privacy, Security, and Governance
Disclose all variants:
- On-device feature extraction (no raw audio/video required)
- Differential privacy and federated learning variants
- Consent management and least-privilege sensing
- Bystander privacy strategies (if multimodal)
- Data retention minimization and audit trails

### 13. Defensive Publication Statement
All combinations, permutations, and obvious extensions of the above methods are intentionally disclosed as public prior art,
including:
- any wearable sensor combination;
- any feature set derived from those sensors;
- any ML / statistical method used to map features to state or change;
- any dementia/memory-care adaptation of the same.

End of disclosure.
```

---

### `PRIOR_ART_MATRIX.md` (maps “claim-like” items to sections)

```markdown
# Prior Art Matrix (Claim-Like Index)

This matrix is designed to make the defensive publication easy to cite in patent defense contexts.

| ID | High-level method (claim-like) | Covered in |
|---|---|---|
| PA-001 | Inferring emotional arousal from wearable HR/HRV features | DISCLOSURE §3–§5 |
| PA-002 | Detecting anxiety episodes using HR spike + HRV suppression at rest | DISCLOSURE §6 |
| PA-003 | Detecting anxiety using EDA tonic/phasic features | DISCLOSURE §3, §6 |
| PA-004 | Predicting panic/anxiety escalation via anomaly detection on physiological precursors | DISCLOSURE §6 |
| PA-005 | Personal baseline calibration and adaptive thresholds for anxiety detection | DISCLOSURE §6, §9 |
| PA-006 | Longitudinal mood change detection using sleep fragmentation + activity reduction | DISCLOSURE §9 |
| PA-007 | Dementia agitation detection using restlessness + autonomic arousal | DISCLOSURE §7 |
| PA-008 | Sundowning-associated arousal window detection using circadian drift measures | DISCLOSURE §7, §9 |
| PA-009 | Context disambiguation: exercise/illness gating for anxiety inference | DISCLOSURE §8 |
| PA-010 | Multi-time-scale modeling: minute-level detection + weekly trend drift | DISCLOSURE §6, §9 |
| PA-011 | Fusion of wearable signals with ambient/phone/speech features (early/late/hierarchical) | DISCLOSURE §10 |
| PA-012 | On-device feature extraction and privacy-preserving learning (FL/DP) for mental health monitoring | DISCLOSURE §12 |

Add new IDs as you expand docs.
```

---

### `THREAT_MODEL.md`

```markdown
# Threat Model (Privacy/Security)

## Assets
- Raw sensor data (physiology, motion)
- Derived features (HRV, EDA peaks, sleep proxies)
- Risk scores and alerts
- User identity and consent records

## Adversaries
- Unauthorized household members
- Malicious app/service operators
- Data brokers
- External attackers (network compromise)
- Insider threats (facility staff misuse)

## Threats
- Re-identification from time-series behavior
- Stigmatizing inference (anxiety/dementia risk)
- Bystander capture (if microphones/cameras used)
- Model inversion / membership inference
- Alert misuse (coercion, surveillance)

## Mitigations (variants)
- On-device processing; store features not raw signals where possible
- Encryption in transit/at rest
- Differential privacy / federated learning options
- Consent + role-based access control
- Minimal retention + audit logging
- Explainability and confidence thresholds to avoid over-alerting
```

---

### `DATA_GOVERNANCE.md`

```markdown
# Data Governance

## Principles
- Consent-first, revocable
- Least-privilege sensing (start wearable-only)
- Minimal retention (store only what is needed)
- Transparency (what is collected; why; who can see it)

## Suggested retention
- Raw signals: 0–72 hours (or none) unless research requires
- Features: 30–180 days for longitudinal baselines
- Risk events: longer if needed for clinical review

## Human-in-the-loop
- For dementia/memory-care: caregiver confirmation for agitation labels
- For anxiety: optional user confirmations (lightweight)

## Compliance note
Regulatory requirements vary by jurisdiction and use. Consult experts when moving toward clinical deployment.
```

---

### `VALIDATION_PROTOCOLS.md`

```markdown
# Validation Protocols (Research-Oriented)

## Target outcomes
- Anxiety: acute episodes, chronic severity trend, relapse risk
- Dementia/memory care: agitation events, sundowning windows, wandering risk proxies

## Ground truth options
- EMA (1–2 questions/day)
- Clinical scales: GAD-7, PHQ-9; caregiver NPI/NPI-Q for dementia symptoms
- Event logs: PRN medication, caregiver incident reports
- Sleep diary + actigraphy comparisons (subset)

## Evaluation
- Within-person detection: change-point sensitivity/specificity
- Event detection: precision/recall, time-to-detect, false alarm rate per day
- Calibration: reliability plots for risk probabilities
- Subgroup fairness: age, sex, skin tone (PPG/EDA performance), comorbidities

## Study designs
- N-of-1 longitudinal baselines
- Stepped-wedge deployments in facilities
- Prospective cohort with regular clinical assessments
```

---

### `REFERENCES.md` (starter; expand as needed)

```markdown
# References (Starter)

Add peer-reviewed sources supporting:
- HRV/EDA associations with stress/anxiety
- Wearables for mental health monitoring
- Speech markers for depression/cognitive impairment (optional multimodal)
- Ambient sensing in aging/dementia (optional multimodal)
- Privacy/ethics in digital phenotyping

Tip: use DOI links and stable citations.
```

---

### `CITATION.cff`

```yaml
cff-version: 1.2.0
title: "Defensive Publication: Wearable Emotion/Affect, Anxiety, and Dementia-Related Neuropsychiatric Change"
message: "If you use this work, please cite it."
type: dataset
authors:
  - family-names: Stewart
    given-names: Guy
version: "1.0.0"
date-released: 2026-02-25
license: CC0-1.0
repository-code: "https://github.com/<ORG>/<REPO>"
```

---

### `CONTRIBUTING.md`

```markdown
# Contributing

Contributions are welcome if they improve clarity, expand variant coverage, or add references.

## Contribution types
- Additional variants/approaches for prior art coverage
- Threat model and governance improvements
- Validation protocol expansions
- Reference additions with DOIs

## Requirements
- No proprietary or confidential material
- Keep it general (defensive publication), not device-specific IP
- Prefer clear, testable wording
```

---

### `SECURITY.md`

```markdown
# Security Policy

This repository is documentation-only. If you believe the content introduces a security risk (e.g., suggests unsafe patterns),
open an issue labeled `security`.

Do not post private data.
```

---

### `CODE_OF_CONDUCT.md` (minimal)

```markdown
# Code of Conduct

Be respectful. No harassment. Assume good intent.
```

---

## Optional: schemas and examples (high value for engineering teams)

### `schemas/feature_vector.schema.json`

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "WearableFeatureVector",
  "type": "object",
  "properties": {
    "subject_id_hash": { "type": "string" },
    "timestamp_utc": { "type": "string", "format": "date-time" },
    "window_seconds": { "type": "integer", "minimum": 10 },
    "activity_state": { "type": "string", "enum": ["sleep", "rest", "walk", "run", "unknown"] },
    "hr_bpm_mean": { "type": "number" },
    "hrv_rmssd_ms": { "type": "number" },
    "eda_tonic_us": { "type": "number" },
    "eda_peak_count": { "type": "integer", "minimum": 0 },
    "skin_temp_c": { "type": "number" },
    "motion_rms": { "type": "number" },
    "sleep_fragmentation_index": { "type": "number" },
    "signal_quality_flags": { "type": "array", "items": { "type": "string" } }
  },
  "required": ["subject_id_hash", "timestamp_utc", "window_seconds"]
}
```

### `schemas/risk_score.schema.json`

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "RiskScore",
  "type": "object",
  "properties": {
    "subject_id_hash": { "type": "string" },
    "timestamp_utc": { "type": "string", "format": "date-time" },
    "risk_type": { "type": "string", "enum": ["acute_anxiety", "chronic_anxiety_trend", "agitation", "sundowning_window"] },
    "risk_score_0_1": { "type": "number", "minimum": 0, "maximum": 1 },
    "confidence_0_1": { "type": "number", "minimum": 0, "maximum": 1 },
    "explanation": { "type": "array", "items": { "type": "string" } }
  },
  "required": ["subject_id_hash", "timestamp_utc", "risk_type", "risk_score_0_1"]
}
```

### `examples/feature_catalog_template.csv`

```csv
feature_name,description,window,notes
hr_bpm_mean,Average heart rate,both,Context-gate for exertion
hrv_rmssd_ms,RMSSD HRV estimate,rest/sleep,Noise sensitive; needs SQI
eda_tonic_us,Tonic EDA level,rest,Useful for arousal
eda_peak_count,Count of EDA peaks,short,Stress reactivity proxy
sleep_fragmentation_index,Nighttime awakenings proxy,night,Correlates with dysregulation
motion_rms,Motion energy,short,Restlessness/agitation proxy
```

---

## Release hygiene (for “real” defensive publication)

**Suggested steps**

1. Create repo (public).
2. Add all files above.
3. Add a GitHub Release: `v1.0.0` and tag it.
4. Enable GitHub Pages for `/docs` (optional) to make it easy to cite.
5. Add a PDF snapshot in `/release/` if you want immutable archiving (optional).
6. Consider mirroring to an immutable archive (e.g., Zenodo) for DOI (optional).

---

## If you want, I can also generate

* A **single-page PDF** of the disclosure suitable for attorneys/examiners (with a formal prior-art style header).
* A **Zenodo-ready metadata file** (for DOI minting).
* A **“Claim chart” expansion** of `PRIOR_ART_MATRIX.md` with more granular IDs (e.g., 50–150 entries).

