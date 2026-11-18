# Exp No.2 : Exploratory Data Analysis (EDA)

## Aim
To perform Exploratory Data Analysis (EDA) on the heart disease dataset to understand the data distribution, relationships, and key patterns useful for business insights and model building.

## Dataset
The dataset used for this experiment is `heartdisease.csv`. It contains medical and demographic information such as age, sex, cholesterol levels (`totChol`), `BMI`, blood pressure, and target values (`TenYearCHD`) indicating heart disease presence.

## Algorithm
1. Import required Python libraries (`numpy`, `pandas`, `seaborn`, `matplotlib`).
2. Load the dataset into a Pandas DataFrame.
3. Display the dataset structure, shape, and descriptive statistics.
4. Check for missing values and duplicate rows.
5. Examine correlations among numeric features using a correlation matrix and heatmap.
6. Visualize univariate distributions using histograms, boxplots, and countplots.
7. Analyze bivariate and multivariate relationships using scatter plots and pairplots.

## Functions and Methods Used

| Category | Function / Method | Purpose / Description |
| :--- | :--- | :--- |
| **Basic Exploration** | `df.info()` | Inspect dataset structure and data types |
| | `df.describe()` | Generate descriptive statistics |
| | `df.isnull().sum()` | Detect missing values in each column |
| | `df.duplicated().sum()` | Identify duplicate rows |
| | `df.corr()` | Find correlations between numeric variables |
| **Univariate Analysis** | `sns.histplot()` | Plot histogram (distribution of single variable) |
| | `sns.boxplot()` | Identify outliers using boxplot |
| | `sns.countplot()` | Count occurrences of categorical variables |
| **Bivariate Analysis** | `sns.scatterplot()` | Display relationship between two variables |
| | `sns.heatmap()` | Show correlation matrix visually |
| **Multivariate Analysis** | `sns.pairplot()` | Show pairwise relationships across variables |
| **Visualization Controls** | `plt.figure()`, `plt.title()`, `plt.xlabel()`, `plt.ylabel()`, `plt.show()` | Configure and display plotted charts |

## Program & Output
import numpy as np  
import pandas as pd  
import matplotlib.pyplot as plt  
import seaborn as sns  

\# Set style for seaborn plots  
sns.set_theme(style="whitegrid")  

\# Load the Dataset into a Pandas DataFrame  
file_path = 'heartdisease.csv'  
df = pd.read_csv(file_path)  

print("--- 1. Dataset Loaded Successfully ---")  
print(f"Dataset Shape (Rows, Columns): {df.shape}\n")  

\# Display Dataset Structure, Shape, and Descriptive Statistics  
print("--- 2. Dataset Structure and Info ---")  
print(df.info())  

print("\n--- 3. Descriptive Statistics ---")  
print(df.describe())    

\# Check for Missing Values and Duplicate Rows  
print("\n--- 4. Data Cleaning Checks ---")  
missing_values = df.isnull().sum()  
print("Missing Values per Column:\n", missing_values[missing_values > 0] if missing_values.sum() > 0 else "No missing values found.")  

duplicate_count = df.duplicated().sum()  
print(f"Number of Duplicate Rows: {duplicate_count}")  

\# Examine Correlations Among Numeric Features  
print("\n--- 5. Correlation Matrix ---")  
numeric_df = df.select_dtypes(include=[np.number])  
correlation_matrix = numeric_df.corr()  
print(correlation_matrix)  

\# Plotting Correlation Heatmap  
plt.figure(figsize=(10, 8))  
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', fmt=".2f", linewidths=0.5)  
plt.title("Correlation Matrix Heatmap of Numeric Features")  
plt.tight_layout()  
plt.show()  
    
\# Visualize Univariate Distributions  
print("\n--- 6. Generating Univariate Visualizations ---")  

\# Histogram for Age or Cholesterol (`totChol`) if available  
column_to_plot = 'totChol' if 'totChol' in df.columns else numeric_df.columns[0]  
plt.figure(figsize=(8, 5))  
sns.histplot(df[column_to_plot], kde=True, color='blue')  
plt.title(f"Univariate Distribution of {column_to_plot}")  
plt.xlabel(column_to_plot)  
plt.ylabel("Frequency")  
plt.tight_layout()  
plt.show()  

\# Boxplot to detect outliers  
plt.figure(figsize=(8, 5))  
sns.boxplot(x=df[column_to_plot], color='orange')  
plt.title(f"Boxplot for Outlier Detection in {column_to_plot}")  
plt.xlabel(column_to_plot)  
plt.tight_layout()  
plt.show()  

\# Countplot for categorical variable (e.g., TenYearCHD or sex if present)  
cat_column = 'TenYearCHD' if 'TenYearCHD' in df.columns else (df.select_dtypes(include=['object', 'category']).columns[0] if len(df.select_dtypes(include=['object', 'category']).columns) > 0 else None)  
if cat_column:  
    plt.figure(figsize=(6, 4))    
    sns.countplot(x=df[cat_column], palette='Set2')  
    plt.title(f"Countplot of {cat_column}")  
    plt.xlabel(cat_column)    
    plt.ylabel("Count")  
    plt.tight_layout()  
    plt.show()  

\# Analyze Bivariate and Multivariate Relationships  
print("\n--- 7. Generating Bivariate and Multivariate Visualizations ---")  

\# Scatter plot (e.g., Age vs totChol or BMI)  
if 'age' in df.columns and 'totChol' in df.columns:  
    plt.figure(figsize=(8, 5))  
    sns.scatterplot(x='age', y='totChol', hue='TenYearCHD' if 'TenYearCHD' in df.columns else None, data=df, palette='viridis')  
    plt.title("Scatter Plot: Age vs Total Cholesterol")  
    plt.xlabel("Age")  
    plt.ylabel("Total Cholesterol")  
    plt.tight_layout()  
    plt.show()  

\# Pairplot for selected numeric features (subset to keep it clean)  
selected_features = [col for col in ['age', 'totChol', 'BMI', 'sysBP'] if col in df.columns]  
if len(selected_features) > 1:  
    sns.pairplot(df[selected_features].dropna())  
    plt.title("Pairplot of Key Numerical Features", y=1.02)  
    plt.show()  
    
<img width="1392" height="788" alt="image" src="https://github.com/user-attachments/assets/3be1546f-3c0b-4609-9f17-6805da448b74" />

## Result
Thus to perform Exploratory Data Analysis (EDA) on the heart disease dataset to understand the data distribution, relationships, and key patterns useful for business insights and model building successfully.
