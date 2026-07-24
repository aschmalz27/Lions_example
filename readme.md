# Final Project


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
