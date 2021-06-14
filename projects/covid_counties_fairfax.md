```python
import pandas as pd
import numpy as np

path_in = r'https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-counties.csv'
counties = pd.read_csv(path_in, dtype={'fips':object})
```


```python
counties.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1417147 entries, 0 to 1417146
    Data columns (total 6 columns):
     #   Column  Non-Null Count    Dtype  
    ---  ------  --------------    -----  
     0   date    1417147 non-null  object 
     1   county  1417147 non-null  object 
     2   state   1417147 non-null  object 
     3   fips    1404223 non-null  object 
     4   cases   1417147 non-null  int64  
     5   deaths  1385594 non-null  float64
    dtypes: float64(1), int64(1), object(4)
    memory usage: 64.9+ MB
    


```python
counties.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date</th>
      <th>county</th>
      <th>state</th>
      <th>fips</th>
      <th>cases</th>
      <th>deaths</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020-01-21</td>
      <td>Snohomish</td>
      <td>Washington</td>
      <td>53061</td>
      <td>1</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-01-22</td>
      <td>Snohomish</td>
      <td>Washington</td>
      <td>53061</td>
      <td>1</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020-01-23</td>
      <td>Snohomish</td>
      <td>Washington</td>
      <td>53061</td>
      <td>1</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020-01-24</td>
      <td>Cook</td>
      <td>Illinois</td>
      <td>17031</td>
      <td>1</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020-01-24</td>
      <td>Snohomish</td>
      <td>Washington</td>
      <td>53061</td>
      <td>1</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
counties[counties.county == 'Fairfax'].head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date</th>
      <th>county</th>
      <th>state</th>
      <th>fips</th>
      <th>cases</th>
      <th>deaths</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>739</th>
      <td>2020-03-07</td>
      <td>Fairfax</td>
      <td>Virginia</td>
      <td>51059</td>
      <td>1</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>851</th>
      <td>2020-03-08</td>
      <td>Fairfax</td>
      <td>Virginia</td>
      <td>51059</td>
      <td>2</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>981</th>
      <td>2020-03-09</td>
      <td>Fairfax</td>
      <td>Virginia</td>
      <td>51059</td>
      <td>4</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1143</th>
      <td>2020-03-10</td>
      <td>Fairfax</td>
      <td>Virginia</td>
      <td>51059</td>
      <td>4</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1342</th>
      <td>2020-03-11</td>
      <td>Fairfax</td>
      <td>Virginia</td>
      <td>51059</td>
      <td>4</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
fairfax = counties[counties.fips == '51059'].copy()
fairfax.loc[:,'date'] = pd.to_datetime(fairfax.loc[:,'date'])
fairfax = fairfax.set_index(fairfax.loc[:,'date'])
fairfax = fairfax.drop(['date'], axis=1)
```


```python
fairfax.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>county</th>
      <th>state</th>
      <th>fips</th>
      <th>cases</th>
      <th>deaths</th>
    </tr>
    <tr>
      <th>date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-03-07</th>
      <td>Fairfax</td>
      <td>Virginia</td>
      <td>51059</td>
      <td>1</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2020-03-08</th>
      <td>Fairfax</td>
      <td>Virginia</td>
      <td>51059</td>
      <td>2</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2020-03-09</th>
      <td>Fairfax</td>
      <td>Virginia</td>
      <td>51059</td>
      <td>4</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2020-03-10</th>
      <td>Fairfax</td>
      <td>Virginia</td>
      <td>51059</td>
      <td>4</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2020-03-11</th>
      <td>Fairfax</td>
      <td>Virginia</td>
      <td>51059</td>
      <td>4</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
fairfax['new_cases'] = fairfax.loc[:,'cases'] - fairfax.loc[:,'cases'].shift(1)
fairfax.iloc[0, fairfax.columns.get_loc('new_cases')] = 1.0
fairfax['cases_sma7'] = fairfax.loc[:,'new_cases'].rolling(window=7).mean().round(0)

