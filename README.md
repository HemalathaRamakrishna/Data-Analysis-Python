# Unicorn Companies Datase Analysis Using Python

The aim of this project is to analyze the growth of unicorn companies based on various factors such as valuation, location, industry, total fundraised, and investors. We will be performing data analysis and visualization on the dataset of unicorn companies to understand the growth patterns of these companies. The insights derived from this analysis will help in understanding the trends in the unicorn companies' ecosystem and how these companies have evolved over the years.

## The dataset for this project has been taken from the URL link:
[Unicorn Companies Dataset](https://www.kaggle.com/datasets/deepcontractor/unicorn-companies-dataset)

## Data Cleaning
**Checking null values and filterning the data**
```
Code
import pandas as pd 
import numpy as np
uc = pd.read_csv('Unicorn_Companies.csv') 
print(uc)
#Check if NaN is present is the dataframe 
uc = uc.isna()
print(uc)

#Check if drop Nan values from dataframe 
uc = uc.dropna()
print(uc)
```
**Removing duplicate values**
```
import pandas as pd
import numpy as np
uc = pd.read_csv('Unicorn_Companies.csv') 
print(uc.head(15))
#To remove duplicate values 
uc = uc.drop_duplicates() 
print(uc.head(15))
```
**Converting column data type**
```
import pandas as pd
df = pd.read_csv('Unicorn_Companies.csv') 
#print(df)
df = pd.DataFrame(df) 
pd.set_option('display.max_rows',1000) 
pd.set_option('display.max_columns',10)
pd.set_option('display.max_colwidth',100) 
pd.set_option('display.width', None) 
#print(df)
#Rename Column "Valuation ($B)" to "Valuation" and remove "$B" from the column 
df.rename(columns = {'Valuation ($B)' : 'Valuation'}, inplace = True) 
df['Valuation']=df['Valuation'].replace('$', '')
df.Valuation = pd.to_numeric(df.Valuation) 
print(df)
```
