Student Data ETL Project
Project Overview

This project demonstrates a complete ETL (Extract, Transform, Load) workflow using Python and PostgreSQL.

We take a student performance dataset, clean and transform it, and load it into a PostgreSQL database. Additionally, we perform basic exploratory data analysis (EDA) to understand the dataset.

Dataset

The dataset contains information about 395 students and 33 columns, including:

Column	Description
school	Student's school
sex	Gender (F/M)
age	Age in years
address	Home address type (Urban/Rural)
famsize	Family size
Pstatus	Parent's cohabitation status
Medu	Mother's education level
Fedu	Father's education level
Mjob	Mother's job
Fjob	Father's job
reason	Reason for choosing school
guardian	Student's guardian
traveltime	Home to school travel time
studytime	Weekly study time
failures	Number of past class failures
schoolsup	Extra educational support
famsup	Family educational support
paid	Extra paid classes
activities	Extracurricular activities
nursery	Attended nursery school
higher	Wants higher education
internet	Internet access at home
romantic	Has a romantic relationship
famrel	Quality of family relationships
freetime	Free time after school
goout	Going out with friends
Dalc	Workday alcohol consumption
Walc	Weekend alcohol consumption
health	Current health status
absences	Number of school absences
G1, G2, G3	Grades for 1st, 2nd, and final periods
Project Steps
1️⃣ Import Libraries

We import essential libraries for data manipulation, visualization, and database connectivity:

import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
from sqlalchemy import create_engine
import psycopg2

2️⃣ Load Dataset

Load the CSV dataset into a Pandas DataFrame:

df = pd.read_csv("student.csv")
df.head()


Shows the first 5 rows of the dataset.

3️⃣ Data Cleaning & Transformation

Check missing values:

df.isnull().sum()


Encode categorical columns (e.g., one-hot encoding for multi-category columns):

multi_cols = ['school', 'Mjob', 'Fjob', 'reason', 'guardian']
df = pd.get_dummies(df, columns=multi_cols, drop_first=True)


Ensure numeric columns are correct and no outliers are present.

4️⃣ Load Data into PostgreSQL

Create database: student_db (if not already exists)

Connect and load DataFrame:

engine = create_engine('postgresql://username:password@localhost:5432/student_db')
df.to_sql('students', engine, if_exists='replace', index=False)


Table students is now available in PostgreSQL under schema public.

5️⃣ Exploratory Data Analysis (EDA)
a) Summary statistics
df.describe()

b) Distribution of final grades
sns.histplot(df['G3'], kde=True)
plt.title("Distribution of Final Grades")
plt.show()

c) Study time vs Final Grade
sns.boxplot(x='studytime', y='G3', data=df)
plt.title("Study Time vs Final Grade")
plt.show()

d) Correlation heatmap
plt.figure(figsize=(12,8))
sns.heatmap(df.corr(), annot=True, cmap='coolwarm')
plt.title("Correlation Heatmap")
plt.show()


Provides insights on relationships between features (e.g., studytime, absences, alcohol consumption) and final grade.

6️⃣ Verification in PostgreSQL

Check that table exists and data is loaded:

query = "SELECT * FROM public.students LIMIT 5;"
df_check = pd.read_sql(query, engine)
df_check.head()

Project Highlights

Showcases data cleaning, transformation, and database ETL.

Uses Python (Pandas, SQLAlchemy, psycopg2) and PostgreSQL.

Includes basic EDA to explore student performance.

Ready for extension to analytics, reporting, or machine learning.



✅ With this README + notebook, your project is professional, social-media ready, and GitHub-ready.

If you want, I can also create a shorter version of this README formatted for LinkedIn/Instagram post, highlighting ETL + insights visually, so it’s attractive to non-technical audiences.
