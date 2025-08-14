# Synthetic Dataset for Paracetamol Reported Incidents in Year 2021
## Random Data Based Approach Applied - Updated by EH in August 2025

## Step 1: Adds-on Applicable Libraries 


```python
import pandas as pd
import numpy as np
import random
from datetime import datetime, timedelta
```

## Step 2: 11 Variables identified Paracetamol Adverse Reported Incidents in 2021


```python
# Set number of records
n = 40000

# Create 1000 random 8-digit "Master IDs"
master_ids = [random.randint(10**7, 10**8 - 1) for _ in range(n)]

# Generate 1,000 samples from a normal distribution
heights = np.random.normal(loc=170, scale=10, size=n)
weights = np.random.normal(loc=70, scale=15, size=n)

# Create a correlation between "height" and "weight"
weights += (heights - 170) * 0.5

# Round and convert to integers
heights = np.round(heights).astype(int)
weights = np.round(weights).astype(int)

# Add categorical data about "sex"
genders = np.random.choice(['Male', 'Female'], size=n)

# Add categorical data about "type of report"
typeofreport = np.random.choice(['Spontanous Report', 'Report from Study', 'Other', 'Unknown'], size=n)

# Create binary flag (0 or 1) for "term_highlighted_by_the_reporter"
# 0 = Highlighted by the reporter NOT serious | 1 = Yes highlighted by the reporter SERIOUS
term_reporter_flag = np.random.choice([0, 1], size=n)

# Create binary flag (0 or 1) for "results_in_death"
# 0 = No | 1 = Yes
death_flag = np.random.choice([0, 1], size=n)

# Create binary flag (0 or 1) for "alert_term"
# 0 = No | 1 = Yes
alert_flag = np.random.choice([0, 1], size=n)

# Add categorical data about "CIOMS_grouped"
CIOMS = np.random.choice(['Serious', 'Non-Serious', 'Fatal'], size=n)

# Add categorical data about "patient_age_group"
age_group = np.random.choice(['Newborns', 'Infant', 'Child', 'Adolescent', 'Adult', 'Elderly'], size=n)

# Function to generate random date within 2021
def random_date_2021():
    start_date = datetime(2021, 1, 1)
    end_date = datetime(2021, 12, 31)
    delta = end_date - start_date
    random_days = random.randint(0, delta.days)
    return start_date + timedelta(days=random_days)

# Generate list of random dates
random_dates = [random_date_2021() for _ in range(n)]

# df['Random_Date_2021'] = df['Random_Date_2021'].dt.strftime('%Y-%m-%d') - if date is required as strings

```

## Step 3: Synthetic Dataset Creation


```python
# Create DataFrame
df = pd.DataFrame({
    'first_recieved_date': random_dates,
    'master_id': master_ids,
    'height_cm': heights,
    'weight_kg': weights,
    'sex':genders,
    'type_of_report': typeofreport,
    'term_highlighted_by_reporter_flag': term_reporter_flag,
    'results_in_death': death_flag,
    'alert_term': alert_flag,
    'CIOMS_grouped': CIOMS,
    'patient_age_group': age_group,
})

print(df.head(50))
print(df.tail(50))
```

## Step 4: Export as a CSV


```python
# Export DataFrame to CSV
df.to_csv('synthetic_paracetamol_dataset_2021.csv', index=False)
```
