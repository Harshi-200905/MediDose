# MediDose — Personalized Medication Dosing Calculator

A polished, clinical-grade web application for weight-based medication dosing guidance.
Built as a healthcare portfolio project demonstrating real-world clinical calculator design.

---

## Overview

MediDose estimates safe dose ranges for common over-the-counter medications based on
patient age and weight. It follows established pediatric dosing principles (AAP guidelines,
Harriet Lane Handbook) and surfaces step-by-step calculation explanations alongside
safety alerts and age restriction warnings.

**This tool is for educational purposes only and is not validated for clinical use.**

---

## Features

- **Weight-based dosing** — mg/kg calculation with per-drug min/max caps
- **Age restriction checks** — real-time alerts when medication is contraindicated by age
- **Overdose safety warnings** — fires when projected daily dose approaches the safe limit
- **lb ↔ kg toggle** — automatic unit conversion built into the calculation engine
- **mL volume calculator** — computes liquid dose volume from formulation concentration
- **Custom concentration override** — for non-standard products
- **Plain-language explanation** — 8-step breakdown of every calculation
- **Confidence badges** — Standard / Check Formulation / Needs Professional Review
- **Caregiver + Student modes** — student mode auto-expands the explanation accordion
- **Example patient cases** — one-click demo scenarios for common presentations
- **Recent calculations** — saved to local storage, reload with one click
- **Copy result** — clipboard-formatted result summary
- **Print / Save** — print-optimized CSS for result card output
- **Dark mode** — full dark theme with system preference detection

---

## Supported Medications

| Medication | Category | Min Age | Dose (mg/kg) | Interval |
|---|---|---|---|---|
| Acetaminophen | Analgesic / Antipyretic | Birth (caution < 3 mo) | 10–15 mg/kg | Every 4–6 h |
| Ibuprofen | NSAID | 6 months | 5–10 mg/kg | Every 6–8 h |
| Diphenhydramine | Antihistamine | 2 years | 1–1.25 mg/kg | Every 6–8 h |

---

## Tech Stack

| Technology | Purpose |
|---|---|
| React 18 | UI framework |
| TypeScript | Type safety across all layers |
| Tailwind CSS v3 | Utility-first responsive styling |
| Vite | Build tool and dev server |
| Lucide React | Icon system |
| clsx | Conditional class composition |

---

## Project Structure

```
src/
├── types/          # Shared TypeScript interfaces
│   └── index.ts
├── data/
│   └── medications.ts   # Medication rules — dose, formulations, safety notes
├── utils/
│   ├── calculations.ts  # Core dosing calculation engine
│   └── validators.ts    # Form validation logic
├── components/
│   ├── ui/              # Button, Card, Badge, FormField
│   ├── layout/          # Header, Footer
│   ├── landing/         # Hero, Features, SupportedMeds, WhyAccuracy, Disclaimer
│   └── calculator/      # PatientForm, ResultPanel, ExampleCases
├── pages/
│   ├── LandingPage.tsx
│   └── CalculatorPage.tsx
├── App.tsx
├── main.tsx
└── index.css
```

---

## Getting Started

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build
```

---

## Calculation Logic

All dosing follows this pipeline:

1. Normalize age → months; normalize weight → kg (with lb conversion if needed)
2. Validate weight plausibility and age against per-drug restrictions
3. Compute weight-based dose range: `weight_kg × [mgPerKgMin, mgPerKgMax]`
4. Apply absolute single-dose cap: `min(calculated, maxSingleDoseMg)`
5. Compute effective max daily dose: `min(maxDailyDoseMg, weight_kg × maxDailyDoseMgPerKg)`
6. If liquid formulation: `volume_mL = dose_mg ÷ concentration_mg_per_mL`
7. Check if `maxDosesPerDay × maxSingleDose > maxDailyDose` and warn if true
8. Assign confidence badge: Standard / Check Formulation / Needs Professional Review

---

## Safety Disclaimer

> **MediDose is for educational and informational purposes only.**
> It does not constitute medical advice, diagnosis, or treatment guidance.
> All results must be verified with a licensed physician, nurse practitioner, or pharmacist
> before any medication is administered.
>
> **In emergencies:** Call 911. For suspected overdose: Poison Control 1-800-222-1222 (US).

---

## Clinical References (educational basis)

- American Academy of Pediatrics (AAP) OTC Medication Guidelines
- Harriet Lane Handbook, 22nd Edition
- FDA OTC Labeling — Acetaminophen, Ibuprofen, Diphenhydramine
- Nelson's Pediatric Antimicrobial Therapy

---

*Built as a healthcare/clinical software portfolio project. Not for clinical use.*
