# 📊 Smart Energy Usage Dashboard

This project visualizes household energy consumption data using time-series analysis and Tableau dashboards. It highlights trends, peak usage periods, and overall energy efficiency through interactive charts.

## 🚀 Overview

The dashboard was built using:

- Python (for data preprocessing)
- Tableau Public (for interactive data visualization)
- Dataset from UCI Machine Learning Repository

## 📁 Dataset

- **Source**: [UCI Household Power Consumption](https://archive.ics.uci.edu/ml/datasets/individual+household+electric+power+consumption)
- **File**: `household_power_consumption.txt`
- **Size**: ~2 million rows (Feb 2007 - Nov 2010)

## 🧹 Data Preprocessing

Used Python to clean, resample, and export the dataset:

```python
import pandas as pd

df = pd.read_csv('household_power_consumption.txt', sep=';', low_memory=False, na_values=['?'])
df['DateTime'] = pd.to_datetime(df['Date'] + ' ' + df['Time'], dayfirst=True)
df = df[['DateTime', 'Global_active_power']]
df.dropna(inplace=True)

df.set_index('DateTime', inplace=True)
df_hourly = df.resample('H').mean().reset_index()
df_daily = df.resample('D').mean().reset_index()

df_hourly.to_csv('hourly_energy.csv', index=False)
df_daily.to_csv('daily_energy.csv', index=False)
```

## 📊 Visualizations in Tableau

**Included:**

- 📈 Daily Energy Line Chart (with Date Filter + Aggregation Toggle)
- 📅 Bar Chart: Avg Usage by Day of Week
- 🔁 7-Day Moving Average Overlay
- 🧮 KPI Tiles: Max, Min, Avg, Sum (in a single sheet)
- 🔥 Heatmap: Hour vs Day Usage Pattern
