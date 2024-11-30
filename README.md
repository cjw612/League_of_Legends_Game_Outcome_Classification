# League of Legends Game Outcome Prediction

### Project Overview and Objective
This project aims to predict which team would win a League of Legends game using in-game data representing the game state at the 15-minute mark. In particular, given the vector of the in-game statistics $X_i$ of game $i$, this project aims to construct a classifier $C$ to predict the outcome $Y_i$ of game $i$, where $Y_i$ is a binary class denoting the win or loss of that particular game.

### Data Source
The dataset used for this analysis is the "match_data_v5.csv" dataset, originally created by Karlo Rusovan and Daria Komic on [Kaggle](https://www.kaggle.com/datasets/karlorusovan/league-of-legends-soloq-matches-at-10-minutes-2024/data).

### Data Structure
This dataset contains 24,224 rows representing unique games and 29 columns, with the first column being the matchID and the last column being an indicator of which team had won that game. The remaining columns represent in-game statistics of both teams, including gold earned, wards placed, turrets destroyed, etc.

|matchID|blueTeamControlWardsPlaced|...|redTeamControlWardsPlaced|...|blueWin|
|-------|--------------------------|---|-------------------------|---|-------|
|EUW1_6882489515|2|...|34|...|1|
|...|...|...|...|...|
|EUW1_6881140491|6|...|1|...|1|

_Sample snapshot of dataset_

### Data Cleaning and Preparation
The dataset does not contain missing values. However, prior to analyzing the data, we performed necessary feature transformation and outlier deletion based on domain knowledge. In particular, we performed the following tasks:

- Created features that represent the difference between a particular column between teams.
- Transformed necessary features to qualitative variables
- Removed outlier games indicated by winning even with a significant gold deficit at 15 minutes/losing even with a significant gold lead at 15 minutes, which constitutes around 3% of the total games.

### Exploratory Data Analysis
EDA in this project is aimed to address the following questions:

- What are the correlations between features?
- What are the distributions of quantitative features?
- What is the difference in the distribution of quantitative features across the two target classes?

### Data Analysis
Four different models are deployed in this analysis to determine which model performs the best on this dataset:
- Logistic Regression with L1 penalty
- Linear Discriminant Analysis (LDA)
- Random Forest
- XGBoost with Bayesian hyperparameter optimization

In addition, K-fold Cross-Validation with $K = 5$ is also implemented for model selection to lower the variance of the results.

### Results
The results of the four models are summarized in the following table:

|Model|Accuracy|Precision|Recall|F1-Score|
|-----|--------|---------|------|--------|
|Logistic Regression|0.784200|0.783132|0.780701|0.781897|
|LDA|0.784456	|0.785814|0.776755|0.781230|
|Random Forest|0.777219|0.783135|0.761377|0.772021|
|XGBoost|0.781987|0.792955|0.758099	|0.775049|

### Limitations
- As some features are highly correlated, implementing a more sophisticated outlier detection algorithm coupled with current domain knowledge-based outlier detection may further improve the results.
- In practice, gold difference at the 15-minute mark does not guarantee the outcome of the game. For example, for team compositions that are more late game-focused, a gold deficit at the 15-minute mark may not affect the outcome of the game. Therefore, incorporating the champion compositions of both teams may further increase prediction accuracy.
- Incorporating player metadata (e.g., proficiency of champion, rank) may also increase prediction accuracy, as the current dataset assumes that all players are homogenous. 

### References
League of Legends SoloQ matches at 15 minutes 2024. (2024). Karlo Rusovan and Daria Komic. Kaggle.
https://www.kaggle.com/datasets/karlorusovan/league-of-legends-soloq-matches-at-10-minutes-2024/data
