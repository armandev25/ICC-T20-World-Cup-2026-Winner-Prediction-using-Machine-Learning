# ICC 2026 Men’s T20 World Cup – Winner Prediction using Machine Learning

**An end-to-end probabilistic simulation of the ICC Men’s T20 World Cup 2026 using historical T20I data, machine learning, and tournament simulation logic.**

![Python](https://img.shields.io/badge/Python-3.9+-blue)
![Machine Learning](https://img.shields.io/badge/Machine%20Learning-Logistic%20Regression-orange)
![Status](https://img.shields.io/badge/Project-Completed-success)
![Dataset](https://img.shields.io/badge/Dataset-Kaggle-lightgrey)
![License](https://img.shields.io/badge/License-MIT-green)
![Notebook](https://img.shields.io/badge/Jupyter-Notebook-orange)

---

## Project Overview

This project presents a data-driven machine learning system to simulate and predict the outcome of the ICC Men’s T20 World Cup 2026.

Rather than producing a single deterministic prediction, the system:

- Estimates match-level win probabilities
- Simulates the complete ICC tournament structure
- Quantifies qualification probabilities and championship win likelihood
- Produces interpretable visual analytics for each stage of the tournament

The final simulation predicts a high-probability **India vs Australia final**, with **India emerging as the most likely champion**.

---

## Problem Statement

How can historical T20 International match data be used to probabilistically simulate a future ICC tournament while respecting official tournament rules and inherent uncertainty?

### Key challenges addressed
- High randomness and volatility of T20 cricket
- Unequal historical data availability across teams
- Preventing data leakage in time-series modeling
- Maintaining interpretability of probabilistic outputs

---

## Solution Architecture

Historical T20I Data (2005–2024)  
↓  
Feature Engineering  
(Rolling Team Statistics)  
↓  
Machine Learning Model  
(Logistic Regression)  
↓  
Match Win Probabilities  
↓  
Tournament Simulation Engine  
(Group → Super 8 → Semi-Finals → Final)  
↓  
Qualification % and Championship Win %

---

## Dataset

- **Source:** Kaggle – *All T20 Internationals Dataset (2005–2024)*
- **Matches Covered:** 2,500+ T20 Internationals

### Key fields used
- Match results
- Team runs and wickets
- Toss information
- Match dates and venues

Only match-level structured data was used for modeling.

---

## Feature Engineering

Time-aware rolling features were engineered for each team:

- Win percentage (last 10 matches)
- Average runs scored (last 10 matches)
- Average runs conceded (last 10 matches)
- Relative team strength (Team1 − Team2)
- Toss advantage indicator

All features were computed strictly from past matches only, ensuring zero data leakage.

---

## Model Details

- **Model Used:** Logistic Regression
- **Reason:** Strong probability calibration, suitable for simulation-based analysis
- **Validation Strategy:** Time-based train–test split

### Performance
- **Accuracy:** ~73–74%
- **Log Loss:** ~0.51

Probability calibration was prioritized over raw accuracy due to the stochastic nature of T20 cricket.

---

## Handling Data Sparsity

Certain teams (e.g., USA, Nepal, Italy) have limited historical match data.

### Mitigation strategy
- Fallback to global-average team statistics
- Prevents instability while maintaining fairness

This approach mirrors practices used in real-world sports analytics.

---

## Tournament Simulation Logic

### Group Stage
- 4 groups (A–D)
- Automatic points table generation
- Top 2 teams from each group qualify

**Visualizations:**  
<img width="590" height="390" alt="image" src="https://github.com/user-attachments/assets/46f04ce0-a55f-4c7d-828a-a07822a8ad08" />
<img width="590" height="390" alt="image" src="https://github.com/user-attachments/assets/41e9cdc4-3473-4149-b42c-7de4ad6a77fb" />
<img width="590" height="390" alt="image" src="https://github.com/user-attachments/assets/9529b462-5974-42e8-aac1-62ca3bc8ec15" />
<img width="590" height="390" alt="image" src="https://github.com/user-attachments/assets/e8810001-b106-4382-833c-98910bdb0fec" />

---

### Super 8 Stage (ICC Logic)

Qualified teams are reorganized into two Super 8 groups:

- **Group G1:** A1, B2, C1, D2
- **Group G2:** A2, B1, C2, D1

Each group follows a round-robin format.

**Visualizations:**  
<img width="590" height="390" alt="image" src="https://github.com/user-attachments/assets/1aaaf24e-7f4e-43d4-9377-03783fecbd4c" />
<img width="590" height="390" alt="image" src="https://github.com/user-attachments/assets/94f0a64a-db03-4395-a75b-845adc0030df" />

---

## Knockout Stage

### Semi-Finals
- SF1: Winner G1 vs Runner-up G2
- SF2: Winner G2 vs Runner-up G1

Match outcomes are based on expected win probabilities, avoiding single-run randomness during presentation.

**Visualization:**  
<img width="889" height="490" alt="image" src="https://github.com/user-attachments/assets/2bdcf1e8-f18a-4eee-9424-f562a87c533a" />

---

### Final

The final match compares both finalists’ win probabilities, clearly highlighting the favourite.

**Visualization:**  
<img width="390" height="390" alt="image" src="https://github.com/user-attachments/assets/6a99f694-9e17-4a0b-b9d3-920350769deb" />

---

## Championship Win Probability (Monte Carlo)

The entire tournament was simulated thousands of times to estimate:

- Qualification probability
- Championship win probability

To improve interpretability, probabilities are normalized among major contenders for visualization.

**Visualization:**  
<img width="590" height="390" alt="image" src="https://github.com/user-attachments/assets/da05258e-32d0-4bde-8e30-a533f5330e0f" />

---

## Key Insights

- Tournament win probabilities decay rapidly due to compounding effects
- Probability calibration is more important than raw accuracy
- Visualization choices significantly affect interpretability
- Clear separation between simulation logic and presentation logic is essential

---

## Limitations and Observations

Some championship win probabilities may appear counter-intuitive when compared with real-world cricket expectations.

This is primarily due to:
- Compounding probability effects across knockout stages
- Rolling-window bias based on recent form
- Data sparsity for associate nations
- Absence of historical prestige priors

To address this, normalized probabilities among major contenders are presented for visualization, while raw Monte Carlo outputs are preserved for analytical integrity.

The model’s primary objective is match-level and progression-level prediction, not absolute certainty.

---

## Future Improvements

- Player-level modeling
- Venue-specific effects
- Net Run Rate simulation
- ELO-based team ratings
- Interactive Streamlit dashboard
- Extension to IPL and ODI World Cups

---

*This project was built for learning, experimentation, and analytical rigor — not betting or gambling.*

