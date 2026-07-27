# Final Project
# This project demonstrates core Python data analysis concepts using Detroit Lions offensive statistics. A dictionary is used to store player data, which is converted into pandas DataFrames. The program combines the DataFrames, analyzes player yards, calculates the average number of yards, identifies above-average performers, checks for missing values, and reports the number of unique players.

import pandas as pd

# Dictionary containing Detroit Lions offensive leaders

lions_stats = { “Passing”: { “Player”: “Jared Goff”, “Yards”: 4564,
“Touchdowns”: 34 }, “Rushing”: { “Player”: “Jahmyr Gibbs”, “Yards”:
1223, “Touchdowns”: 13 }, “Receiving”: { “Player”: “Amon-Ra St. Brown”,
“Yards”: 1401, “Touchdowns”: 11 } }

print(lions_stats.keys())

# Function that converts one category into a DataFrame

def stats_function(category): try: data = lions_stats\[category\]

        df = pd.DataFrame([data])
        df["Category"] = category

        return df

    except KeyError:
        print("Category not found.")
        return pd.DataFrame()

# Create a list of DataFrames

stats_list = \[\]

for category in lions_stats.keys(): print(f”Loading {category} stats”)
stats_list.append(stats_function(category))

# Combine into one DataFrame

all_stats = pd.concat(stats_list, ignore_index=True)

print(all_stats)

print(“:”) print(all_stats.shape)

print(“:”) print(all_stats.columns)

print(“Sample:”) print(all_stats.sample(2))

# Find player with the most yards

print(“by Yards:”) print(all_stats.sort_values(by=“Yards”,
ascending=False))

# Average yards

print(“Yards:”) print(all_stats\[“Yards”\].mean())

# Above average?

all_stats\[“Above Average”\] = all_stats\[“Yards”\] \>
all_stats\[“Yards”\].mean()

print(“Data:”) print(all_stats)

# Missing values

print(“Values:”) print(all_stats.isna().sum())

# Unique players

print(“Players:”) print(all_stats\[“Player”\].nunique())

lions = pd.read_csv(“detroit_lions_stats.csv”)

#a bar chart of player yards
all_stats.plot(
    kind="bar",
    x="Player",
    y="Yards",
    legend=False,
    title="Detroit Lions Offensive Leaders by Total Yards",
    figsize=(8,5)
)

plt.xlabel("Player")
plt.ylabel("Total Yards")
plt.xticks(rotation=0)
plt.tight_layout()
plt.show()

all_stats.plot(
    kind="bar",
    x="Player",
    y="Touchdowns",
    legend=False,
    title="Detroit Lions Offensive Leaders by Touchdowns",
    figsize=(8,5)
)

plt.xlabel("Player")
plt.ylabel("Touchdowns")
plt.xticks(rotation=0)
plt.tight_layout()
plt.show()

## Detroit Lions Offensive Leaders by Total Yards
5000 ┤
4500 ┤ █
4000 ┤ █
3500 ┤ █
3000 ┤ █
2500 ┤ █
2000 ┤ █
1500 ┤ █        █
1000 ┤ █        █        █
 500 ┤ █        █        █
   0 ┼────────────────────────────────────────
      Jared     Jahmyr    Amon-Ra
      Goff      Gibbs     St. Brown

## Detroit Lions Offensive Leaders by Total Yards

5000 ┤
4500 ┤ ███████████████████████████████████ Jared Goff
4000 ┤
3500 ┤
3000 ┤
2500 ┤
2000 ┤
1500 ┤                 ████████████ Amon-Ra St. Brown
1000 ┤        ██████████ Jahmyr Gibbs
 500 ┤
   0 ┼──────────────────────────────────────────────
        Jared Goff   Jahmyr Gibbs   Amon-Ra St. Brown
