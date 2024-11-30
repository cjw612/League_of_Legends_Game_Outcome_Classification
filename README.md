# League of Legends Winrate Prediction

### Project Overview and Objective
This project aims to predict which team would win a League of Legends game using in-game data representing the game state at the 15-minute mark. In particular, given the vector of the in-game statistics $X_i$ of game $i$, we aim to predict the outcome $Y_i$ of game $i$, where $Y_i$ is a binary class denoting the win or loss of that particular game.

### Data Source
The dataset used for this analysis is the "match_data_v5.csv" dataset, originally created by Karlo Rusovan and Daria Komic on [Kaggle](https://www.kaggle.com/datasets/karlorusovan/league-of-legends-soloq-matches-at-10-minutes-2024/data).

### Data Structure
This dataset contains 29 columns and 24224 rows, with the first column being the matchID and the last column being an indicator of which team had won that game. The remaining columns represent in-game statistics of both teams, including gold earned, minions slain, turrets destroyed, etc.

|matchID|blueTeamControlWardsPlaced|...|redTeamControlWardsPlaced|...|blueWin|
|-------|--------------------------|---|-------------------------|---|-------|
|EUW1_6882489515|2|...|34|...|1|
|...|...|...|...|...|
|EUW1_6881140491|6|...|1|...|1|

_Sample snapshot of dataset_

### Data Cleaning and Preparation
The dataset does not contain missing values. However, prior to analyzing the data, we performed necessary feature transformation and outlier deletion based on domain knowledge. In particular, we performed the following tasks:

- Created features that represent the difference between a particular column between teams.
- Transferred necessary features to qualitative variables
- Removed outlier games indicated by winning even with a large gold deficit at 15 minutes/losing even with a large gold lead at 15 minutes, which constitutes to around 3% of the total data.

### Exploratory Data Analysis
EDA in this project is aimed to address the following questions:

- What are the correlations between features?
- What are the distributions of quantitative features?
- What is the difference in the distribution of quantitative features across the two target classes?

### Data Analysis
Four different models are deployed in this analysis to determine which model performs the best in this dataset:
- Logistic Regression with L1 penalty
- Linear Discriminant Analysis (LDA)
- Random Forest
- XG Boosting with hyperparameter optimization

In addition, we performed model selection with K-fold Cross-Validation with $K = 5$ to lower the variance of our results.

### Results
The results of the four models are summarized as follows:

|Model|Accuracy|Precision|Recall|F1-Score|
|-----|--------|---------|------|--------|
|Logistic Regression|0.784158|0.783160|0.780529|0.781826|
|LDA|0.784073|0.785103|0.776931|0.780966|
|Random Forest|0.776581|0.782572|0.760548|0.771334|
|XGB|0.779816|0.787437|0.761364|0.774055|

### Limitations
- As some features are highly correlated, implementing a more sophisticated outlier detection algorithm coupled with current domain knowledge-based outlier detection may further improve the results.
- In practice, gold difference at the 15-minute mark does not guarantee the outcome of the game. For example, for team compositions that are late game-focused, a gold deficit at the 15-minute mark may not effect the outcome of the game. Therefore, incorporating the champion compositions of both teams may increase prediction accuracy.
- Incorporating player metadata (e.g., proficiency of champion, rank) may also increase prediction accuracy, as the current dataset assumes that all players are homogenous. 

