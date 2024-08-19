# Predicting NBA Player Impact

## Introduction
One of my favorite classes that I got the opportunity to take at the University of Notre Dame was Human Performance Analytics. A short description of the course, as given by the Notre Dame Course guidelines, is: "In this class we will learn how to extract insights from a range of data sources with the objective of maximizing athlete performance in competition. This includes optimizing physical readiness and avoiding injuries, long term player development and the identification of strategic advantages in competition which can be targeted by both athletes and coaches." My time learning about Human Performance Analytics, and taking Sports Analytics in my undergrad as well, really spurred my interest in the many roles analytics can play in the sports industry. I loved the fact that it could pair my interest in data analytics with my life-long passion for sports and the first-hand experience I gained with the opportunity to play soccer at the collegiate level. The culmination of the class was a final group project, one in which we were given the option to explore whatever Human Performance Analytics topic we found the most interesting. For my group, that was a project centered around the NBA and specifically whether we could predict the true impact a player would have on game outcomess by looking at point differential rather than just wins or losses. We chose to

## Data Description
The dataset we used to analyze this problem is the nbastatR package which is linked directly to the NBA Stats API. We used game logs from the 2018-2019 regular season as it was the last full season at the time of the project's completion to get data of player statistics from each individual game across the season. We aggregated the data from the individual athletes to create team level statistics for each game and created a loop to compile season averages at both levels. The data was formatted into two datasets: game_data and player_df. Game_data had 93 variables relating to in-game performance and over 4,000 samples representing team statistics while player_df had 45 variables and over 45,000 observations holding game performance metrics as well as other human performance variables from individual players.

## Methods


## Results and Discussion


## Conclusion
