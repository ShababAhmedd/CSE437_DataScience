# Uniform currencies
```python 
# Find values of acct_cur that are equal to 'euro'
acct_eu = banking['acct_cur'] == 'euro'

# Convert acct_amount where it is in euro to dollars
banking.loc[acct_eu, 'acct_amount'] = banking.loc[acct_eu, 'acct_amount'] * 1.1

# Unify acct_cur column by changing 'euro' values to 'dollar'
banking.loc[acct_eu, 'acct_cur'] = 'dollar'

# Assert that only dollar currency remains
assert banking['acct_cur'].unique() == ['dollar']
```


# Uniform dates 
Instructions 1/4 
```python
# Print the header of account_opened
print(banking['account_opened'].head())
```

Instructions 3/4 
```python
# Print the header of account_opened
print(banking['account_opened'].head())

# Convert account_opened to datetime
banking['account_opened'] = pd.to_datetime(banking['account_opened'],
                                           # Infer datetime format
                                           infer_datetime_format=True,
                                           # Return missing value for error
                                           errors='coerce')
```

Instructions 4/4

```python
# Print the header of account_opened
print(banking['account_opened'].head())

# Convert account_opened to datetime
banking['account_opened'] = pd.to_datetime(banking['account_opened'],
                                           # Infer datetime format
                                           infer_datetime_format=True,
                                           # Return missing value for error
                                           errors='coerce')

# Get year of account opened
banking['acct_year'] = banking['account_opened'].dt.strftime('%Y')

# Print acct_year
print(banking['acct_year'])
```

# How's our data integrity?
Instructions 1/2
```python
# Store fund columns to sum against
fund_columns = ['fund_A', 'fund_B', 'fund_C', 'fund_D']

# Find rows where fund_columns row sum == inv_amount
inv_equ = (banking[fund_columns].sum(axis=1) == banking['inv_amount'])

# Store consistent and inconsistent data
consistent_inv = banking[inv_equ]
inconsistent_inv = banking[~inv_equ]

# Print number of inconsistent investments
print("Number of inconsistent investments:", inconsistent_inv.shape[0])
```
Instructions 2/2
```python
import datetime

# Store today's date and find ages
today = datetime.date.today()
ages_manual = today.year - banking['birth_date'].dt.year

# Find rows where age column == ages_manual
age_equ = banking['age'] == ages_manual

# Store consistent and inconsistent data
consistent_ages = banking[age_equ]
inconsistent_ages = banking[~age_equ]

# Print number of inconsistent ages
print("Number of inconsistent ages:", inconsistent_ages.shape[0])
```

# Missing investors
Instructions 1/4
```python
# Print number of missing values in banking
print(banking.isna().sum())

# Visualize missingness matrix
msno.matrix(banking)
plt.show()
```
Instructions 2/4
```python
# Isolate missing and non-missing values of inv_amount
missing_investors = banking[banking['inv_amount'].isnull()]
investors = banking[~banking['inv_amount'].isnull()]
```
Instructions 4/4
```python
# Sort banking by age
banking_sorted = banking.sort_values(by='age')

# Visualize missingness matrix of banking_sorted
msno.matrix(banking_sorted)
plt.show()
```

# Follow the money
```python
# Drop missing values of cust_id
banking_fullid = banking.dropna(subset=['cust_id'])

# Compute estimated acct_amount
acct_imp = banking_fullid['inv_amount'] * 5

# Impute missing acct_amount with corresponding acct_imp
banking_imputed = banking_fullid.fillna({'acct_amount': acct_imp})

# Print number of missing values
print(banking_imputed.isna().sum())
```


