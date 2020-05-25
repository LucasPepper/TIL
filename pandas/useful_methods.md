# Useful Description and Selection Methods in Pandas

*There should be one -- and preferably only one -- obvious way to do it.* - The Zen of Python by Tim Peters, Item 13

In Pandas, there are many of them!

## Describing your dataset:
```
df.head(), df.info(), df.describe(), df.shape, df.values, df.columns, df.index, 
```
## Sorting:
```
df.sort_values(['column1_name', 'column2_name'], ascending = [True, False])

dogs_ind3.sort_index(level=["color", "breed"], ascending=[True, False])
```
## Subsetting columns and rows:
```
# Columns
# 2 ways:
df[['column1_name', 'column2_name']]                # 1

cols_to_subset = ['column1_name', 'column2_name'] 
df[cols_to_subset]                                  # 2

# Rows
df['column3_name'] > 50
df[df['column3_name'] > 50]
```
## Subsetting based on conditions:
```
df[df['column3_name'] == 'text']
df[df['column4_date'] > '2020-01-01']

```
### Multiple Conditions:
```
cond1 = df['column3_name'] == 'text'
cond2 = df['column4_date'] > '2020-01-01'

df[cond1 & cond2]                                                           # 1
df[(df['column3_name'] == 'text') & (df['column4_date'] > '2020-01-01')]    # 2
temp[(temp['date'] >= '2010') & (temp['date'] < '2012')
```
## Using .loc[]:
```
# Index temp by country & city
temperatures_ind = temp.set_index(['country', 'city'])

# List of tuples: Brazil, Rio De Janeiro & Pakistan, Lahore
rows_to_keep = [('Brazil', 'Rio De Janeiro'), ('Pakistan', 'Lahore')]

# Subset for rows to keep
temperatures_ind.loc[rows_to_keep])
```

## Using .isin():
```
has_x_or_y_value = df['column1_name'].isin([10, 20])
df[has_x_or_y_value]
```

[Pandas Documentation](https://pandas.pydata.org/docs/user_guide/index.html)