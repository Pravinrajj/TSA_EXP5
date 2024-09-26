### NAME: PRAVINRAJJ G.K
### REG.NO: 212222240080

# Ex.No: 05  IMPLEMENTATION OF TIME SERIES ANALYSIS AND DECOMPOSITION
### Date: 


### AIM:
To illustrate how to perform time series analysis and decomposition on the monthly average closing price of XAUUSD (Gold price in USD) from the provided dataset.


### ALGORITHM:
1. Import the required libraries such as pandas and matplotlib.
2. Load the dataset using pandas and parse the date column.
3. Resample the data to a monthly frequency and fill any missing values using interpolation.
4. Perform the seasonal decomposition process on the resampled data using a defined period.
5. Plot the original data and the decomposition results (trend, seasonality, residuals).
6. Display the results with properly formatted axes and labels.


### PROGRAM:
```py
import pandas as pd
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose
import matplotlib.dates as mdates

# Load the dataset
data = pd.read_csv('XAUUSD_2010-2023.csv')

# Parse the 'time' column as dates and set it as the index
data['Date'] = pd.to_datetime(data['time'], format='%d-%m-%Y %H:%M')
data.set_index('Date', inplace=True)

# Resample to monthly frequency and interpolate missing data
monthly_data = data['close'].resample('M').mean().interpolate()

# Plot the original monthly resampled data
plt.figure(figsize=(7, 4))
plt.plot(monthly_data, label='Monthly Average Close (Interpolated)')
plt.title('XAUUSD Time Series Data (Monthly Average)', fontsize=10)
plt.xlabel('Date', fontsize=14)
plt.ylabel('Price (USD)', fontsize=14)
plt.grid(True)
plt.legend()
plt.xticks(fontsize=10)
plt.yticks(fontsize=10)
plt.tight_layout()
plt.show()

# Perform seasonal decomposition
decomposition = seasonal_decompose(monthly_data.dropna(), model='multiplicative', period=3)

# Plot the decomposition results
fig = decomposition.plot()
fig.set_size_inches(7, 4)

# Format the x-axis labels for each plot
for ax in fig.axes:
    ax.xaxis.set_major_locator(mdates.YearLocator())
    ax.xaxis.set_major_formatter(mdates.DateFormatter('%Y'))
    ax.tick_params(axis='x', rotation=45, labelsize=10)
    ax.tick_params(axis='y', labelsize=10)

plt.tight_layout()
plt.show()

```


### OUTPUT:
FIRST FIVE ROWS:
![image](https://github.com/user-attachments/assets/c0fe9108-a199-408e-bbc0-61ed96a172bd)

PLOTTING THE DATA:
![image](https://github.com/user-attachments/assets/53ff7917-52b9-4627-a9f2-a4e820552b09)

![image](https://github.com/user-attachments/assets/6049bb25-5ee5-47b9-bcb3-85e954a7a3c5)



### RESULT:
Thus we have created the python code for the time series analysis and decomposition.
