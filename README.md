# COVID-19 Home Diagnosis AI System
### Using the DEMI Causal Algorithm + Large Language Model (Claude)

**Course:** Comparative Effectiveness  
**Instructor:** Abdul Hafeez 
**Author:** Katarzyna Rzucidlo
**Spring 2026**

---

## What This Project Does

This project builds an AI-powered COVID-19 home diagnostic tool that:

1. Loads real patient data from the COVIDCARE Phase II Survey (MIT, 2021)
2. Applies the **DEMI causal algorithm** to compute pairwise associations across 5 temporal tiers
3. Trains **Logistic Regression, LASSO, and XGBoost** models to predict PCR-confirmed COVID-19
4. Builds a **causal network diagram** showing relationships between symptoms and outcomes
5. Uses **Claude (Anthropic LLM)** to interpret the probability score in plain English for the patient

---

## Files in This Repository

| File | Description |
|------|-------------|
| `Covidanalysis.ipynb` | Main notebook — full DEMI + LLM pipeline |
| `merged.csv` | COVIDCARE DEMI Knowledgebase (70,983 variable pairs) |
| `COVIDCARE_FORSUBMISSION_MIT_CLEANED_Phase_II_2021-12-03.csv` | Raw patient data (822 patients, 472 variables) |
| `COVIDCARE_survey_dictionary_v2_ForSubmission_MIT_Phase_II_2021-12-26.csv` | Variable dictionary |
| `requirements.txt` | Python dependencies |

---

## How to Run

### Option 1 — GitHub Codespaces (Recommended)

1. Click the green **Code** button on this repo
2. Select **Codespaces** → **Create codespace on main**
3. Once it loads, open `Covidanalysis.ipynb`
4. Click **Run All** (or run cells top to bottom)
5. When you reach **Part R**, paste your Anthropic API key
6. View the LLM interpretation output in **Part S**

### Option 2 — Local

```bash
git clone https://github.com/Gchandanareddy/analysis.git
cd analysis
pip install -r requirements.txt
jupyter notebook Covidanalysis.ipynb
```

---

## API Key Setup

This project uses the **Claude API (Anthropic)** for LLM interpretation.

1. Get a free API key at [console.anthropic.com](https://console.anthropic.com)
2. In the notebook, find **Part R** and replace:
```python
ANTHROPIC_API_KEY = "YOUR_ANTHROPIC_API_KEY_HERE"
```
with your actual key.

---

## Model Results

| Model | AUC | Accuracy | McFadden R² | % Variation Explained |
|-------|-----|----------|-------------|----------------------|
| XGBoost | 0.948 | 93.6% | 0.565 | 56.5% |
| Logistic | 0.876 | 95.7% | -0.169 | -16.9% |
| LASSO | 0.867 | 95.0% | -0.246 | -24.6% |

**Baseline COVID-19 probability (no symptoms):** 38.08%

**Top direct predictor:** Neurological symptom cluster (LASSO coefficient: 1.066)

---

## DEMI Algorithm — 5 Tier Structure

| Tier | Variables | Count |
|------|-----------|-------|
| Tier 0 | Demographics (age, sex, race, ethnicity) | 27 |
| Tier 1 | Vaccination status | 50 |
| Tier 2 | Self-reported symptoms & exposures | 377 |
| Tier 3 | At-home rapid test results | 17 |
| Tier 4 | PCR lab confirmation (outcome) | 1 |

---

## Data Source

COVIDCARE Phase II Survey — MIT, December 2021  
822 participants | 472 variables | 70,983 pairwise knowledgebase entries

---

## References

1. Alemi F. DEMI: Directed Expectation-Maximization for Inference. Comparative Effectiveness, Spring 2026.
2. Menni C, et al. Real-time tracking of self-reported symptoms to predict COVID-19. *Nature Medicine*, 2020.
3. Larremore DB, et al. Test sensitivity is secondary to frequency and turnaround time. *Science Advances*, 2021.
4. Grant MC, et al. The prevalence of symptoms in 24,410 adults infected by SARS-CoV-2. *PLOS ONE*, 2020.
5. CDC. COVID-19 Testing Overview. cdc.gov/coronavirus. Accessed 2024.
