# League of Legends Winrate Prediction

### Project Overview and Objective
This project aims to predict which team would win a League of Legends game using in-game data representing the game state at the 15-minute mark. In particular, given the vector of the in-game statistics $X_i$ of game $i$, we aim to predict the outcome $Y_i$ of game $i$, where $Y_i$ is a binary class denoting the win or loss of that particular game.

### Data Source
The dataset used for this analysis is the "match_data_v5.csv" dataset, originally created by Karlo Rusovan and Daria Komic on [Kaggle](https://www.kaggle.com/datasets/karlorusovan/league-of-legends-soloq-matches-at-10-minutes-2024/data).

### Data Structure
This dataset contains 29 columns, with the first column being the matchID and the last column being an indicator of which team had won that game. The remaining columns represent in-game statistics of both teams, including gold earned, minions slain, turrets destroyed, etc.

|matchID|blueTeamControlWardsPlaced|...|redTeamControlWardsPlaced|...|blueWin|
|-------|--------------------------|---|-------------------------|---|-------|
|EUW1_6882489515|2|...|34|...|1|
|...|...|...|...|...|
|EUW1_6881140491|6|...|1|...|1|

_Sample snapshot of dataset_

### Data Cleaning and Preperation
The dataset does not contain missing values. However, prior to analyzing the data, we performed necessary feature transformation and outlier deletion based on domain knowledge. In particular, we performed the following tasks:

- Created features that represent the difference between a particular column between teams.
- Transferred necessary features to qualitative variables
- Removed outlier games indicated by winning even with a large gold deficit at 15 minutes/losing even with a large gold lead at 15 minutes, which constitutes to around 3% of the total data.

### Exploratory Data Analysis
EDA in this project is aimed to answer the following questions:

- What are the correlations between features?
- What are the distributions of quantitative features?
- What is the difference of the distribution of quantitative features across the two target classes? 
