# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION
# Reg no:212223240071
# Name :KEERTHIKA M P
# Date:26.08.2025
# AIM:
To Implement Linear and Polynomial Trend Estiamtion Using Python.

# ALGORITHM:
Import necessary libraries (NumPy, Matplotlib)

Load the dataset

Calculate the linear trend values using least square method

Calculate the polynomial trend values using least square method

End the program
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

data = pd.read_csv('/mnt/data/laptop_price.csv', encoding='latin1')

years = data['Inches'].tolist()
ram_values = data['Price_euros'].tolist()

X = [i - years[len(years) // 2] for i in years]
x2 = [i ** 2 for i in X]
xy = [i * j for i, j in zip(X, ram_values)]
n = len(years)

b = (n * sum(xy) - sum(ram_values) * sum(X)) / (n * sum(x2) - (sum(X) ** 2))
a = (sum(ram_values) - b * sum(X)) / n
linear_trend = [a + b * X[i] for i in range(n)]

x3 = [i ** 3 for i in X]
x4 = [i ** 4 for i in X]
x2y = [i * j for i, j in zip(x2, ram_values)]
coeff = [[len(X), sum(X), sum(x2)],
         [sum(X), sum(x2), sum(x3)],
         [sum(x2), sum(x3), sum(x4)]]
Y = [sum(ram_values), sum(xy), sum(x2y)]
A = np.array(coeff)
B = np.array(Y)
solution = np.linalg.solve(A, B)
a_poly, b_poly, c_poly = solution
poly_trend = [a_poly + b_poly * X[i] + c_poly * (X[i] ** 2) for i in range(n)]

print(f"Linear Trend: y={a:.2f} + {b:.2f}x")
print(f"Polynomial Trend: y={a_poly:.2f} + {b_poly:.2f}x + {c_poly:.2f}x²")

data['Linear Trend'] = linear_trend
data['Polynomial Trend'] = poly_trend
data['Index'] = years

data.set_index('Index', inplace=True)

data['Price_euros'].plot(kind='line', color='blue', marker='o', label="Price")
data['Linear Trend'].plot(kind='line', color='black', linestyle='--', label="Linear Trend")
plt.title("Linear Trend Estimation (Price vs Inches)")
plt.legend()
plt.show()

data['Price_euros'].plot(kind='line', color='blue', marker='o', label="Price")
data['Polynomial Trend'].plot(kind='line', color='red', marker='o', label="Polynomial Trend")
plt.title("Polynomial Trend Estimation (Price vs Inches)")
plt.legend()
plt.show()
```

### OUTPUT
A - LINEAR TREND ESTIMATION
<img width="794" height="557" alt="Screenshot 2025-08-26 091949" src="https://github.com/user-attachments/assets/f911812b-c3b4-497a-8d4d-2ba028280021" />

B- POLYNOMIAL TREND ESTIMATION
<img width="756" height="519" alt="Screenshot 2025-08-26 092007" src="https://github.com/user-attachments/assets/a78f5c06-99a4-4a17-b680-70de8b43f62d" />



### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
