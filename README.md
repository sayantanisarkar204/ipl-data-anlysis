# ipl-data-anlysis
performed exploratory data analysis on ipl match data.Analyzed match trends ,team performance , player stats, and toss-winning impact using pandas and matplotlib
IPL_Analysis_Project/
│
├── matches.csv
├── deliveries.csv
└── ipl_analysis.ipynb (Jupyter notebook)
# Step 1: Import libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Step 2: Load the data
matches = pd.read_csv('matches.csv')
deliveries = pd.read_csv('deliveries.csv')

# Step 3: Basic exploration
print(matches.shape)
print(matches.columns)
matches.head()

# Step 4: Number of matches per season
matches_per_season = matches['season'].value_counts().sort_index()
matches_per_season.plot(kind='bar', color='skyblue')
plt.title("Matches per Season")
plt.xlabel("Season")
plt.ylabel("Number of Matches")
plt.show()

# Step 5: Most successful teams
team_wins = matches['winner'].value_counts()
team_wins.plot(kind='bar', color='orange')
plt.title("Most Winning Teams")
plt.xlabel("Team")
plt.ylabel("Wins")
plt.xticks(rotation=90)
plt.show()

# Step 6: Toss vs Match Winner
toss_match_win = matches[matches['toss_winner'] == matches['winner']]
percentage = len(toss_match_win) / len(matches) * 100
print(f"Percentage of matches where toss winner also won the match: {percentage:.2f}%")

# Step 7: Top Batsmen
top_batsmen = deliveries.groupby('batsman')['batsman_runs'].sum().sort_values(ascending=False).head(10)
top_batsmen.plot(kind='bar', color='green')
plt.title("Top 10 Batsmen")
plt.ylabel("Runs")
plt.show()

# Step 8: Top Bowlers (by wickets)
wickets = deliveries[deliveries['dismissal_kind'].notnull()]
top_bowlers = wickets['bowler'].value_counts().head(10)
top_bowlers.plot(kind='bar', color='red')
plt.title("Top 10 Bowlers (by dismissals)")
plt.ylabel("Wickets")
plt.show()

# Step 9: Most Man of the Match awards
mom = matches['player_of_match'].value_counts().head(10)
mom.plot(kind='bar', color='purple')
plt.title("Top 10 MOM Award Winners")
plt.ylabel("Awards")
plt.show()
