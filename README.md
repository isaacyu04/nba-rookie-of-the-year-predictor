# NBA Rookie of the Year Predictor

A predictive analytics project completed for the NBA Future Analytics Stars Tech Challenge / Rising Stars Analyst Program. The analysis estimates 2025–26 NBA Rookie of the Year likelihoods from rookie regular-season statistics.

This project won from 2400+ submissions, accepting me into the 3rd cohort of the NBA Future Analytics Stars.

For a quick video explanation of this project, click this link: [https://youtu.be/EM-kIXQVa9s]([url](https://youtu.be/EM-kIXQVa9s))

## Portfolio artifact

- [`ROY_Predictor.Rmd`](ROY_Predictor.Rmd) — complete R Markdown analysis: preparation, exploratory analysis, model training, evaluation, and scoring.
- [`ROY_Predictor.pdf`](ROY_Predictor.pdf) — rendered project report.
- [`predictions.csv`](predictions.csv) — scored current-rookie output from the full random-forest model.
- `Previous_Rookies*.csv` and `Current_Rookies*.csv` — historical and current basic/advanced-stat inputs.

## Data

The model joins two data families by player and team:

| Dataset | Records | Purpose |
| --- | ---: | --- |
| Historical basic rookie statistics | 1,450 | Training outcomes, including the `ROY_winner` label |
| Historical advanced rookie statistics | 1,450 | Efficiency, usage, pace, and rating features |
| Current basic rookie statistics | 63 | Scoring input |
| Current advanced rookie statistics | 63 | Scoring input |

The supplied inputs use player statistics and include fields such as points, rebounds, assists, steals, blocks, offensive/defensive rating, true-shooting percentage, usage, pace, and possessions.

## Approach

1. Normalizes player/team text, joins basic and advanced statistics, and removes redundant or highly correlated predictors.
2. Uses a stratified 70/30 historical train/test split and class weights because Rookie of the Year winners are rare.
3. Compares lasso logistic regression, a full random forest, a feature-reduced random forest, and a five-fold cross-validated random forest.
4. Selects the full random forest for scoring based on the report's held-out-data discussion.

The committed `predictions.csv` ranks Cooper Flagg, VJ Edgecombe, and Kon Knueppel as its three highest-probability prospects in this snapshot. These are model outputs, not claims about the eventual award result.

## Reproduce the analysis

### Requirements

- R
- R packages: `dplyr`, `stringi`, `stringr`, `ggplot2`, `corrplot`, `gridExtra`, `caret`, `glmnet`, `ROCR`, `e1071`, and `randomForest`

### Render

```r
install.packages(c(
  "dplyr", "stringi", "stringr", "ggplot2", "corrplot", "gridExtra",
  "caret", "glmnet", "ROCR", "e1071", "randomForest", "rmarkdown"
))
rmarkdown::render("ROY_Predictor.Rmd")
```

Run the command from this repository so the relative CSV paths resolve.

## Notes

This repository preserves the submitted analysis and its data snapshot. The predictions reflect that historical snapshot; they should not be interpreted as live forecasts.
