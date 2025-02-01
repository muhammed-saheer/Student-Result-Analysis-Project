# Student Result Analysis Project

## Introduction
This project involves analyzing student results using Python to uncover patterns and insights that can help improve student performance. The dataset used for this project is sourced from Kaggle and includes various student attributes such as gender, parental education, ethnic group, and scores in subjects like Mathematics, Reading, and Writing.


## Dataset
The dataset used for this project is sourced from Kaggle. You can find the dataset[here](https://www.kaggle.com/datasets/desalegngeb/students-exam-scores/data?select=Expanded_data_with_more_features.csv).

## Libraries Used
The following Python libraries are used for data processing and visualization:

- **numpy** – for numerical operations
- **pandas** – for data manipulation and analysis
- **matplotlib** – for data visualization
- **seaborn** – for advanced statistical plotting


## Project Steps


```python
# Data Loading and Preparation
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load the dataset
data = pd.read_csv("stdn_scrs.csv")

# Display first few rows of the dataset
data.head()

# Get information about the dataset
data.info()

# Check for missing values
data.isnull().sum()

# Drop unnecessary columns
data = data.drop("Unnamed: 0", axis=1)

# Display first 5 rows after dropping the column
data.head(5)

# Gender Distribution
plt.figure(figsize=(5,5))
ax = sns.countplot(data=data, x="Gender")
colors = ['#FF6347', '#4682B4']  # Specify your colors here
for bar, color in zip(ax.patches, colors):
    bar.set_facecolor(color)
ax.bar_label(ax.containers[0])
plt.title("Gender Distribution")
plt.show()

# Relationship between Parent's Education and Student's Score
gb = data.groupby("ParentEduc").agg({"MathScore":'mean', "ReadingScore":'mean', "WritingScore":'mean'})
plt.figure(figsize=(4,4))
sns.heatmap(gb, annot=True)
plt.title("Relationship between Parent's Education and Student's Score")
plt.show()

# Relationship between Parent's Marital Status and Student's Score
gb1 = data.groupby("ParentMaritalStatus").agg({"MathScore":'mean', "ReadingScore":'mean', "WritingScore":'mean'})
plt.figure(figsize=(4,4))
sns.heatmap(gb1, annot=True)
plt.title("Relationship between Parent's Marital Status and Student's Score")
plt.show()

# Math Score Distribution
sns.boxplot(data=data, x="MathScore")
plt.show()

# Reading Score Distribution
sns.boxplot(data=data, x="ReadingScore")
plt.show()

# Writing Score Distribution
sns.boxplot(data=data, x="WritingScore")
plt.show()

# Ethnic Group Distribution
print(data["EthnicGroup"].unique())
groupA = data.loc[(data['EthnicGroup'] == "group A")].count()
groupB = data.loc[(data['EthnicGroup'] == "group B")].count()
groupC = data.loc[(data['EthnicGroup'] == "group C")].count()
groupD = data.loc[(data['EthnicGroup'] == "group D")].count()
groupE = data.loc[(data['EthnicGroup'] == "group E")].count()

labels = ["group A", "group B", "group C", "group D", "group E"]
mlist = [groupA["EthnicGroup"], groupB["EthnicGroup"], groupC["EthnicGroup"], groupD["EthnicGroup"], groupE["EthnicGroup"]]

# Pie chart of Ethnic Groups
plt.pie(mlist, labels=labels, autopct="%1.2f%%")
plt.title("Distribution of Ethnic Groups")
plt.show()

# Count plot of Ethnic Groups
a = sns.countplot(data=data, x='EthnicGroup')
a.bar_label(a.containers[0])
plt.show()
```

## Results
- Key findings from the data analysis, such as the impact of study time on grades, etc.

## Conclusion
Based on the analysis, recommendations are made to improve student performance in future exams.
