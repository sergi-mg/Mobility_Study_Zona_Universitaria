# Mobility Study in Zona Universitària: Stops and Walking Distances
This repository contains the data recorded during a mobility study excuted by students of the Physics of Economic and Social Systems course from the Master in Physics of Complex Systems and Biophysics at UB. The experiment was performed the 1st of June from 15:15 h to 16:00 h.

## Data structure
Data recorded during each group walk can be found in the csv's named Group_x where x is the number associated with each group (form 1 to 6). The csv contains the following information, for groups from 1 to 4.
| Column Name | Description | Unit / Format | Data Type |
|-------------|-------------|---------------|-----------|
| `latitude` | Latitude coordinate of the GPS track point. | Decimal degrees| `float` |
| `longitude` | Longitude coordinate of the GPS track point. | Decimal degrees| `float` |
| `elevation` | Altitude of the GPS track point above mean sea level. | Meters (m) | `float` |
| `time` | Date and time at which the GPS point was recorded. | UTC timestamp: `YYYY-MM-DD HH:MM:SS+UTC` | `datetime` |

In the case of groups 4 and 5, the previously defined columns are called `X`, `Y` , `ele` and `time`. There are also additional columns containing no information which were eliminated (see Data Cleaning section).

## Data Cleaning
The data was cleaned using the following Python code.
```python
df_1 = pd.read_csv('../data/group_1.csv')
df_2 = pd.read_csv('../data/group_2.csv')
df_3 = pd.read_csv('../data/group_3.csv')
df_4 = pd.read_csv('../data/group_4.csv')
df_5 = pd.read_csv('../data/group_5.csv')
df_6 = pd.read_csv('../data/group_6.csv')

# Cleaning
df_1 = df_1.drop([0])
df_1 = df_1.reset_index(drop=True)

# -----------------------------------------
df_2 = df_2.drop([0])
df_2 = df_2.reset_index(drop=True)

# -----------------------------------------
df_4 = df_4.drop([df_4.index[-1], df_4.index[-2]])
df_4 = df_4.reset_index(drop=True)

# -----------------------------------------
df_5 = df_5[["X", "Y", "ele", "time"]]
df_5 = df_5.rename(columns={
    "X": "longitude",
    "Y": "latitude",
    "ele": "elevation",
    "time": "time"
})
df_5 = df_5.drop([0, 1, 2, 3, 4, 5, 6])
df_5 = df_5.reset_index(drop=True)

# -----------------------------------------
df_6 = df_6[["X", "Y", "ele", "time"]]
df_6 = df_6.rename(columns={
    "X": "longitude",
    "Y": "latitude",
    "ele": "elevation",
    "time": "time"
})
```