fairfax['new_deaths'] = fairfax.loc[:,'deaths'] - fairfax.loc[:,'deaths'].shift(1)
fairfax.iloc[0, fairfax.columns.get_loc('new_deaths')] = 0.0
fairfax['deaths_sma7'] = fairfax.loc[:,'new_deaths'].rolling(window=7).mean().round(0)

fairfax['cases_per_100k'] = ((fairfax.cases_sma7 / 1147532) * 100000).round(2)

fairfax['deaths_per_100k'] = ((fairfax.deaths_sma7 / 1147532) * 100000).round(2)

fairfax = fairfax[[
    'county', 
    'state',
    'fips',
    'cases',
    'new_cases',
    'cases_sma7',
    'cases_per_100k',
    'deaths', 
    'new_deaths',
    'deaths_sma7',
    'deaths_per_100k',
]].copy()
```


```python
fairfax.tail()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>county</th>
      <th>state</th>
      <th>fips</th>
      <th>cases</th>
      <th>new_cases</th>
      <th>cases_sma7</th>
      <th>cases_per_100k</th>
      <th>deaths</th>
      <th>new_deaths</th>
      <th>deaths_sma7</th>
      <th>deaths_per_100k</th>
    </tr>
    <tr>
      <th>date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2021-06-09</th>
      <td>Fairfax</td>
      <td>Virginia</td>
      <td>51059</td>
      <td>77021</td>
      <td>-7.0</td>
      <td>2.0</td>
      <td>0.17</td>
      <td>1105.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2021-06-10</th>
      <td>Fairfax</td>
      <td>Virginia</td>
      <td>51059</td>
      <td>77027</td>
      <td>6.0</td>
      <td>2.0</td>
      <td>0.17</td>
      <td>1105.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2021-06-11</th>
      <td>Fairfax</td>
      <td>Virginia</td>
      <td>51059</td>
      <td>77026</td>
      <td>-1.0</td>
      <td>1.0</td>
      <td>0.09</td>
      <td>1105.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2021-06-12</th>
      <td>Fairfax</td>
      <td>Virginia</td>
      <td>51059</td>
      <td>77026</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>1105.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2021-06-13</th>
      <td>Fairfax</td>
      <td>Virginia</td>
      <td>51059</td>
      <td>77023</td>
      <td>-3.0</td>
      <td>-1.0</td>
      <td>-0.09</td>
      <td>1105.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
import matplotlib
import matplotlib.pyplot as plt
%matplotlib inline

fig, axs = plt.subplots(2, 2, figsize=(16, 14))

fig.suptitle('Covid-19 Cases and Deaths\nFairfax County, VA', fontsize=18)

axs[0,0].plot(fairfax.cases_sma7)
axs[0,0].set_ylabel('Cases per Day')
axs[0,0].set_title('Daily Confirmed Cases (7-Day Rolling Average)')

axs[0,1].plot(fairfax.deaths_sma7)
axs[0,1].set_ylabel('Deaths per Day')
axs[0,1].set_title('Daily Confirmed Deaths (7-Day Rolling Average)')

axs[1,0].plot(fairfax.cases_per_100k)
axs[1,0].set_title('Daily Cases per 100,000')

axs[1,1].plot(fairfax.deaths_per_100k)
axs[1,1].set_title('Daily Deaths per 100,000')

fig.savefig(r'/Users/edpar/Desktop/fairfax_covid.jpeg', dpi=300)  
# display(fig)

plt.show()
```


![png](output_8_0.png)



```python
fairfax_covid = fairfax[[
    'county', 
    'state',
    'fips',
    'cases_sma7',
    'cases_per_100k', 
    'deaths_sma7',
    'deaths_per_100k',
]]
```


```python
path_out = r'C:\Users\edpar\Documents\6 - Social Explorer\Higher Ed Project\fairfax_covid.csv'
# fairfax_covid.to_csv(path_out, index = False, header = True)
```


```python

```
