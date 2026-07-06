# Uncovering-Patterns-in-MLB-Performance-Data

## Project Overview

This project analyzes Major League Baseball Statcast data to uncover patterns in batted ball outcomes, hit locations, and player performance across game situations. Using the 2019 Statcast season, the analysis applies supervised machine learning, unsupervised clustering, and dimensionality reduction methods to model how swing characteristics, hit coordinates, and in-game context relate to player outcomes.

The project was completed for a graduate-level statistical learning course and focuses on three complementary questions: predicting whether a batted ball results in a hit, out, or home run; identifying hit type from batted ball coordinates; and determining which game-situation features contribute most to offensive performance.

![Hit Coordinates of Batted Balls](figures/hit_coordinates.png)

*Figure 1. Hit coordinates of batted balls colored by type of hit.*

---

## Research Questions

1. Can we predict whether a batted ball will result in a hit, out, or home run based on swing characteristics?
2. Can we identify the type of batted ball, such as single, double, triple, home run, sacrifice bunt, or sacrifice fly, using hit coordinates?
3. What are the key factors contributing to player performance in different game situations?

---

## Dataset

The analysis uses the **2019 MLB Statcast dataset**, which contains pitch-level and batted-ball-level information collected using MLB tracking technology. The 2019 season was selected to maintain consistency in data collection and reduce computational overhead.

The dataset contains:

- 732,473 observations
- 93 original features
- Pitch characteristics
- Swing and batted ball metrics
- Hit coordinates
- Game context variables
- Player performance metrics

Key engineered variables include:

- `outcome`: grouped into `hit`, `out`, and `home_run`
- `type_of_hit`: grouped into `single`, `double`, `triple`, `home_run`, `sac_bunt`, and `sac_fly`
- `team_at_bat`: indicates whether the home or away team was batting

---

## Methods

### Data Preprocessing

- Removed deprecated and irrelevant variables
- Filtered observations with missing pitch release speed
- Created outcome and hit-type labels
- Handled missing values based on variable meaning
- One-hot encoded categorical variables where needed
- Used stratified train-test splitting for supervised models

### Exploratory Data Analysis

- Exit velocity by batted ball outcome
- Hit coordinate distributions by hit type
- wOBA variation across pitch types
- Correlation analysis among numeric features
- Distributional checks for model assumptions

### Research Question 1: Batted Ball Outcome Classification

Models used:

- Random Forest
- XGBoost
- Feedforward Neural Network

Model evaluation included:

- Accuracy
- Precision
- Recall
- F1 score
- Confusion matrices
- 5-fold cross-validation

Traditional models such as multinomial logistic regression, LDA, and QDA were considered but rejected because the data showed multicollinearity, non-linearity, and violations of normality assumptions.

### Research Question 2: Hit-Type Clustering

- Spectral clustering was applied to hit coordinate data.
- A random sample of 5,000 observations was used due to computational cost.
- Clustering was used to evaluate whether natural groupings of hit types could be recovered from batted ball location.

### Research Question 3: Player Performance Factors

- Principal Component Analysis (PCA) was used for dimensionality reduction.
- XGBoost was applied to principal components to identify features associated with wOBA.
- Feature importance and component loadings were used to interpret influential game-situation variables.

---

## Key Findings

### Batted Ball Outcome Prediction

- Random Forest, XGBoost, and Neural Network models were effective for predicting batted ball outcomes.
- Random Forest achieved strong predictive performance and served as an interpretable baseline.
- Tree-based methods were well-suited to the nonlinear and high-dimensional structure of the Statcast data.

### Hit-Type Clustering

- Hit coordinates showed clear spatial structure by type of hit.
- Home runs, singles, doubles, and sacrifice bunts occupied distinct regions of the field.
- Spectral clustering was appropriate because the hit-location clusters were non-convex and unevenly distributed.

### Player Performance Analysis

- PCA reduced the dimensionality of the game-context feature space.
- XGBoost helped identify important components associated with offensive performance.
- The analysis highlighted the value of combining dimensionality reduction with machine learning for interpreting high-dimensional baseball data.

---

## Repository Structure

```text
MLB-Performance-Analysis/
│
├── analysis/
│   └── MLB_Analysis_Final.Rmd
│
├── data/
│   └── Statcast_2019.csv
│
├── figures/
│   ├── exit_velocity_by_outcome.png
│   ├── hit_coordinates.png
│   ├── woba_by_pitch_type.png
│   ├── confusion_matrix_random_forest.png
│   └── spectral_clustering.png
│
├── report/
│   ├── Report.pdf
│   └── mlb_analysis_final.pdf
│
└── README.md
```

---

## Software and Packages

The analysis was conducted in **R** using packages including:

- tidyverse
- caret
- recipes
- rsample
- randomForest
- xgboost
- nnet
- yardstick
- pROC
- corrplot
- MASS
- ggplot2
- dplyr

---

## Reproducibility

1. Clone the repository.
2. Download or place `Statcast_2019.csv` in the `data/` folder.
3. Open `analysis/MLB_Analysis_Final.Rmd`.
4. Install the required R packages.
5. Knit the R Markdown file to reproduce the analysis, figures, and model results.

---

## Author

**Nevena Ciganovic**  
M.Sc. Statistical Sciences  
University of Toronto

Project collaborators: **Adele Lauzon** and **Joanna Lo**

---

## License

This repository is intended for academic and educational purposes. The MLB Statcast data remain subject to the licensing terms of the original data provider.
