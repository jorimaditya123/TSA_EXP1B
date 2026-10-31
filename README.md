# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 31.10.2026

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:

```python

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Step 1: Read the dataset
data = pd.read_csv("weatherHistory.csv")

# Step 2: Preprocessing
data['Formatted Date'] = pd.to_datetime(
    data['Formatted Date'], utc=True
)
data.set_index('Formatted Date', inplace=True)

# Resample data to monthly average
monthly_data = data['Temperature (C)'].resample('ME').mean()

# Original Data
plt.figure(figsize=(12, 5))
plt.plot(monthly_data)
plt.title('Original Temperature Data')
plt.xlabel('Date')
plt.ylabel('Temperature (C)')
plt.show()

# Step 3: Regular Differencing
regular_diff = monthly_data.diff()

plt.figure(figsize=(12, 5))
plt.plot(regular_diff)
plt.title('Regular Differencing')
plt.xlabel('Date')
plt.ylabel('Temperature Difference')
plt.show()

# Step 4: Seasonal Adjustment
seasonal_diff = monthly_data.diff(12)

plt.figure(figsize=(12, 5))
plt.plot(seasonal_diff)
plt.title('Seasonal Differencing')
plt.xlabel('Date')
plt.ylabel('Seasonal Difference')
plt.show()

# Step 5: Log Transformation
# Shift values to make all values positive
shifted_data = monthly_data - monthly_data.min() + 1

log_data = np.log(shifted_data)

plt.figure(figsize=(12, 5))
plt.plot(log_data)
plt.title('Log Transformation')
plt.xlabel('Date')
plt.ylabel('Log Temperature')
plt.show()

# Step 6: Display Results
print("Original Mean:", monthly_data.mean())
print("Regular Differencing Mean:", regular_diff.mean())
print("Seasonal Differencing Mean:", seasonal_diff.mean())
print("Log Transformation Mean:", log_data.mean())

# Combined Transformation
combined = log_data.diff().diff(12)

plt.figure(figsize=(12, 5))
plt.plot(combined)
plt.title('Combined Transformation')
plt.xlabel('Date')
plt.ylabel('Transformed Temperature')
plt.show()

print("\nCombined Transformation:")
print(combined.dropna().head(10))

```

### OUTPUT:

<img width="1636" height="709" alt="image" src="https://github.com/user-attachments/assets/05d3d6a7-4474-4acf-b811-6bc1c4417e0b" />

REGULAR DIFFERENCING:
<img width="1711" height="724" alt="image" src="https://github.com/user-attachments/assets/319c92bd-80d8-4fcd-aa9e-04b06734b11d" />


SEASONAL ADJUSTMENT:
<img width="1647" height="709" alt="image" src="https://github.com/user-attachments/assets/fdf36337-0de1-49cb-b149-abe854b2d1e9" />


LOG TRANSFORMATION:
<img width="1642" height="801" alt="image" src="https://github.com/user-attachments/assets/a5e08842-95ee-46f1-a69d-4e703fc19bb2" />


<img width="1678" height="1062" alt="image" src="https://github.com/user-attachments/assets/11fa2552-54ab-4028-9bf2-995f0a3bb821" />

### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
