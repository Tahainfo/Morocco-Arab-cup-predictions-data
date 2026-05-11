# Arab Cup 2025 Final — Morocco vs Jordan: Match Prediction Model

> **Actual result: Morocco 3-2 Jordan** — ranked **#2** on the model's probability list.

---

## Overview

A Monte Carlo simulation model that predicted Morocco's victory in the FIFA Arab Cup 2025 Final against Jordan. Using only shots-on-target statistics from each team's five tournament matches, the model computed expected goals and ran **1,000,000 match simulations** to generate a full probability distribution over all possible scores.

---

## Key Results

| Outcome | Probability |
|---------|-------------|
| **Morocco wins** | **66.16%** |
| Jordan wins | 23.59% |
| Draw | 10.25% |

### Top 5 Most Probable Scores

| Rank | Score | Probability |
|------|-------|-------------|
| 1 | Morocco 2–1 Jordan | 7.58% |
| **2** | **Morocco 3–2 Jordan ✓ (ACTUAL RESULT)** | **7.01%** |
| 3 | Morocco 3–1 Jordan | 6.92% |
| 4 | Morocco 5–1 Jordan | 5.64% |
| 5 | Morocco 4–1 Jordan | 5.09% |

---

## Methodology

### 1. Data Collection
For each team's 5 tournament matches (group stage + quarterfinal + semifinal), the following were recorded:
- Shots on target (offensive)
- Shots on target conceded (defensive)
- Goals scored

### 2. Conversion Factor (xG Proxy)

The empirical shot-to-goal conversion rate for each team across the tournament:

```
conversion = total goals scored / total shots on target
```

| Team | Goals | Shots on Target | Conversion |
|------|-------|-----------------|------------|
| Morocco | 8 | 22 | **0.3636** |
| Jordan | 10 | 27 | **0.3703** |

### 3. Expected Goals (Lambda)

```
λ_team = mean_attack_SoT × mean_defense_SoT_opponent × (conversion / 1.6)
```

The calibration factor `1.6` prevents over-estimation for high-stakes knockout matches.

| Parameter | Morocco | Jordan |
|-----------|---------|--------|
| Mean SoT (attack) | 4.40 | 5.40 |
| Mean SoT (defense) | 1.40 | 3.00 |
| **Expected goals λ** | **3.00** | **1.75** |

### 4. Monte Carlo Simulation

- **1,000,000 iterations**
- Goals sampled from Poisson distribution: `X ~ Poisson(λ)`
- Draws handled with extra time: add `Poisson(0.3)` goals per team
- Score distribution estimated from empirical frequencies

---

## Files

| File | Description |
|------|-------------|
| [`maroc.txt`](maroc.txt) | Morocco's match statistics (5 games) with SoT breakdown |
| [`jordan.txt`](jordan.txt) | Jordan's match statistics (5 games) with SoT breakdown |
| [`maroc_jordan.ipynb`](maroc_jordan.ipynb) | Full Python analysis notebook |

---

## How to Run

**Requirements:**
```bash
pip install numpy pandas
```

**Launch notebook:**
```bash
jupyter notebook maroc_jordan.ipynb
```

---

## Morocco Tournament Path

| Stage | Opponent | Score | SoT (att) | SoT (def) |
|-------|----------|-------|-----------|-----------|
| Group 1 | Comoros | 3–1 | 5 | 3 |
| Group 2 | Oman | 0–0 | 0 | 1 |
| Group 3 | Saudi Arabia | 1–0 | 2 | 0 |
| Quarter-final | Syria | 1–0 | 8 | 1 |
| Semi-final | UAE | 3–0 | 7 | 2 |

## Jordan Tournament Path

| Stage | Opponent | Score | SoT (att) | SoT (def) |
|-------|----------|-------|-----------|-----------|
| Group 1 | UAE | 2–1 | 6 | 2 |
| Group 2 | Kuwait | 3–1 | 6 | 2 |
| Group 3 | Egypt | 3–0 | 6 | 7 |
| Quarter-final | Iraq | 1–0 | 4 | 3 |
| Semi-final | Saudi Arabia | 1–0 | 5 | 1 |

---

## Key Takeaway

A lightweight statistical model using **10 data series** (5 matches × 2 teams), combined with **1,000,000 Monte Carlo simulations**, was able to:

1. Correctly predict Morocco as the winner (66% confidence)
2. Rank the actual score (3–2) as the **2nd most likely outcome** (7.01%)

This demonstrates that principled probabilistic modeling — even with minimal data — can outperform uninformed prediction significantly.

---

## Author

**Ismaili Taha** | Data Science Enthusiast  
[LinkedIn](https://www.linkedin.com) · [GitHub](https://www.github.com)
