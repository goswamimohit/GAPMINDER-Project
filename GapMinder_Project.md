# GapMinder Project


```python
import pandas as pd
import matplotlib.pyplot as plt
```


```python
gapminder = pd.read_excel("Gapminder_key_1.xlsx")
```


```python
gapminder.head()
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
      <th>country</th>
      <th>year</th>
      <th>population</th>
      <th>continent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>1952</td>
      <td>8425333</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Afghanistan</td>
      <td>1957</td>
      <td>9240934</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Afghanistan</td>
      <td>1962</td>
      <td>10267083</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Afghanistan</td>
      <td>1967</td>
      <td>11537966</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Afghanistan</td>
      <td>1972</td>
      <td>13079460</td>
      <td>Asia</td>
    </tr>
  </tbody>
</table>
</div>




```python
gapminder2 = pd.read_excel("Gapminder_key_2.xlsx")
```


```python
gapminder2.head()
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
      <th>country</th>
      <th>year</th>
      <th>life_exp</th>
      <th>gdp_cap</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>1952</td>
      <td>28.801</td>
      <td>779.445314</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Afghanistan</td>
      <td>1957</td>
      <td>30.332</td>
      <td>820.853030</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Afghanistan</td>
      <td>1962</td>
      <td>31.997</td>
      <td>853.100710</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Afghanistan</td>
      <td>1967</td>
      <td>34.020</td>
      <td>836.197138</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Afghanistan</td>
      <td>1972</td>
      <td>36.088</td>
      <td>739.981106</td>
    </tr>
  </tbody>
</table>
</div>




```python
df = pd.merge(gapminder,gapminder2 ,how='inner',on=['country','year'])
```


```python
df.shape
```




    (1704, 6)




```python
df['life_exp'].std()
```




    12.917107415241187




```python
df['gdp_cap'].mean()
```




    7215.327081212142




```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 1704 entries, 0 to 1703
    Data columns (total 6 columns):
     #   Column      Non-Null Count  Dtype  
    ---  ------      --------------  -----  
     0   country     1704 non-null   object 
     1   year        1704 non-null   int64  
     2   population  1704 non-null   int64  
     3   continent   1704 non-null   object 
     4   life_exp    1704 non-null   float64
     5   gdp_cap     1704 non-null   float64
    dtypes: float64(2), int64(2), object(2)
    memory usage: 93.2+ KB
    

### Country and Continents are in string data type ,convert them into categorial type of data by using progarmming consrtuct.


```python
df1 = df.astype({"country":'category', "continent":'category'})
```


```python
gdp_sort['GDP'] = gdp_sort['gdp_cap'] * gdp_sort['population']
```


```python
gdp_sort = df1.sort_values(by = 'gdp_cap',ascending = False)
```


```python
gdp_sort.GDP.max()
```




    12934458535084.986



### Total number of country in dataset.


```python
grp_cont = gdp_sort.groupby('country')
```


```python
len(set(gdp_sort['country']))
```




    142




```python
df2 = df1.drop_duplicates('country')
df2['country'].count()
```




    142



### Which country has lowest life-expectancy in 2007.


```python
Gapminder_2007=df[df['year']==2007]
```


```python
Gapminder_2007[Gapminder_2007.life_exp==Gapminder_2007.life_exp.min()]
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
      <th>country</th>
      <th>year</th>
      <th>population</th>
      <th>continent</th>
      <th>life_exp</th>
      <th>gdp_cap</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1463</th>
      <td>Swaziland</td>
      <td>2007</td>
      <td>1133066</td>
      <td>Africa</td>
      <td>39.613</td>
      <td>4513.480643</td>
    </tr>
  </tbody>
</table>
</div>



### Which country had the highest GDP per capita in 2007.


```python
Gapminder_2007['GDP']=Gapminder_2007['gdp_cap']*Gapminder_2007['population']
```

    C:\Users\Mohit\AppData\Local\Temp/ipykernel_12148/164237267.py:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      Gapminder_2007['GDP']=Gapminder_2007['gdp_cap']*Gapminder_2007['population']
    


