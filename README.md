# HR Employee Attrition --- Data Cleaning with Python
## Project Overview
This project focuses on cleaning and preparing an HR Employee
Attrition dataset using Python and pandas.

The objective is to transform the raw HR data into a clean, more
focused dataset that can be used for employee attrition analysis and
visualization.
## Tools Used
- Python
- Pandas
- Jupyter Notebook
  
## Data Cleaning Workflow
1. Import Pandas
import pandas as pd
Pandas is used for loading, inspecting, manipulating, and exporting the
dataset.
2. Load the Dataset
data = pd.read_csv(r"C:\Users\iroge\OneDrive\Desktop\COVENANT PROJECT\Portfolio Projects\Freelance Project\Cleaning Projects\HR-Employee-Attrition.csv")
<img width="1164" height="123" alt="image" src="https://github.com/user-attachments/assets/b55e756f-094b-47f7-8174-26bd93e74919" />

The HR Employee Attrition CSV file is loaded into a pandas DataFrame.
4. Initial Data Inspection
data
data.head()
data.info()
These steps provide an initial view of the dataset, its columns, data
types, and general structure.
<img width="1269" height="573" alt="image" src="https://github.com/user-attachments/assets/578e7e9e-75f8-4ac4-9a68-da763f004cc4" />

5. Select Relevant Columns
Two approaches were used to reduce the dataset to the columns required
for the analysis.
Method 1 --- Select columns to keep
columns_to_keep = [
    'Age', 'Attrition', 'BusinessTravel', 'DailyRate', 'Department',
    'DistanceFromHome', 'Education', 'HourlyRate', 'JobRole',
    'YearsAtCompany', 'YearsInCurrentRole', 'YearsSinceLastPromotion',
    'YearsWithCurrManager'
]

new_data = data[columns_to_keep]
This approach creates a new DataFrame containing only the selected
columns.
<img width="1292" height="585" alt="image" src="https://github.com/user-attachments/assets/48021a66-ec81-4ef8-98d0-d77eac35ab45" />

Method 2 --- Drop unnecessary columns
columns_to_drop = [
    'EducationField', 'EmployeeCount', 'EmployeeNumber',
    'EnvironmentSatisfaction', 'Gender', 'JobInvolvement',
    'JobLevel', 'JobSatisfaction', 'MaritalStatus', 'MonthlyIncome',
    'MonthlyRate', 'NumCompaniesWorked', 'Over18', 'OverTime',
    'PercentSalaryHike', 'PerformanceRating', 'RelationshipSatisfaction',
    'StandardHours', 'StockOptionLevel', 'TotalWorkingYears',
    'TrainingTimesLastYear', 'WorkLifeBalance'
]

data = data.drop(columns=columns_to_drop)
This approach removes columns that were not required for the selected
analysis.
<img width="1270" height="583" alt="image" src="https://github.com/user-attachments/assets/9abbd65f-13d4-4d4e-be0e-b7e92421ee54" />

5. Rename Columns
The notebook checks the column names and renames x to
y.
for i in data.columns:
    print(i.upper())

data = data.rename(columns={"DistanceFromHome": "DistanceHome"})
This makes the selected column name shorter and easier to work with.
<img width="1285" height="579" alt="image" src="https://github.com/user-attachments/assets/39a67290-7be2-4caf-a492-95dbf87f40a2" />

6. Check for Missing Values
data.isna().sum()
This checks the number of missing values in each column.

Missing rows are then removed:
data.dropna(inplace=True)
After this step, the dataset contains only rows without missing values
in the retained columns.
7. Check for Duplicates
data.duplicated().sum()
This checks whether duplicate records exist in the cleaned dataset.
8. Check Dataset Shape
data.shape
The shape check confirms the number of rows and columns remaining after
the cleaning steps.
<img width="1272" height="587" alt="image" src="https://github.com/user-attachments/assets/dfb0596a-88bd-4948-8fdb-af26393e76db" />

9. Inspect Attrition Values
data[data["Attrition"] == "Yes"]["Attrition"].unique()
This checks the values associated with employee attrition.
10. Clean Business Travel Values
The original BusinessTravel values contain underscores. They are
replaced with spaces.
data["BusinessTravel"] = data["BusinessTravel"].str.replace("_", " ")
For example:
Travel_Rarely → Travel Rarely
Travel_Frequently → Travel Frequently
Non-Travel → Non-Travel
This improves the readability of the categorical values.
<img width="1270" height="585" alt="image" src="https://github.com/user-attachments/assets/4ba3a540-32a6-49bb-a395-72f39bc5f00f" />

12. Convert Attrition into Numeric Values
The Attrition column is converted from text values to binary values:
data["Attrition"] = data["Attrition"].apply(
    lambda x: 1 if x == "Yes" else 0
)
The resulting interpretation is:

  Attrition     Value
  Yes               1
No                0

The distribution is then checked:
print(data["Attrition"].value_counts())
print(data["Attrition"].unique())
<img width="1253" height="505" alt="image" src="https://github.com/user-attachments/assets/2dbc7dfb-5c9a-4289-ae19-c22f4cbe0a56" />

12. Export the Cleaned Dataset
data.to_csv("Cleaned_data.csv", index=False)
The cleaned dataset is exported as Cleaned_data.csv.
<img width="1285" height="686" alt="image" src="https://github.com/user-attachments/assets/06873d64-af3d-4e49-be27-50f25091bbef" />

index=False prevents pandas from writing the DataFrame index as an
additional column in the CSV file.
Final Cleaning Steps
The workflow can be summarized as:
1. Load the HR dataset.
2. Inspect the dataset.
3. Identify the columns required for analysis.
4. Remove unnecessary columns.
5. Rename a selected column.
6. Check for missing values.
7. Remove rows containing missing values.
8. Check for duplicate records.
9. Standardize BusinessTravel values.
10. Convert Attrition from Yes/No to 1/0.
11. Verify the cleaned values.
12. Export the cleaned dataset.
Key Data-Cleaning Techniques Demonstrated
- pd.read_csv()
- DataFrame.head()
- DataFrame.info()
- Column selection
- drop(columns=...)
- rename()
- isna().sum()
- dropna()
- duplicated().sum()
- String replacement with .str.replace()
- Conditional transformation with .apply() and lambda
- value_counts()
- CSV export with to_csv(index=False)
Project Outcome
The raw HR Employee Attrition dataset was transformed into a more
focused and analysis-ready dataset by removing unnecessary fields,
handling missing records, standardizing categorical values, converting
the target variable into a numeric format, and exporting the cleaned
data for further analysis.
