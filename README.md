import pandas as pd

# 1. Load the Dataset
df = pd.read_csv("https://raw.githubusercontent.com/datasciencedojo/datasets/master/titanic.csv")

print("Before Cleaning - Rows:", df.shape[0], "Columns:", df.shape[1])
print("\nMissing Values:")
print(df.isnull().sum())

# 2. Handle Missing Values
df['Age'] = df['Age'].fillna(df['Age'].median())
df['Embarked'] = df['Embarked'].fillna(df['Embarked'].mode()[0])
df['Fare'] = df['Fare'].fillna(df['Fare'].median())

# 3. Drop Unnecessary Columns
# Cabin has 77% missing values, so we drop it
df = df.drop(columns=['Cabin', 'Ticket', 'Name', 'PassengerId'])

# 4. Remove Duplicate Rows
df = df.drop_duplicates()

# 5. Clean Text Data
df['Sex'] = df['Sex'].str.strip().str.lower()
df['Embarked'] = df['Embarked'].str.strip().str.upper()

# 6. Fix Data Types
df['Survived'] = df['Survived'].astype(int)
df['Pclass'] = df['Pclass'].astype(int)

# 7. Save Cleaned File
df.to_csv("titanic_cleaned.csv", index=False)

print("\nAfter Cleaning - Rows:", df.shape[0], "Columns:", df.shape[1])
print("\nMissing Values After Cleaning:")
print(df.isnull().sum())
print("\nCleaned file saved as titanic_cleaned.csv")
