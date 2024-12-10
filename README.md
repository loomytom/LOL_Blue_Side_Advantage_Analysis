
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
The last step towarsd cleaning the data was to query only the relevant columns that were listed above. This is what the cleaned Dataframe looks like:
it will work



