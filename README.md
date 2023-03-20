# Unicorn Companies Dataset Analysis Using Python

The aim of this project is to analyze the growth of unicorn companies based on various factors such as valuation, location, industry, total fundraised, and investors. We will be performing data analysis and visualization on the dataset of unicorn companies to understand the growth patterns of these companies. The insights derived from this analysis will help in understanding the trends in the unicorn companies' ecosystem and how these companies have evolved over the years.

## The dataset for this project has been taken from the URL link:
[Unicorn Companies Dataset](https://www.kaggle.com/datasets/deepcontractor/unicorn-companies-dataset)

## Data Cleaning
**Checking null values and filterning the data**
```
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
## Data Analysis and Visualizations
**1. What are the top 10 most valued unicorn companies?** 
```
**Code**
import pandas as pd 
import numpy as np
import matplotlib.pyplot as plt
uc = pd.read_csv('Unicorn_Companies.csv') 
pd.set_option('display.max_rows',1000) 
pd.set_option('display.max_columns',10) 
pd.set_option('display.max_colwidth',100) 
pd.set_option('display.width',None) 
#print(uc)
uc['Investors Count']=uc['Investors Count'].astype(int) 
uc.head(10).plot(x="Company",y=["Valuation","Investors Count"],kind="bar",figsize=(9,8))
# Display 
plt.xlabel('Company')
plt.ylabel('Valuation') 
plt.legend()
plt.title('Top 10 Valued Unicorn Companies') 
plt.show()
```
<img width="357" alt="111" src="https://user-images.githubusercontent.com/122247029/226221192-58200b99-de37-4445-bc63-9e268ca0ad38.PNG">
**2. Which industry has the most unicorn companies and the minor ones?** 
```
**Code**
import pandas as pd 
import numpy as np
import matplotlib.pyplot as plt 
import seaborn as sns
uc = pd.read_csv('Unicorn_Companies.csv') 
pd.set_option('display.max_rows',1000) 
pd.set_option('display.max_columns',10) 
pd.set_option('display.max_colwidth',100) 
pd.set_option('display.width',None) 
print(uc)
uc = uc.sort_values(by="Valuation", ascending=False).head(20) 
sns.scatterplot(data=uc, x=uc["Founded Year"], y=uc["Industry"], size=uc["Valuation"],legend=False, sizes=(20, 2000), hue=uc["Industry"], alpha=0.5)
plt.xlabel('Founded Year') 
plt.ylabel('Industry') 
plt.legend()
plt.title('Top Valued Unicorn Industry based on valuation and year') 
plt.show()
```
<img width="555" alt="222" src="https://user-images.githubusercontent.com/122247029/226221216-a653e6fa-e078-4db3-97a8-455ed5726669.PNG">
**3. Valuation based on top 10 Country and top 10 City** 
```
**Code**
import pandas as pd
import matplotlib.pyplot as plt
df = pd.read_csv('Unicorn_Companies.csv') 
#print(df)
df = pd.DataFrame(df) 
pd.set_option('display.max_rows',1000) 
pd.set_option('display.max_columns',10) 
pd.set_option('display.max_colwidth',100) 
pd.set_option('display.width', None) 
#print(df)
a = df.groupby('Country').sum().sort_values(by='Valuation',ascending=False).head(10)
a = a.reset_index() 
print(a)
b = df.groupby('City').sum().sort_values(by='Valuation',ascending=False).head(10) 
b = b.reset_index()
print(b)
fig, ax = plt.subplots(figsize=(12,5)) 
ax2 = ax.twinx()
ax.set_title('Valuation Based on Countries and Cities') 
ax.set_xlabel('Valuation ($ in Billion)') 
ax.plot(a['Valuation'], a['Country'], color='green', marker='x') 
ax2.plot(b['Valuation'], b['City'], color='red', marker='o') 
ax.set_ylabel('Country')
ax2.set_ylabel('City') 
ax.legend(['Country']) 
ax2.legend(['City'], loc='upper center')
ax.yaxis.grid(color='lightgray', linestyle='dashed') 
plt.tight_layout()
plt.show()
```
<img width="610" alt="333" src="https://user-images.githubusercontent.com/122247029/226221233-e073415c-4581-4b3b-94b8-b254d08f639b.PNG">
**4. Top five cities with the highest number of Unicorn Companies** 
```
**Code**
import pandas as pd
import matplotlib.pyplot as plt
df = pd.read_csv('Unicorn_Companies.csv') 
#print(df)
df = pd.DataFrame(df) 
pd.set_option('display.max_rows',1000) 
pd.set_option('display.max_columns',10) 
pd.set_option('display.max_colwidth',100) 
pd.set_option('display.width', None)
df.City.value_counts().head(5).plot(kind='pie', textprops={'color':'darkblue'}, autopct='%.1f%%', pctdistance=0.6,labeldistance=1.04, wedgeprops={'edgecolor':'k', 'linestyle': 'dashdot','antialiased':True}, figsize=(10, 10))
plt.title('Top Five Cities with highest number of Unicorn Companies', fontweight='bold')
plt.legend()
```
<img width="367" alt="444" src="https://user-images.githubusercontent.com/122247029/226221259-33c7b3a3-873b-4c4c-b47a-4fb3fabca8e8.PNG">
