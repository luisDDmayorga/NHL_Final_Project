# Becoming a NHL analyst from scracht

## Creating a model able to predict if a team will make the PlayOffs this season (21-22)
## Creating a model able to predict the player performance this season (21-22)

<p align="center"><img width="300" alt="nhl" src="https://user-images.githubusercontent.com/90793442/146153272-dc60850c-ca8f-46ed-a2c0-fb368696fd5e.png"></p>

## Table of contents
- [Project Brief](#PB)
- [Data](#DT)
- [Process & Tools](#PT)
- [Visualization](#VI) 
- [Key Takeaways](#KT)

<a name="PB"></a>
## Project Brief
I've always been pasionate about sports. Since I was a kid I've loved watching basketball, tennis, judo or boxing... but never hockey. That's the reason why I've chosen this project: becoming an NHL analyst without ever having watched any game or even understanding the rules.
<p style='text-align: justify;'>The main objective of the project is to be able to predict which teams are going to make the playoffs at the end of the current season, based on data from past years. Once I achieve that, I will try to predict the players performance during this season (based on their performance from past years) and create my own team capable of winning the league at the end of the season. </p>

<a name="DT"></a>
## Data
The data whas obtained by scrapping from an official NHL API. The documentation of the API was a bit messy but I found a [GitLab repo](https://gitlab.com/dword4/nhlapi/-/blob/master/stats-api.md) where it was super detailed.  
For the playoff prediction, the dataframe obtained consists on:
- 574 samples
- 14 columns:season, team_id, team_name, gamesplayed_x,
       goals_against_per_game, goals_scored_per_game, power_play_goals,
       power_play_goals_against, power_play_opportunities,
       shots_per_game, shots_allowed_per_game, gamesplayed_y, points,
       rank
- Target value: points
For further details on all features, please refer to [notebook 1](https://github.com/luisDDmayorga/NHL_Final_Project/blob/main/Jupyter%20Notebooks/PlayOffs%20Prediction%20-%20Final%20Project.ipynb)

<img width="1129" alt="Captura de pantalla 2021-12-15 a las 12 44 36" src="https://user-images.githubusercontent.com/90793442/146180676-1c857c53-032e-4af6-9d88-dcd40ecb068e.png">

For the players perfonces prediction, the dataframe obtained consists on:
- 12055 samples
- 29 columns: name, position, country, birthday, id, height, weight,
       goals_1, assists_1, pim_1, games_1, hits_1, hots_1,
       time_1, plus_minus_1, goals_2, assists_2, pim_2, games_2,
       hits_2, shots_2, time_2, plus_minus_2, season_1, season_2,
       season_3, ppg_3, team_1 and team_2
- Target value: ppg_3
For further details on all features, please refer to [notebook 2](https://github.com/luisDDmayorga/NHL_Final_Project/blob/main/Jupyter%20Notebooks/Players%20performance%20Prediction%20-%20Final%20Project.ipynb)

<img width="1112" alt="Captura de pantalla 2021-12-15 a las 12 41 19" src="https://user-images.githubusercontent.com/90793442/146180277-78e07170-a896-4e35-b674-79ca2da332a9.png">

<a name="PT"></a>
## Process & Tools
**Process**

The process includes:
- Learning rules of the NHL - how many games per season, maximum points that can be gained per game, etc
- Understanding hockey stats
- Finding out wich are the best teams in the league
- Finding out who are the superstars players in the league
- __Playoff Precictions:__
  - Scrapping teams stats from past seasons
  - Converting total stats into stats per game - scaling data
  - Exploratory Data Analysis - EDA:
    - Dealing with nulls
    - Finding Correlations - dropping power_play_opportunities - high correlated - (after experimenting leaving it)
    - Dropping irrelevant features for modeling - season, team_id, team_name, gamesplayed_x, gamesplayed_y, rank
<p align="center"><img width="513" alt="Captura de pantalla 2021-12-15 a las 12 45 32" src="https://user-images.githubusercontent.com/90793442/146180823-d32f6001-626d-4a38-9449-49c9bc4642c9.png"></p>

  - Preparing data for modeling:
    - Isolate target value
    - Trying different scalers - in the end I opted not to use any as my data was already scaled by number of games
  - Tried different Machine learning models for regression as follows:
    - **_Model 1:_ Linear Model**
    - _Model 2:_ Decission Tree
    - _Model 3:_ Random Forest
    - _Model 4:_ Stack Best of - Linear Model, Decission Tree, Random Forest
    - _Model 5:_ Stack Best of - Linear Model, Random Forest
  - Comparing models
<p align="center"><img width="565" alt="Captura de pantalla 2021-12-15 a las 13 02 18" src="https://user-images.githubusercontent.com/90793442/146183064-382f8455-23ba-46cc-9778-ec4660863d0c.png"></p>

  - Scrapping teams in current season
  - Process data the same way as I've done with the past seasons teams
  - Using _Model 1_ to predict teams points per game
  - Ranking teams and adding a playoff columns to say if they will make the playoffs or not

<p align="center"><img width="980" alt="Captura de pantalla 2021-12-15 a las 14 21 43" src="https://user-images.githubusercontent.com/90793442/146194013-a4f57599-650f-41db-9b66-097ddc71b6cb.png"></p>

- __Players performance prediction__
  - Scrapping player stats from past seasons
  - Exploratory Data Analysis - EDA:
    - Dealing with nulls
    - Transforming weight into kg and height into cms
    - Creating 'age' column
    - Changing 'birthday' type to DateTime
    - Creating 'games_per_season' columns
    - Changing 'time' and 'season' columns format 
    - Creating 'points' columns
    - Converting total stats into stats per game - scaling data
    - Dealing with outliers - Dropping some outliers (after experimenting leaving some of them)
    - Finding correlation - Dropping some columns (after experimenting leaving some of them)
    - Selecting relevant features for modeling (after experiment with some others)
    - Plotting data in scatter matrix

 <p align="center"><img width="587" alt="Captura de pantalla 2021-12-15 a las 14 36 36" src="https://user-images.githubusercontent.com/90793442/146196339-99134b2b-eb04-4303-8291-17262c0eb907.png"></p>
 
  - Preparing data for modeling:
    - Isolate target value
    - Trying different scalers - in the end I opted not to use any as my data was already scaled by number of games
  - Tried different Machine learning models for regression as follows:
    - _Model 1:_ Linear Model
    - _Model 2:_ Decission Tree
    - _Model 3:_ Random Forest
    - **_Model 4:_ Stack Best of - Linear Model, Decission Tree, Random Forest**
    - _Model 5:_ Stack Best of - Linear Model, Random Forest
    - _Model 6_ Neural Network
  - Comparing models

<p align="center"><img width="500" alt="Captura de pantalla 2021-12-15 a las 14 39 27" src="https://user-images.githubusercontent.com/90793442/146196790-a7fdb883-9cf7-4f77-8375-ab82b38814b4.png"></p>

  - Scrapping players in current season
  - Process data the same way as I've done with the past seasons players
  - Using _Model 4_ to predict teams points per game
  - Create dataframe with players and predicted points

**Tools**

- Scrapping Data - [NHL API](https://gitlab.com/dword4/nhlapi/-/blob/master/stats-api.md)
- Code: [Jupyter Notebook](https://github.com/luisDDmayorga/NHL_Final_Project/tree/main/Jupyter%20Notebooks)
- Vizualizations: [Tableau] / Pandas / Seaborn / Matplotlib
- Presentation: [Keynote]

<a name="KT"></a>
## Key Takeaways

**PlayOffs prediction:** The best model was _Model 1_ - Linear Regression Model. With it, my predictions have the following socores:
- R2 - 0.86
- MSE - 0.0038
- RMSE - 0.062
This means that for a whole season, my predictions are wrong in just about 0.3 points per team - which is really good.

<p align="center"><img width="700" alt="Captura de pantalla 2021-12-15 a las 21 50 25" src="https://user-images.githubusercontent.com/90793442/146263081-392f1022-61d1-4318-a5ea-dccee910fb8d.png"></p>

**Player Performance prediction:** The best model was _Model 4:_ Stack Best of - Linear Model, Decission Tree, Random Forest.  
With it, my predictions have the following socores:
- R2 - 0.70
- MSE - 0.023
- RMSE - 0.15 
This means that for a whole season, my predictions are wrong in just about 1.9 points per player - which is really good.

<p align="center"><img width="500" alt="Captura de pantalla 2021-12-15 a las 21 52 12" src="https://user-images.githubusercontent.com/90793442/146263253-0f5ccb77-53ef-4106-88d1-cdfcfa497ca8.png"></p>

