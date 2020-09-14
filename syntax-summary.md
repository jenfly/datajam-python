# Syntax Summary

## Pandas

### Importing `pandas` Library
```python
import pandas
```
> In general, it's good practice to collect all your `import` commands together and put them at the start of the notebook.

### DataFrames and Series

Data in `pandas` is organized into DataFrames and Series.

- **DataFrame:** 2-dimensional array, like a table in a spreadsheet
- **Series:** 1-dimensional array, like a single column or row in a spreadsheet
  - Each individual column or row of a DataFrame is represented as a Series

### Reading a CSV File

To read a CSV file and store it as a DataFrame variable:
```python
df = pandas.read_csv('some_cool_data.csv')
```

Missing data in a DataFrame or Series is represented as `NaN` ("not a number").

### Saving to a CSV File

To save a DataFrame to a CSV file: 
```python
df.to_csv('cool_output.csv', index=False)
```
- To include the DataFrame's index as a column in the CSV file, omit the `index=False` keyword argument.

### Quick and Easy Summaries of a DataFrame

|||
---|----
**General Overview** | 
Number of rows and columns; names, data types, and non-null counts for each column; memory usage | `df.info()`
**Useful Attributes** |
Number of rows and columns (rows first, columns second) | `df.shape` 
Names and data types of each column |  `df.dtypes` 
Just the names of each column | `df.columns` 
**Rows at a Glance** |
First `n` rows (default 5) |`df.head(n)`
Last `n` rows (default 5) | `df.tail(n)`
A random sampling of `n` rows (default 1) | `df.sample(n)`

#### Summary Statistics

Full set of summary statistics (min, max, mean, standard deviation, etc.) for each numerical column of a DataFrame:
```python
df.describe()
```

Mean value of each column:
```python
df.mean()
```

And similarly for other summary statistics: `df.min()`, `df.max()`, `df.median()`, `df.std()`

### Selecting Columns

#### Single Columns

Each column of a DataFrame is a Series.
```python
series_X = df['X']
```

Most DataFrame methods can be applied to a Series, for example:
```python
df['X'].head()
df['X'].max()
```

#### Multiple Columns

Use a list of column names to select several columns of a DataFrame, in a specified order:
```python
df_subset = df[['E', 'A', 'C']]
```

### Selecting Rows

Extracting rows from a DataFrame or Series based on a criteria:
  - Create a filter (Boolean Series) using a comparison operator or other functions (such as the `isin()` method)
  - Use the filter to extract the desired rows from the DataFrame

Example:
```python
world_long_life = world[world['life_expectancy'] > 82] 
```

### Selecting Rows and Columns

To select both rows and columns, use `.loc[<rows>, <columns>]`:
```python
canada_pop = world.loc[world['country'] == 'Canada', 
                       ['country', 'year', 'population']
                      ]
```

### Creating New Columns

```python
df['Double X'] = 2 * df['X']
```

### Unique Values & Counting

For a column `df['A']` which contains many repeated values (such as categories), some useful summary methods are:

|||
---|---
Unique values | `df['A'].unique()`
Number of unique values | `df['A'].nunique()`
Counts of each unique value | `df['A'].value_counts()`

> Note: The `unique()` and `value_counts()` methods can only be applied to a Series (not a DataFrame)

### Sorting

Sorting a DataFrame based on the values in the column `'B'`:
```python
df.sort_values('B')
```
To sort in descending order, use the keyword argument `ascending=False`.

### Aggregation

For basic aggregation operations, use the `groupby()` method chained with an aggregation method (e.g., `sum()`, `mean()`, `sum()`, `max()`, etc.)
- Use `as_index=False` keyword argument to keep the grouping variable as a regular column rather than the index

For example, to find the sum totals of column `'population'` grouped by column `'region'`: `
```python
world_2015.groupby('region', as_index=False)['population'].sum()
```

You can also group by multiple columns:
```python
world_2015.groupby(['region', 'income_group'], as_index=False)['population'].sum()
```

For more complex aggregations, you can use the `agg` method:

Specify a list of aggregation statistics, for example: 
```python
world_2015.groupby('region', as_index=False)['population'].agg(['sum', 'min', 'max'])
```

Use a dictionary to specify different aggregation statistics for different columns, for example:

```python
agg_dict = {'population' : 'sum', 
            'life_expectancy' : ['min', 'max']}
