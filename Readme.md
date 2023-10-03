<h1 style="font-weight:normal">
  Preppin' Data with Python :snake:, R :pirate_flag:, SQL :snowflake:, Alteryx :arrow_up:, and Tableau Prep :sparkles:
</h1>

Solving [Preppin' Data Challenges](https://preppindata.blogspot.com/).

[![Status](https://img.shields.io/badge/status-active-success.svg)]() [![GitHub Issues](https://img.shields.io/github/issues/wjsutton/preppin-data.svg)](https://github.com/wjsutton/preppin-data/issues) [![GitHub Pull Requests](https://img.shields.io/github/issues-pr/wjsutton/preppin-data.svg)](https://github.com/wjsutton/preppin-data/pulls) [![License](https://img.shields.io/badge/license-MIT-blue.svg)](/LICENSE)


## :a: About 

At the start of 2021 I wanted to improve my data prep skills with Python. Now in 2022 I'm doing the same for Alteryx and Tableau Prep.

[Preppin' Data](https://preppindata.blogspot.com/) is a weekly data prep challenge built around [Tableau Prep](https://www.tableau.com/en-gb/products/prep) but the challenges apply to other tools and even coding languages, so ideal practice if you're looking to improve your data prep skills. 

From participating, I'm much more confident in Python and use Python in projects such as working out the [life expectancy of chess pieces](https://github.com/wjsutton/life_expectancy_in_chess) and finding the [resale value of Pokemon trading cards](https://github.com/wjsutton/pokemon_tcg_stockmarket).

Below are my solutions and Python code snippets I regularly use in these challenges.



## :snake: Python Snippets

### Reading Files

Reading csv files | Example: [W05 2021](https://github.com/wjsutton/preppin-data/blob/main/2021/2021-week-05.py)
```
import pandas as pd

df = pd.read_csv('folder\\filename.csv')
```

Reading Excel files | Example: [W04 2021](https://github.com/wjsutton/preppin-data/blob/main/2021/2021-week-04.py)
```
import pandas as pd

df = pd.read_excel('folder\\filename.xlsx', engine='openpyxl', sheet_name = 'Sheet1')
```

Reading and aggregrating multiple Excel tabs | Example: [W21 2021](https://github.com/wjsutton/preppin-data/blob/main/2021/2021-week-21.py)
```
import pandas as pd

# Read all Excel tabs and concat as one dateframe
all_tabs = pd.read_excel('folder\\filename.xlsx', sheet_name=None)

# Bring all the sheets together
all_dfs = []
for tab_name, df in all_tabs.items():
    df['sheet_name'] = tab_name
    all_dfs.append(df)
    combined_df = pd.concat(all_dfs, ignore_index=True)
```

Skipping rows and columns in an Excel tab | Example: [W48 2021](https://github.com/wjsutton/preppin-data/blob/main/2021/2021-week-48.py)
```
import pandas as pd

df = pd.read_excel('folder\\filename.xlsx', engine='openpyxl', sheet_name='Sheet1',nrows= 3,skiprows = range(1,7), usecols = "B:D")
```

### Writing Files

Writing csv files with utf-8 encoding | Example: [W10 2021](https://github.com/wjsutton/preppin-data/blob/main/2021/2021-week-10.py)
```
import pandas as pd

df.to_csv('folder\\filename.csv', encoding='utf-8-sig', index=False)
```

Writing Excel files | Example: [W14 2021](https://github.com/wjsutton/preppin-data/blob/main/2021/2021-week-14.py)
```
import pandas as pd

with pd.ExcelWriter('folder\\filename.xlsx') as writer:  
    df_1.to_excel(writer, sheet_name='Sheet1', index=False)
    df_2.to_excel(writer, sheet_name='Sheet2', index=False)
    df_3.to_excel(writer, sheet_name='Sheet3', index=False)
```

### DataFrame Transformations

Unioning dataframes together with concat
```
import pandas as pd

df_total = pd.concat([df1,df2,df3])
```

Replacing null values with zero, blank, previous or preceeding values
```
import pandas as pd

# replace nulls with zeroes
df['Column with nulls'] = df['Column with nulls'].fillna(0)

# replace nulls with empty string (blank)
df['Column with nulls'] = df['Column with nulls'].fillna('')

# replace nulls with previous non-null value
df['Column with nulls'] = df['Column with nulls'].fillna(method='ffill')

# replace nulls with next non-null value
df['Column with nulls'] = df['Column with nulls'].fillna(method='bfill')
```

### Aggregrating data

Create aggregrated columns grouped by other columns
```
import pandas as pd

df = df.groupby(['Col1','Col2']).agg(col3_min=('Col3','min'),col3_max=('Col3','max'),col3_sum=('Col3','sum')).reset_index()
```

### Data Clean-up

Rename single column
```
import pandas as pd

df.rename( columns={'Col1':'Col1_New_Name'}, inplace=True )
```
