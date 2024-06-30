# Election Results Analysis 2024

This project analyzes the results of the 2024 elections using a dataset of election results. The analysis includes identifying the party with the highest and lowest margins of victory, visualizing the number of seats won by each party, and examining the top margins achieved by different parties.
![image](https://github.com/deeptimurugesan21/LokSabha_election-/assets/131357285/505ffdbd-3006-4788-8b7c-889d136946ae)

## Table of Contents
- [Introduction](#introduction)
- [Dataset](#dataset)
- [Installation](#installation)
- [Usage](#usage)
- [Analysis Overview](#analysis-overview)
- [Visualizations](#visualizations)
- [Contributing](#contributing)
- [License](#license)

## Introduction

The goal of this project is to provide a comprehensive analysis of the 2024 election results. This includes:
- Identifying which party had the highest and lowest margin of victory.
- Plotting the number of seats won by each party.
- Highlighting the top margins achieved by different parties.
- Visualizing the election results on a map.

## Dataset

The dataset used for this analysis is `election_results_2024.csv`, which contains information on the election results, including the leading party and the margin of victory for each constituency.

## Installation

To run this project, you will need to install the required Python libraries listed in `requirements.txt`:

```sh
pip install -r requirements.txt
```

## Usage
1. Clone this repository:

```sh
git clone https://github.com/deeptimurugesan21/LokSabha_election-
```

2. Navigate to the project directory:


3. Ensure you have the dataset election_results_2024.csv in the Dataset directory.

4. Run the Jupyter notebook:

```sh
jupyter notebook Election2024_result_analaysis.ipynb
```
## Analysis Overview
### Import Libraries

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np
import plotly.express as px
import plotly.offline as py
from geopy.geocoders import Nominatim
import warnings
```

### Load Data

```python
data = pd.read_csv('Dataset/election_results_2024.csv')
data.head(10)
```

### Party with Highest and Lowest Margin of Victory

```python
party_votes = data.groupby('Leading Party')['Margin'].sum().sort_values(ascending=False)
data['Margin'] = pd.to_numeric(data['Margin'], errors='coerce')

highest_margin = data.loc[data['Margin'].idxmax()]
lowest_margin = data.loc[data['Margin'].idxmin()]
```
![image](https://github.com/deeptimurugesan21/LokSabha_election-/assets/131357285/218cf977-8ddf-4d79-b5bb-2c14bfff1efd)

### Plot Number of Seats Won by Each Party

```python
leading_party_highest_votes = party_votes.idxmax()
leading_party_lowest_votes = party_votes.idxmin()
seats_won = data['Leading Party'].value_counts()

plt.figure(figsize=(20, 8))
sns.barplot(x=seats_won.index, y=seats_won.values, palette='viridis')
plt.title('Number of Seats Won by Each Party')
plt.xlabel('Party')
plt.ylabel('Seats Won')
plt.xticks(rotation=90)
plt.show()
```
![image](https://github.com/deeptimurugesan21/LokSabha_election-/assets/131357285/667f0cc5-7567-4b02-81cd-30b089de3783)

### Top Margin Achieved by Party
The analysis further explores the top margins achieved by different parties.
![image](https://github.com/deeptimurugesan21/LokSabha_election-/assets/131357285/bfc0e197-8dc1-4797-b620-3d1cb703546c)

## Visualizations
### Election Results Map
To visualize the election results on a map, you can use the following code snippet:
```python
# Assuming your data has columns 'Constituency', 'Latitude', 'Longitude', 'Leading Party'
fig = px.scatter_geo(data,
                     lat='Latitude',
                     lon='Longitude',
                     color='Leading Party',
                     hover_name='Constituency',
                     size='Margin',
                     projection='natural earth')

fig.update_layout(title='Election Results 2024')
fig.show()
```
![State wise party distribution](https://github.com/deeptimurugesan21/LokSabha_election-/assets/131357285/0e5877f2-251c-4af9-b59e-8e0430cb3a81)

### Number of Seats Won by Each Party
Here is a sample visualization of the number of seats won by each party:
![image](https://github.com/deeptimurugesan21/LokSabha_election-/assets/131357285/9d8cb79b-f35a-4c49-ae78-dbdd076cc83e)

## License
This project is licensed under the MIT License - see the LICENSE file for details.
