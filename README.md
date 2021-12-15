# Becoming a NHL analyst from scracht

## Creating a model able to predict wheter or not a team will make the PlayOffs this season (21-22)
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
For further details on all features, please refer to [notebook 1]

<img width="1129" alt="Captura de pantalla 2021-12-15 a las 12 44 36" src="https://user-images.githubusercontent.com/90793442/146180676-1c857c53-032e-4af6-9d88-dcd40ecb068e.png">

For the players perfonces prediction, the dataframe obtained consists on:
- 12055 samples
- 29 columns: name, position, country, birthday, id, height, weight,
       goals_1, assists_1, pim_1, games_1, hits_1, hots_1,
       time_1, plus_minus_1, goals_2, assists_2, pim_2, games_2,
       hits_2, shots_2, time_2, plus_minus_2, season_1, season_2,
       season_3, ppg_3, team_1 and team_2
- Target value: ppg_3
For further details on all features, please refer to [notebook 2]

<img width="1112" alt="Captura de pantalla 2021-12-15 a las 12 41 19" src="https://user-images.githubusercontent.com/90793442/146180277-78e07170-a896-4e35-b674-79ca2da332a9.png">

<a name="PT"></a>
## Process & Tools
**Process**

The process includes:
- Learning rules of the NHL - how many games per season, maximum points that can be gained per game, etc
- Understanding hockey stats
- Finding out wich are the best teams in the league
- Finding out who are the superstars players in the league
- Starting with __Playoff Precictions__
  - Scrapping teams stats from past seasons
  - Converting total stats into stats per game - scaling data
  - Exploratory Data Analysis - EDA:
    - Dealing with nulls
    - Finding Correlations - dropping power_play_opportunities after trying leaving it (high correlated)
    - Dropping irrelevant features for modeling - season, team_id, team_name, gamesplayed_x, gamesplayed_y, rank
<p align="center"><img width="513" alt="Captura de pantalla 2021-12-15 a las 12 45 32" src="https://user-images.githubusercontent.com/90793442/146180823-d32f6001-626d-4a38-9449-49c9bc4642c9.png"></p>

- Preparing data for modeling:
    - Isolate target value
    - Trying different scalers - in the end I opted not to use any as my data was already scaled by number of games
 - Tried different Machine learning models for regression as follows:
    - _Model 1:_ Linear Model
    - _Model 2:_ Decission Tree
    - _Model 3:_ Random Forest
    - _Model 4:_ Stack Best of - Linear Model, Decission Tree, Random Forest
    - _Model 5:_ Stack Best of - Linear Model, Random Forest
 - Comparing models
<p align="center"><img width="565" alt="Captura de pantalla 2021-12-15 a las 13 02 18" src="https://user-images.githubusercontent.com/90793442/146183064-382f8455-23ba-46cc-9778-ec4660863d0c.png"></p>

