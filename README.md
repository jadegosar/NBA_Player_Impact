# Predicting NBA Player Impact

## Introduction
One of my favorite classes that I got the opportunity to take at the University of Notre Dame was Human Performance Analytics. A short description of the course, as given by the Notre Dame Course guidelines, is: "In this class we will learn how to extract insights from a range of data sources with the objective of maximizing athlete performance in competition. This includes optimizing physical readiness and avoiding injuries, long term player development and the identification of strategic advantages in competition which can be targeted by both athletes and coaches." My time learning about Human Performance Analytics, and taking Sports Analytics in my undergrad as well, really spurred my interest in the many roles analytics can play in the sports industry. I loved the fact that it could pair my interest in data analytics with my life-long passion for sports and the first-hand experience I gained with the opportunity to play soccer at the collegiate level. The culmination of the class was a final group project, one in which we were given the option to explore whatever Human Performance Analytics topic we found the most interesting. For my group, that was a project centered around the NBA and specifically whether we could predict the true impact a player would have on game outcomess by looking at point differential rather than just wins or losses. We chose to

## Data Description
The dataset we used to analyze this problem is the nbastatR package which is linked directly to the NBA Stats API. We used game logs from the 2018-2019 regular season as it was the last full season at the time of the project's completion to get data of player statistics from each individual game across the season. We aggregated the data from the individual athletes to create team level statistics for each game and created a loop to compile season averages at both levels. The data was formatted into two datasets: game_data and player_df. Game_data had 93 variables relating to in-game performance and over 4,000 samples representing team statistics while player_df had 45 variables and over 45,000 observations holding game performance metrics as well as other human performance variables from individual players.

## Methods
We initially ran a random forest model to predict game outcome, using all of the quantitative variables in the dataset. For this random forest model, we used 200 trees and an mtry of 84 for each variable in the game stat dataframe. This model looked at previous wins and losses to predict outcomes, but its accuracy level was only 0.575. We compared our random forest results to an XGBBoost model to determine which variables have the most predictive power. To achieve this, we extracted each variable’s importance but ultimately we decided that the random forest model was not powerful enough to accurately predict wins and losses.
We ran an XGBoost model to predict game point differential and to increase the power and applicability of our predictions. XGBoost gives misclassified samples more weight and avoids error on the test dataset, while maintaining flexibility in classification and evaluation. Thus, we find XGBoost ideal for a dataset as large as ours.
The Random Forest and XGBoost models revealed several different important features within the dataset. Running our model on the test data yielded an unimpressive 0.575 accuracy.
With “wins” as the positive class, a confusion matrix showed a sensitivity of 0.5832 and a specificity of 0.5667. These numbers mean that though our model is fairly balanced, the model is more likely to predict a loss over a win. In addition, we ran an importance matrix to determine the most influential variables in the Random Forest model. The importance matrix revealed that the most prominent variables were rebounds (both offensive and defensive), field goal (average of two and three pointer) percentage, and steals as is shown in Figure 1. Subsequently, we created an XGBoost model, using root mean squared error (RMSE) to evaluate its success. We set nrounds to 100 and the model yielded a 15.499 RMSE, which we further tuned in order to increase accuracy. After parameter tuning, the RMSE was 14.2 which meant that through tuning we were able to create a more accurate model. Though these results did not explicitly predict win or loss, the results can determine a game’s outcome by predicting if the point differential between home and away teams is positive or negative. Due to the fact that this model was looking at the most significant metrics for predicting performance at the team level, we thought the model would be most applicable to point spread betting and was helpful in determining what in-game performance statistics has a significant relationship with the point differential at the end of game.