```python
Gapminder_2007.head()
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
      <th>country</th>
      <th>year</th>
      <th>population</th>
      <th>continent</th>
      <th>life_exp</th>
      <th>gdp_cap</th>
      <th>GDP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>11</th>
      <td>Afghanistan</td>
      <td>2007</td>
      <td>31889923</td>
      <td>Asia</td>
      <td>43.828</td>
      <td>974.580338</td>
      <td>3.107929e+10</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Albania</td>
      <td>2007</td>
      <td>3600523</td>
      <td>Europe</td>
      <td>76.423</td>
      <td>5937.029526</td>
      <td>2.137641e+10</td>
    </tr>
    <tr>
      <th>35</th>
      <td>Algeria</td>
      <td>2007</td>
      <td>33333216</td>
      <td>Africa</td>
      <td>72.301</td>
      <td>6223.367465</td>
      <td>2.074449e+11</td>
    </tr>
    <tr>
      <th>47</th>
      <td>Angola</td>
      <td>2007</td>
      <td>12420476</td>
      <td>Africa</td>
      <td>42.731</td>
      <td>4797.231267</td>
      <td>5.958390e+10</td>
    </tr>
    <tr>
      <th>59</th>
      <td>Argentina</td>
      <td>2007</td>
      <td>40301927</td>
      <td>Americas</td>
      <td>75.320</td>
      <td>12779.379640</td>
      <td>5.150336e+11</td>
    </tr>
  </tbody>
</table>
</div>




```python
Gapminder_2007[Gapminder_2007.GDP==Gapminder_2007.GDP.max()]
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
      <th>country</th>
      <th>year</th>
      <th>population</th>
      <th>continent</th>
      <th>life_exp</th>
      <th>gdp_cap</th>
      <th>GDP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1619</th>
      <td>United States</td>
      <td>2007</td>
      <td>301139947</td>
      <td>Americas</td>
      <td>78.242</td>
      <td>42951.65309</td>
      <td>1.293446e+13</td>
    </tr>
  </tbody>
</table>
</div>



### Is there any change in the trend from 1952 to 2007 in life expectancy?


```python
import seaborn as sns
from matplotlib import rcParams
```


```python
sns.set_style ='whitgrid'
sns.boxplot(y="life_exp", x="year", data=df)
```




    <AxesSubplot:xlabel='year', ylabel='life_exp'>




    
![png](output_29_1.png)
    



```python
rcParams['figure.figsize'] = 15,8
sns.scatterplot(y="life_exp", x="year", data=df)
```




    <AxesSubplot:xlabel='year', ylabel='life_exp'>




    
![png](output_30_1.png)
    


### Which continent has lowest life expectancy in 2007?


```python
Gapminder_2007[Gapminder_2007.life_exp==Gapminder_2007.life_exp.min()]
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
      <th>country</th>
      <th>year</th>
      <th>population</th>
      <th>continent</th>
      <th>life_exp</th>
      <th>gdp_cap</th>
      <th>GDP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1463</th>
      <td>Swaziland</td>
      <td>2007</td>
      <td>1133066</td>
      <td>Africa</td>
      <td>39.613</td>
      <td>4513.480643</td>
      <td>5.114071e+09</td>
    </tr>
  </tbody>
</table>
</div>




```python
x = df.continent
y = df.life_exp
plt.bar(x,y)
```




    <BarContainer object of 1704 artists>




    
![png](output_33_1.png)
    



```python
sns.set_style ='whitgrid'
sns.boxplot(y="life_exp", x="continent", data=df)
```




    <AxesSubplot:xlabel='continent', ylabel='life_exp'>




    
![png](output_34_1.png)
    



```python
gdp_sort.describe()
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
      <th>year</th>
      <th>population</th>
      <th>life_exp</th>
      <th>gdp_cap</th>
      <th>GDP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>1704.00000</td>
      <td>1.704000e+03</td>
      <td>1704.000000</td>
      <td>1704.000000</td>
      <td>1.704000e+03</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>1979.50000</td>
      <td>2.960121e+07</td>
      <td>59.474439</td>
      <td>7215.327081</td>
      <td>1.868096e+11</td>
    </tr>
    <tr>
      <th>std</th>
      <td>17.26533</td>
      <td>1.061579e+08</td>
      <td>12.917107</td>
      <td>9857.454543</td>
      <td>7.140297e+11</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1952.00000</td>
      <td>6.001100e+04</td>
      <td>23.599000</td>
      <td>241.165876</td>
      <td>5.278469e+07</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1965.75000</td>
      <td>2.793664e+06</td>
      <td>48.198000</td>
      <td>1202.060309</td>
      <td>5.895295e+09</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1979.50000</td>
      <td>7.023596e+06</td>
      <td>60.712500</td>
      <td>3531.846988</td>
      <td>2.234330e+10</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1993.25000</td>
      <td>1.958522e+07</td>
      <td>70.845500</td>
      <td>9325.462346</td>
      <td>1.057441e+11</td>
    </tr>
    <tr>
      <th>max</th>
      <td>2007.00000</td>
      <td>1.318683e+09</td>
      <td>82.603000</td>
      <td>113523.132900</td>
      <td>1.293446e+13</td>
    </tr>
  </tbody>
