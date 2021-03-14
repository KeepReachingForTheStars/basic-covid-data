# basic-covid-data
Review basic information on COVID-19 data

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.ticker import StrMethodFormatter
import csv

# data source: https://github.com/owid/covid-19-data/blob/master/public/data/vaccinations/us_state_vaccinations.csv
# pulled ~ 11:23pm on 3/4/21 and saved as csv file

# read data and store it as a data frame object in the variable covid_vaccines
covid_vaccines = pd.read_csv(r"C:\Users\hpdda\Desktop\vaccinations_test.csv")
print(covid_vaccines)

# list of column headers
with open(r'C:\Users\hpdda\Desktop\vaccinations_test.csv') as f:
    reader = csv.reader(f)
    i = next(reader)
    print(i)

# print number of rows by number of columns
print(covid_vaccines.shape)

# Data type of columns:
# vaccine_data_type = covid_vaccines.dtypes
# print(vaccine_data_type)

# Information about the date, specifically the columns (note: return of RangeIndex = 3403 rows)
covid_vaccines.info()

# print(covid_vaccines.describe(include=object))
# print(covid_vaccines.describe())

# Exploring Data sets
print(covid_vaccines["date"].value_counts())

# print(covid_vaccines["total_vaccinations"].max())

# dropping rows with null values and check to see rows are the same in all columns
rows_without_nulls = covid_vaccines.dropna()
rows_without_nulls.info()

# Histogram of vaccinations
_ = plt.hist(covid_vaccines["total_vaccinations"], bins=20)
plt.tight_layout()
plt.show()

# Bar chart of vaccinations
_ = plt.bar(x=rows_without_nulls["date"], height=10, bottom=rows_without_nulls["total_vaccinations"])
plt.show()

# max and max of covid vaccines
total_vaccinations = covid_vaccines["total_vaccinations"]
max_value = total_vaccinations.max()
min_value = total_vaccinations.min()
print(max_value, min_value)
