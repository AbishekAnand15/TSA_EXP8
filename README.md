## DEVELOPED BY: Abishek Xavier A
## REGISTER NO: 212222230004
## DATE:

# Ex.No: 08 MOVING AVERAGE MODEL AND EXPONENTIAL SMOOTHING
 
## AIM:
To implement Moving Average Model and Exponential smoothing Using Python.
## ALGORITHM:
1. Import necessary libraries
2. Read the House Sales time series data from a CSV file,Display the shape and the first 20 rows of
the dataset
3. Set the figure size for plots
4. Suppress warnings
5. Plot the first 50 values of the 'Value' column
6. Perform rolling average transformation with a window size of 5
7. Display the first 10 values of the rolling mean
8. Perform rolling average transformation with a window size of 10
9. Create a new figure for plotting,Plot the original data and fitted value
10. Show the plot
11. Also perform exponential smoothing and plot the graph
## PROGRAM:
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import warnings
from statsmodels.tsa.holtwinters import ExponentialSmoothing

warnings.filterwarnings('ignore')
data = pd.read_csv("/content/Super_Store_data.csv", encoding='ISO-8859-1')
print("Shape of the dataset:", data.shape)
print("First 20 rows of the dataset:")
print(data.head(20))

# Convert 'Date' column to datetime format and set as index
# Changed format to '%m/%d/%Y' to match the actual date format in the 'Order Date' column
data['Order Date'] = pd.to_datetime(data['Order Date'], format='%m/%d/%Y')  
data.set_index('Order Date', inplace=True)

# Resample the data to get monthly sales totals
monthly_sales = data['Sales'].resample('M').sum()

# Plot original sales data
plt.figure(figsize=(12, 6))
plt.plot(monthly_sales, label='Total Sales', color='blue')
plt.title(f'Total Sales Over Time for Furniture Store')
plt.xlabel('Year')
plt.ylabel('Sales (in dollars)')
plt.legend()
plt.grid()
plt.show()

# Moving average calculation (window=3 months)
rolling_mean_3 = monthly_sales.rolling(window=3).mean()

# Plot moving average along with original data
plt.figure(figsize=(12, 6))
plt.plot(monthly_sales, label='Total Sales', color='blue')
plt.plot(rolling_mean_3, label='Moving Average (window=3)', color='orange')
plt.title(f'Moving Average of Sales for Furniture Store')
plt.xlabel('Year')
plt.ylabel('Sales (in dollars)')
plt.legend()
plt.grid()
plt.show()

# Apply Exponential Smoothing
model = ExponentialSmoothing(monthly_sales, trend='add', seasonal=None)
model_fit = model.fit()

# Forecast future steps (next 6 months for example)
future_steps = 6
predictions = model_fit.predict(start=len(monthly_sales), end=len(monthly_sales) + future_steps - 1)

# Create future dates for forecasting
future_dates = pd.date_range(start=monthly_sales.index[-1] + pd.Timedelta(days=30), periods=future_steps, freq='M')

# Plot forecast
plt.figure(figsize=(12, 6))
plt.plot(monthly_sales, label='Total Sales', color='blue')
plt.plot(future_dates, predictions, label='Exponential Smoothing Forecast', color='orange')
plt.title(f'Exponential Smoothing Predictions for Furniture Store Sales')
plt.xlabel('Year')
plt.ylabel('Sales (in dollars)')
plt.legend()
plt.xticks(rotation=45)
plt.grid(True)
plt.tight_layout()
plt.show()
```

## OUTPUT:
### GIVEN DATA
![Screenshot 2024-10-18 093316](https://github.com/user-attachments/assets/80fc89e7-e465-46ca-8aca-1ef37bc05957)

### Moving Average
![Screenshot 2024-10-18 093638](https://github.com/user-attachments/assets/faa09521-b606-4903-8444-40d8e0a4dfe2)

### Plot Transform Dataset
![image](https://github.com/user-attachments/assets/7163a790-83ee-4615-a324-22da4237d506)

### Exponential Smoothing
![image](https://github.com/user-attachments/assets/d54b7fc2-fd76-4823-a795-2d2f51ced3c3)


## RESULT:
Thus, the program to implement the Moving Average Model and Exponential smoothing using python is executed successfully.
