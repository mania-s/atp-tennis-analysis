# 🎾 ATP Tennis Match Analysis (2000–2026)

A data analysis project exploring professional ATP (men's) tennis matches from 2000 to 2026 — cleaning the data, visualizing it, and testing two statistical hypotheses about betting favourites and player rankings.

**Authors:** Sofia Ostreikova & Ivan Shiryaev
**Course project:** HSE, Introduction to Python for Data Science

---

## 📋 Overview

Each row in the dataset is a single ATP match with general match info, both players, and betting odds. The goal of the project is to describe and visualize the data, clean up invalid rows, and answer two questions:

1. Does the betting favourite really win more often — and does that depend on the court surface?
2. Does a bigger gap in ranking make the stronger player more likely to win — and is that effect stronger in best-of-5 matches?

## 📊 Dataset

- Source: [ATP Tennis 2000–2026, Daily Update (Kaggle)](https://www.kaggle.com/datasets/dissfya/atp-tennis-2000-2023daily-pull)
- ~68,000 matches, 17 columns grouped into: match context (tournament, surface, round...), players (names, winner), and numeric fields (rankings, ranking points, betting odds)
- Missing numeric values are encoded as `-1` in the raw data (e.g. ~23% of matches have no ranking points, ~6% have no odds) — these are converted to `NaN` and cleaned before analysis
- After cleanup, ~64,000 matches remain

## 🛠️ Tools & methods

- **pandas / numpy** — data cleaning, feature engineering, aggregation
- **matplotlib / seaborn** — visualization (histograms, box plots, scatter plots, heatmaps)
- **scipy.stats** — binomial and chi-square hypothesis tests
- **Jupyter Notebook** — full analysis end-to-end

## 🔍 Key findings

### Rankings and betting odds follow similar, right-skewed distributions
Most matches involve players ranked in the top 200 with odds close to 1–3, but a long tail of weaker players and longer odds pulls the mean above the median.

![Distribution of player ranking and betting odds](images/rank_odds_distribution.png)

### Worse ranking → higher odds
A clear upward trend confirms that bookmakers price in the ranking gap: players with a worse (higher) ranking number tend to get higher odds.

![Player ranking vs betting odds](images/rank_vs_odds_scatter.png)

### Rankings, points, and odds are closely correlated
The correlation heatmap shows the expected pattern — better rank goes with lower odds and more ranking points.

![Correlation between numeric fields](images/correlation_heatmap.png)

### Hard and Clay dominate the calendar; Carpet disappeared after 2009
Carpet courts were removed from the ATP tour after 2009. 2026 appears to drop off simply because the season isn't over yet.

![Matches per year by surface](images/matches_per_year_by_surface.png)

### Hypothesis 1 — favourites win ~70% of matches, and it varies slightly by surface
A binomial test confirms favourites win far more than the 50% coin-flip baseline; a chi-square test shows the win rate isn't identical across surfaces (best on Grass, slightly lower on Carpet/Clay).

![Favourite win rate by surface](images/favorite_winrate_by_surface.png)

### Hypothesis 2 — a bigger ranking gap predicts the winner, more so in best-of-5
When players are close in the rankings (gap 0–10) the stronger player wins ~55% of the time; with a 100+ gap that rises to 73–80%. The effect is consistently stronger in best-of-5 matches than best-of-3.

![Stronger player's win rate vs ranking gap](images/winrate_vs_rank_gap.png)

## ✅ Conclusion

Both hypotheses held up. Betting favourites win about 70% of matches — far more than chance — and the edge varies modestly by surface. A bigger ranking gap makes the stronger player noticeably more likely to win, and this effect is more pronounced in best-of-5 matches, where there's more room for the better player to assert themselves.

## ▶️ How to run

```bash
git clone https://github.com/mania-s/atp-tennis-analysis.git
cd atp-tennis-analysis
pip install pandas numpy matplotlib seaborn scipy jupyter
jupyter notebook
```

Download `atp_tennis.csv` from the [Kaggle dataset page](https://www.kaggle.com/datasets/dissfya/atp-tennis-2000-2023daily-pull) and place it in the same folder before running the notebook.

## 📁 Repository structure

```
.
├── ATP_Tennis_Analysis.ipynb   # full analysis notebook
├── images/                     # charts used in this README
└── README.md
```
