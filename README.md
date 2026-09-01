# Ex.No: 05  IMPLEMENTATION OF TIME SERIES ANALYSIS AND DECOMPOSITION

### AIM:
To Illustrates how to perform time series analysis and decomposition on the monthly average temperature of a city/country and for airline passengers.
### DATASET: E-COMMERCE
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the decomposition process for the required data.
4. Plot the data according to need, either seasonal_decomposition or trend plot.
5. Display the overall results.

### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose
# Step 1: Load the dataset, Convert 'order_date' column to datetime format, Set it as index
data = pd.read_csv('/content/ecommerce_sales_analytics_5000.csv', parse_dates=['order_date'], index_col='order_date')

# Ensure the index is a DatetimeIndex, as resample() requires it
# Using 'mixed' format to handle different date formats observed in the data.
data.index = pd.to_datetime(data.index, format='mixed')

# Resample the data to monthly frequency and sum the revenue
# Seasonal decomposition works best with regular time series, so we aggregate by month
monthly_revenue = data['revenue'].resample('MS').sum().to_frame()

# Step 2: Perform seasonal decomposition using the 'revenue' column
decomposition = seasonal_decompose(monthly_revenue['revenue'], model='additive', period=12)

# Step 3: Plot the decomposition
plt.figure(figsize=(12, 10))  # Adjust the figure size

# Original Data
plt.subplot(411)
plt.plot(monthly_revenue['revenue'], label='Monthly Revenue')
plt.legend(loc='upper left')
plt.title('Monthly Revenue')

# Trend Plot
plt.subplot(412)
plt.plot(decomposition.trend, label='Trend', color='orange')
plt.legend(loc='upper left')
plt.title('Trend Component')

# Seasonal Plot
plt.subplot(413)
plt.plot(decomposition.seasonal, label='Seasonal', color='green')
plt.legend(loc='upper left')
plt.title('Seasonal Component')

# Residual Plot
plt.subplot(414)
plt.plot(decomposition.resid, label='Residual', color='red')
plt.legend(loc='upper left')
plt.title('Residual Component')

plt.tight_layout()
plt.show()
```
### OUTPUT:
<img width="986" height="413" alt="image" src="https://github.com/user-attachments/assets/a571f08f-c015-42a5-ba94-0178f19915d3" />
<img width="982" height="405" alt="image" src="https://github.com/user-attachments/assets/1435bb68-7eae-4476-917e-d30ba2022b9a" />



### RESULT:
Thus we have created the python code for the time series analysis and decomposition.