## Results and Discussion (current at time of project completion)
We used the Random Forest and XGBoost models to collect the most valuable variables that impacted the game outcome and used that to evaluate individual performance. Both the Random Forest and XGBoost models prioritized steals, total rebounds, and two point field goal percentage (though these values were emphasized in a different order). Though the feature importance analysis revealed that steals are the most powerful metric, no variables in our XGBoost model were vastly more important than the others. Though both models have mediocre accuracy and high RMSE scores, they include the same variables, which implies that these metrics are important. Using these variables, we were able to analyze how much impact an individual athlete has on the point differential of the game meaning that we were able to compare the actual point differential to the predicted point differential if a key player was available for the game or was not available and replaced by an NBA player with league average stats. We decided to focus on three players in particular: Jayson Tatum, Nikola Jokic, and Chris Paul. 
Jayson Tatum is a three-time NBA all star and an Olympic gold medalist, as well as a forward for the Boston Celtics. As a 24 year old, he is a rising star and has the potential to be an important player for years to come. The data used in this project occurred early in his NBA career and, while he is a stronger player now, our model asserts that he still had a large impact on his team during the 2018-2019 season. For example, on November 5, 2018, against the Denver Nuggets, the Celtics lost by 8 points, with a final score of 107-115. The model predicted that the final score would be 105-115; without Tatum’s contributions, the model predicted a 96-115 point differential. Though the Celtics still lost, Tatum largely impacted his team’s performance in that game in a positive way. This type o projection could be supportive to coaches or performance staff when they are deciding what night Tatum should play of back-to-back if they feel he needs to rest one of the two or if there are other performance factors that need to be considered if they start to see a significant decline in his individual contributions to the team.
Nikola Jokic, also known as the Joker, has played for the Denver Nuggets since his rookie season in 2015-2016. The 27 year old is already in the top 10 all-time players with the most triple doubles. He also is a four-time NBA all star and was voted the NBA’s most valuable player in 2021. However, his value did not show on February 2, 2019 against the Timberwolves, in a back to back game after playing the Rockets. The Nuggets won by 10 points; our model predicts a Nuggets win by 3, though that differential increases to 8 without the Joker playing. The talented Jokic struggled in this back to back game, and the model apparently detected some pattern to reach this same conclusion. Moving forward, we would investigate how long Jokic takes to recover. 
Legendary player Chris is considered one of the greatest point guards of all time, with a number of awards and accolades too long to list. During the 2017-2018 and 2018-2019 seasons, Paul started for the Houston Rockets. For one game against the Utah Jazz, the model predicts a loss of 12 points without Paul, but a 3 point loss with him. The model was one basket away from the actual outcome, with the Rockets losing by 5 points. This pattern follows in other games: the Rockets will lose by less and win by more with Paul in the game.
However, since Paul is the oldest NBA player in the 2021 season, he needs more rest than younger players. Therefore, while he is a key player, coaches and performance staff could use this model to strategically prevent Paul’s fatigue and burnout.


## Conclusion
Our team sought to create a model that could predict NBA teams’ wins and losses, using extensive game data. Offensive and defensive rebounds, two point field goal percentage, and steals are the most influential predictors in our Random Forest model. Players who consistently get offensive boards are likely to have a high two point field goal percentages, so our model did detect existent patterns. However, overall accuracy is low at 0.575.
Rather than create a model to outright predict wins and losses, we created an XGBoost model to predict point differentials per game. The “stl_2_off” and “treb_2_def” variables are XGBoost’s most important predictors for predicting point differential. Stl_2_off records the visiting team’s average steals over the past 10 games; treb_2_def tracks the average rebounds that the visiting team allows over the past 10 games. Unsurprisingly, XGBoost prefers moving averages to individual game values, since aggregate metrics show a team’s consistency (or lack thereof). 
We then used the XGBoost model to predict the outcome of individual games and attribute outcomes to individual player contributions. To start, we evaluated contributions from Jayson Tatum, Nikola Jokic, and Chris Paul. We accomplished this by running the model twice—once with the original player’s metrics, and once with league average player statistics—and comparing the difference in point differential predictions to determine player contribution. The model, which consistently values individual players higher in lost games, correctly predicted whether a player’s team would win or lose for every game we analyzed.
In the future, we believe that our model could be applied to individual players across the to analyze their actual impact on an individual game level. Additionally, we would want to explore if this model could be applied to evaluate if players are a necessity to keep on the roster or, due to their overall influence being lower than expected, could be traded for more impactful players. Lastly, given more time and resources, we would like to look deeper into metrics such as days rest, minutes played, or if on a back-to-back game significantly contribute to performance changes for players if they do not have proper rest and recovery time between games.
