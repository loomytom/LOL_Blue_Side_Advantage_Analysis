
# League of Legends Red vs Blue Side Analysis

Welcome!

This project is a project conducted at UCSD with multiple sets of analyses including hypothesis testing, missingness testing, and modeling. The main objective of this project is to determine whether or not there is a significant difference between win rates of teams playing from Blue Side and playing from Red Side.

## Project Objectives

- Examine the differences between red and blue side performance.
- Use t-tests and statistical methods for analysis.
- Provide insights into game balance.
[View the Repository on GitHub](https://github.com/loomytom/LOL_Blue_Side_Advantage_Analysis)

## Introduction 

League of Legends (LOL) is a globally popular multiplayer online battle arena (MOBA) game developed by Riot Games. LOL has established itself as one of the most prominent titles in competitive gaming with millions of players worldwide. The data for this project is sourced from Oracle's Elixir, a professional-grade data platform that compiles gameplay statistics from professional matches. This dataset pulls match records from professional play, offering a rich array of features such as kills, deaths, gold differences at 10 minutes, barons, dragons, and more.

One of the most intriguing dynamics in League of Legends is the perceived advantage or disadvantage tied to which side of the map a team starts on — Red Side or Blue Side. This perceived asymmetry has sparked debates among both casual and professional players  as they believe there may be a meaningful difference in win rates between the two sides. Riot Games has also acknowledged this potential issue, making it a relevant area of study.

The focus of this analysis is to investigate whether these differences in win rates are statistically significant. By using professional match data, this project aims to find whether Red Side or Blue Side holds an advantage, and if so, what metrics might drive this disparity. For instance, does Blue Side tend to secure more barons? Is Red Side more likely to take the first dragon? To further explore these patterns, a predictive model was developed to determine a team’s side based on key gameplay metrics. This model provides valuable insights into potential biases associated with playing on each side and can inform both in-game decision-making and future balancing efforts by Riot Games. 

# Data 

The data that was used for this analysis was pulled from the professional matches in 2022. In the data there are 150180 rows and 161 columns. Out of these columns, the ones that are important to this analysis are listed below.

- <span style="background-color:#f0f8ff; border-radius:8px; padding:4px 8px; font-weight:bold; display:inline-block; box-shadow:0px 2px 4px rgba(0, 0, 0, 0.1);">side</span>: This column represents what the team affiliation for each game, and it is either Red or Blue. 
- <span style="background-color:#f0f8ff; border-radius:8px; padding:4px 8px; font-weight:bold; display:inline-block; box-shadow:0px 2px 4px rgba(0, 0, 0, 0.1);">result</span>: This column is a binary indication of the outcome of the match, 1 for a win and 0 for a loss.
- <span style="background-color:#f0f8ff; border-radius:8px; padding:4px 8px; font-weight:bold; display:inline-block; box-shadow:0px 2px 4px rgba(0, 0, 0, 0.1);">firstdragon</span>: This column represents whether or not a team was the first team to secure a dragon. 1 means they got the first dragon and 0 means they did not.
- <span style="background-color:#f0f8ff; border-radius:8px; padding:4px 8px; font-weight:bold; display:inline-block; box-shadow:0px 2px 4px rgba(0, 0, 0, 0.1);">heralds</span>: The 'heralds' column denotes how many rift heralds, another epic monster, each team takes.
- <span style="background-color:#f0f8ff; border-radius:8px; padding:4px 8px; font-weight:bold; display:inline-block; box-shadow:0px 2px 4px rgba(0, 0, 0, 0.1);">barons</span>: The ‘barons’ column records how many barons, a third type of epic monster, each team takes.
- <span style="background-color:#f0f8ff; border-radius:8px; padding:4px 8px; font-weight:bold; display:inline-block; box-shadow:0px 2px 4px rgba(0, 0, 0, 0.1);">golddiffat10</span>: This column represents how much gold a team is up by 10 minutes into the game. A positive value tells us that they are leading the other team by a certain amount, and a negative value means they are behind by that amount.
- <span style="background-color:#f0f8ff; border-radius:8px; padding:4px 8px; font-weight:bold; display:inline-block; box-shadow:0px 2px 4px rgba(0, 0, 0, 0.1);">golddiffat15</span>: Similar to ‘golddiffat10’, this column specifically denotes the gold differential of a team at 15 minutes.
- <span style="background-color:#f0f8ff; border-radius:8px; padding:4px 8px; font-weight:bold; display:inline-block; box-shadow:0px 2px 4px rgba(0, 0, 0, 0.1);">golddiffat20</span>: Similar to ‘golddiffat15’, this column specifically denotes the gold differential of a team at 20 minutes.
- <span style="background-color:#f0f8ff; border-radius:8px; padding:4px 8px; font-weight:bold; display:inline-block; box-shadow:0px 2px 4px rgba(0, 0, 0, 0.1);">golddiffat25</span>: Similar to ‘golddiffat20’, this column specifically denotes the gold differential of a team at 25 minutes. A null value in the golddiffat25 suggests that the game ended before 25 minutes.

# Data Cleaning 

### 1. Filtering for Complete Data
The first step towards cleaning the data was to only grab data that is considered 'complete', which was under the column 'datacompleteness' in the original dataframe. The column was divided into 'complete' and 'partial' so the data was queried to only use rows that had complete data. 

### 2. Aggregating Team-Level Data
The next step was to query out each player's performance and only grab information regarding the team for each game. This was done by looking at the 'position' column in the dataframe and setting it to only grab position = 'team'.

### 3. Selecting Relevant Columns
The last step towards cleaning the data was to query only the relevant columns that were listed above. This is what the cleaned Dataframe looks like:

| Side  | Result | First Dragon | Heralds | Dragons | Barons | GoldDiff10 | GoldDiff15 | GoldDiff20 | GoldDiff25 |
|-------|--------|--------------|---------|---------|--------|------------|------------|------------|------------|
| Blue  | 0      | 0            | 2       | 1       | 0      | 1523       | 107        | -944       | 88         |
| Red   | 1      | 1            | 0       | 3       | 0      | -1523      | -107       | 944        | -88        |
| Blue  | 0      | 0            | 1       | 1       | 0      | -1619      | -1763      | -5140      | -7280      |
| Red   | 1      | 1            | 1       | 4       | 2      | 1619       | 1763       | 5140       | 7280       |
| Blue  | 1      | 1            | 1       | 1       | 4      | -103       | 1191       | 1744       | 4145       |

# Univariate Analysis 
The first analysis that was performed was looking at overall wins on blue side vs red side 
<iframe
  src="assets/win_rate_sides.html"
  width="700"
  height="500"
  frameborder="0"
></iframe>

This pie chart shows that there is a 4.6 point difference between win rates of teams on blue side to red side. From the graph, it shows that teams playing on blue side win more than teams playing on red side. 

# Bivariate Analysis 
The second analysis that was done looked at how many rift heralds each team took when they won and when they lost
<iframe
  src="assets/heralds_sides.html"
  width="700"
  height="500"
  frameborder="0"
></iframe>

This bar chart shows that blue side teams take more rift heralds when they win, but they also take more rift heralds when they lose compared to red side. No matter win or lose, on average blue side will take more rift heralds than red side.

# Interesting Aggregates
These were some of the interesting aggregates that were found when grouping by result, either win or loss, and summing the columns. 

|   result |   firstdragon |   heralds |   dragons |   barons |
|---------:|--------------:|----------:|----------:|---------:|
|        0 |          4491 |      8146 |     15394 |     2372 |
|        1 |          6129 |     12817 |     32334 |    11971 |

From this above we can see that winning teams take more dragons, heralds, and barons, but also more likely to take the first dragon compared to teams that lost. This makes sense because taking objectives helps teams get ahead in the game, and contributing to them being stronger than the enemy team.

# NMAR Analysis 
In looking at the columns of interest, the column **firstdragon**, could be NMAR because the value of **firstdragon** depends on itself. For exmaple, if **firstdragon** is missing, it is possible that the team did not take the first dragon due to their strategy or simply did not try and contest the dragon. In this case the missingness of **firstdragon** is dependent on the value of the column, which would make it NMAR.

# Missingness Dependency 
To test for missingnes, the column **golddiffat25** was tested to see if its missingness was dependent on any columns. The significance level that was chosen for these tests was a = 0.05 and the test statistic was Kolmogorov–Smirnov.

The first column tested with **golddiffat25** was the column **baron**.

**Null Hypothesis**: The distribution of **barons** is the same when **golddiffat25** is missing then when it is not missing.

**Alternative Hypothesis**: The distribution of **barons** is different when **golddiffat25** is missing than when it is not missing.

Below is a graph showing what the distribution of values look like:
<iframe
  src="assets/baron_missing.html"
  width="700"
  height="500"
  frameborder="0"
></iframe>

From the graph, it can be seen that observed difference is much larger than any of the tests. The p-value was 0.0, lower than the 0.05 threshold, showing that it is statistically significant, or in other words, the missingness of **golddiffat5** is related to the **barons** column. This makes sense because if there are a lot of baron's taken, the game likely ran longer than 25 minutes because the first baron is spawned in at 20 minutes. 

The second column tested with **golddiffat25** was the column **firstdragon**.

**Null Hypothesis**: The distribution of **firstdragon** is the same when **golddiffat25** is missing then when it is not missing.

**Alternative Hypothesis**: The distribution of **firstdragons** is different when **golddiffat25** is missing than when it is not missing.

Below is a graph showing what the distribution of values look like:
<iframe
  src="assets/first_dragon_missing.html"
  width="700"
  height="500"
  frameborder="0"
></iframe>

From the graph, it can be seen that observed difference is smaller than most of the permuted tests. The p-value was 0.928, above the 0.05 threshold, showing that it is not statistically significant, or in other words, the missingness of **golddiffat5** is not related to the **firstdragon** column. 

# Hypothesis Testing

For the hypothesis test, the goal was to find out if there is a significant difference between win rates on blue side and win rates on red side. This is important to understanding possible biases in League of Legends and being able to address them to ensure fairness in gameplay. 

**Null Hypothesis**: The win rate of teams on Blue side is the same as the win rate of teams on Red side.

**Alternative Hypothesis**: The win rate of teams on Blue side is greater than the win rate of teams on Red side.

**Test Statistic**: Difference in mean

**Significance Level**: 0.05