world.groupby('region', as_index=False).agg(agg_dict)
```

## Data Visualization

## Simple Plots with Pandas

Bar plot:

```python
region_pop.plot(x='region', y='pop_millions', kind='bar');
```

Scatter plot:

```python
world_2015.plot(x='gdp_per_capita', y='life_expectancy', kind='scatter');
```

Saving a plot:
```python
ax = region_pop.plot(x='region', y='pop_millions', kind='bar');
ax.get_figure().savefig('region_populations.png', bbox_inches='tight')
```

## Statistical Plots with Seaborn

Import library:

```python
import seaborn as sns
```

Switch to `seaborn` default aesthetics:

```python
sns.set()
```

Example scatter plot with axes customization:

```python
g = sns.relplot(data=world_2015, x='gdp_per_capita', y='life_expectancy', hue='region',
                size='pop_millions', sizes=(40, 400), alpha=0.8)
g.set(xscale='log', title='Life Expectancy vs. GDP per Capita in 2015');
```

Example scatter plot with facets:

```python
income_order= ['Low', 'Lower middle', 'Upper middle', 'High']
g = sns.relplot(data=world_2015, x='gdp_per_capita', y='life_expectancy', col='region',
                col_wrap=3, height=3, hue='income_group', hue_order=income_order)
g.set(xscale='log');
```

Example line plot with aggregation and facets:

```python
sns.relplot(data=world, x='year', y='pop_millions', hue='income_group', hue_order=income_order,
            style='income_group', kind='line', estimator='sum', ci=None, col='region',
            col_wrap=3, height=3);
```

Example bar plot with aggregation:

```python
g = sns.catplot(data=world_2015, x='region', y='life_expectancy', kind='bar', aspect=1.5)
g.set(title='Mean Life Expectancy by Region in 2015');
```

Saving a plot:
```python
g = sns.relplot(data=world_2015, x='gdp_per_capita', y='life_expectancy', hue='region',
                size='pop_millions', sizes=(40, 400), alpha=0.8)
g.set(xscale='log', title='Life Expectancy vs. GDP per Capita in 2015');
g.savefig('life_exp_vs_gdp_percap.png')
```


## Interactive Plots with Plotly

Import Plotly Express:

```python
import plotly.express as px
```

Example scatter plot:

```python
px.scatter(data_frame=world_2015, x='gdp_per_capita', y='life_expectancy', color='region',
           size='pop_millions', size_max=30, log_x=True, hover_data=['country'],
           title='Life Expectancy vs. GDP per Capita in 2015')
```

Example scatter plot with facets:

```python
px.scatter(data_frame=world_2015, x='gdp_per_capita', y='life_expectancy', 
           facet_col='region', facet_col_wrap=3,
           color='income_group', 
           category_orders={'income_group' : ['Low', 'Lower middle', 'Upper middle', 'High']},
           log_x=True, hover_data=['country'],
           title='Life Expectancy vs. GDP per Capita in 2015')
```

Example scatter plot with animation:

```python
px.scatter(data_frame=world, x='gdp_per_capita', y='life_expectancy', color='region',
           size='pop_millions', size_max=30, log_x=True, range_y=(20, 90),
           title='Life Expectancy vs. GDP per Capita (1950-2015)',
           animation_frame='year')
```

Saving a figure:

```python
fig = px.scatter(data_frame=world_2015, x='gdp_per_capita', y='life_expectancy', color='region',
                 size='pop_millions', size_max=30, log_x=True, hover_data=['country'],
                 title='Life Expectancy vs. GDP per Capita in 2015')

# Save to HTML (interactive)
fig.write_html('plotly_life_exp_vs_gdp_percap.html')

# Save as a static PNG image
fig.write_image('plotly_life_exp_vs_gdp_percap.png')
```

---
Back to [home](https://jenfly.github.io/datajam-python/0-jupyter.html)