</table>
</div>



### Is there an relationship between GDP_capita and life expectancy?


```python
sns.scatterplot( y = 'life_exp',  x ='gdp_cap',  data=df,hue='continent')
```




    <AxesSubplot:xlabel='gdp_cap', ylabel='life_exp'>




    
![png](output_37_1.png)
    


from plot it seems that countries have higher life expectancy  have higher GDP per capita.However there is no clear trend or relationship.

### Trend of life expectancy in India from 1950 -2007


```python
Gapminder_India=df[df['country']=='India']
```


```python
sns.set_style ='whitgrid'
sns.lineplot(y="life_exp", x="year", data=Gapminder_India)
```




    <AxesSubplot:xlabel='year', ylabel='life_exp'>




    
![png](output_41_1.png)
    



```python
sns.set_style ='whitgrid'
```

### Trend of GDP per capita in India from 1950 -2007


```python
sns.lineplot(y="gdp_cap", x="year", data=Gapminder_India)
```




    <AxesSubplot:xlabel='year', ylabel='gdp_cap'>




    
![png](output_44_1.png)
    


### what is median age of each continent by each  year ?


```python
grp_y_a=df.groupby(['year','continent'])['life_exp'].median()
grp_y_a
```




    year  continent
    1952  Africa       38.8330
          Americas     54.7450
          Asia         44.8690
          Europe       65.9000
          Oceania      69.2550
    1957  Africa       40.5925
          Americas     56.0740
          Asia         48.2840
          Europe       67.6500
          Oceania      70.2950
    1962  Africa       42.6305
          Americas     58.2990
          Asia         49.3250
          Europe       69.5250
          Oceania      71.0850
    1967  Africa       44.6985
          Americas     60.5230
          Asia         53.6550
          Europe       70.6100
          Oceania      71.3100
    1972  Africa       47.0315
          Americas     63.4410
          Asia         56.9500
          Europe       70.8850
          Oceania      71.9100
    1977  Africa       49.2725
          Americas     66.3530
          Asia         60.7650
          Europe       72.3350
          Oceania      72.8550
    1982  Africa       50.7560
          Americas     67.4050
          Asia         63.7390
          Europe       73.4900
          Oceania      74.2900
    1987  Africa       51.6395
          Americas     69.4980
          Asia         66.2950
          Europe       74.8150
          Oceania      75.3200
    1992  Africa       52.4290
          Americas     69.8620
          Asia         68.6900
          Europe       75.4510
          Oceania      76.9450
    1997  Africa       52.7590
          Americas     72.1460
          Asia         70.2650
          Europe       76.1160
          Oceania      78.1900
    2002  Africa       51.2355
          Americas     72.0470
          Asia         71.0280
          Europe       77.5365
          Oceania      79.7400
    2007  Africa       52.9265
          Americas     72.8990
          Asia         72.3960
          Europe       78.6085
          Oceania      80.7195
    Name: life_exp, dtype: float64




```python

```
