# How sparse is my data?
Instructions 1/2
```python
# Subset the DataFrame to include only the 'Age' and 'Gender' columns
sub_df = so_survey_df[['Age', 'Gender']]

# Print the number of non-missing values
print(sub_df.notnull().sum())
```

# Finding the missing values
Instructions 1/3
```python
# Print the top 10 entries of the DataFrame
print(sub_df.head(10))
```
Instructions 2/3
```python
# Print the locations of the missing values
print(sub_df.head(10).isnull())
```
Instructions 3/3
```python
# Print the locations of the non-missing values
print(sub_df.head(10).notnull())
```

# Listwise deletion
Instructions 1/4
```python
# Print the number of rows and columns
print(so_survey_df.shape)
```
Instructions 2/4
```python
# Create a new DataFrame dropping all incomplete rows
no_missing_values_rows = so_survey_df.dropna()

# Print the shape of the new DataFrame
print(no_missing_values_rows.shape)
```
Instructions 3/4
```python
# Create a new DataFrame dropping all columns with incomplete rows
no_missing_values_cols = so_survey_df.dropna(axis=1)

# Print the shape of the new DataFrame
print(no_missing_values_cols.shape)
```
Instructions 4/4
```python
# Drop all rows where Gender is missing
no_gender = so_survey_df.dropna(subset=['Gender'])

# Print the shape of the new DataFrame
print(no_gender.shape)
```

# Replacing missing values with constants
Instructions 1/2
```python
# Print the count of occurrences
print(so_survey_df['Gender'].value_counts())
```
Instructions 2/2
```python
# Replace missing values
so_survey_df['Gender'].fillna('Not Given', inplace=True)

# Print the count of each value
print(so_survey_df['Gender'].value_counts())
```

# Filling continuous missing values
Instructions 1/3
```python
# Print the first five rows of StackOverflowJobsRecommend column
print(so_survey_df['StackOverflowJobsRecommend'].head())
```
Instructions 2/3
```python
# Fill missing values with the mean
so_survey_df['StackOverflowJobsRecommend'].fillna(so_survey_df['StackOverflowJobsRecommend'].mean(), inplace=True)

# Print the first five rows of StackOverflowJobsRecommend column
print(so_survey_df['StackOverflowJobsRecommend'].head())
```
Instructions 3/3
```python
# Fill missing values with the mean
so_survey_df['StackOverflowJobsRecommend'].fillna(so_survey_df['StackOverflowJobsRecommend'].mean(), inplace=True)

# Round the StackOverflowJobsRecommend values
so_survey_df['StackOverflowJobsRecommend'] = so_survey_df['StackOverflowJobsRecommend'].round()

# Print the top 5 rows
print(so_survey_df['StackOverflowJobsRecommend'].head())
```

# Dealing with stray characters (I)
Instructions 1/2
```python
# Remove the commas in the column
so_survey_df['RawSalary'] = so_survey_df['RawSalary'].str.replace(',', '')
```
Instructions 2/2
```python
# Remove the dollar signs in the column
so_survey_df['RawSalary'] = so_survey_df['RawSalary'].str.replace('$', '')
```

#  Dealing with stray characters (II)
Instructions 1/2
```python
# Attempt to convert the column to numeric values
numeric_vals = pd.to_numeric(so_survey_df['RawSalary'], errors='coerce')

# Find the indexes of missing values
idx = numeric_vals.isna()

# Print the relevant rows
print(so_survey_df['RawSalary'][idx])
```
Instructions 2/2
```python
# Replace the offending characters
so_survey_df['RawSalary'] = so_survey_df['RawSalary'].str.replace('£', '')

# Convert the column to float
so_survey_df['RawSalary'] = so_survey_df['RawSalary'].astype(float)

# Print the column
print(so_survey_df['RawSalary'])
```

# Method chaining
```python
# Use method chaining
so_survey_df['RawSalary'] = so_survey_df['RawSalary'] \
                                .str.replace(',', '') \
                                .str.replace('$', '') \
                                .str.replace('£', '') \
                                .astype(float)

# Print the RawSalary column
print(so_survey_df['RawSalary'])
```

