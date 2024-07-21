import pandas as pd

# Define column names
column_names = [
    "age", "sex", "cp", "trestbps", "chol", "fbs", "restecg",
    "thalach", "exang", "oldpeak", "slope", "ca", "thal", "num"
]

# Load dataset
data = pd.read_csv(
    "https://archive.ics.uci.edu/ml/machine-learning-databases/heart-disease/processed.cleveland.data",
    names=column_names
)

# Data exploration
print(data.head())
print(data.info())

# Replace '?' with NaN and convert columns to appropriate types
data = data.replace('?', pd.NA)

# Convert columns to numeric, forcing errors to NaN
for column in data.columns:
    data[column] = pd.to_numeric(data[column], errors='coerce')

# Drop rows with any NaN values
data = data.dropna()

# Ensure all columns are in the correct type (integer for categorical, float for continuous)
categorical_columns = ["sex", "cp", "fbs", "restecg", "exang", "slope", "ca", "thal", "num"]
for column in categorical_columns:
    data[column] = data[column].astype(int)

# Check the cleaned data
print(data.head())
print(data.info())
