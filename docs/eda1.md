---
title: EDA
notebook: eda1.ipynb
nav_include: 1
---


{:.no_toc}
*  
{: toc}


# EDA



```python
# prevent vertical scrolling windows
# also, this needs to be the first code cell
# or else it might not work properly
```




```python
%%javascript
IPython.OutputArea.prototype._should_scroll = function(lines) {
    return false;
}
```



    <IPython.core.display.Javascript object>




```python
from graphviz import Source
from IPython.display import display
from IPython.display import Image
import matplotlib
import matplotlib.pyplot as plt
plt.rcParams.update({'figure.max_open_warning': 0})
import numpy as np
import pandas as pd
import pydot
import seaborn as sns
import datetime
%matplotlib inline
sns.set()
sns.set_context('poster')
sns.set_style('dark')
```




```python
start = datetime.datetime.time(datetime.datetime.now())
```




```python
df = pd.read_csv('../data/merged/eda_2010_noindexcol.csv')
```




```python
df.info()
```


    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 94 entries, 0 to 93
    Columns: 191 entries, year to murder_per_100_k
    dtypes: float64(173), int64(17), object(1)
    memory usage: 140.3+ KB




```python
df.describe()
```





<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>total_population</th>
      <th>gender_male</th>
      <th>gender_female</th>
      <th>age_under_5_years</th>
      <th>age_5_to_17_years</th>
      <th>age_18_to_24_years</th>
      <th>age_25_to_34_years</th>
      <th>age_35_to_44_years</th>
      <th>age_45_to_54_years</th>
      <th>...</th>
      <th>1_01_or_more_occupants_per_room</th>
      <th>monthly_owner_costs_as_percentage_of_household_income_less_than_30_percent</th>
      <th>monthly_owner_costs_as_percentage_of_household_income_30_percent_or_more</th>
      <th>house_median_value_(dollars)</th>
      <th>house_median_selected_monthly_owner_costs_with_a_mortgage_(dollars)</th>
      <th>house_median_selected_monthly_owner_costs_without_a_mortgage_(dollars)</th>
      <th>gross_rent_as_percentage_of_household_income_less_than_30_percent</th>
      <th>gross_rent_as_percentage_of_household_income_30_percent_or_more</th>
      <th>median_gross_rent_(dollars)</th>
      <th>murder_per_100_k</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>94.0</td>
      <td>9.400000e+01</td>
      <td>94.00000</td>
      <td>94.00000</td>
      <td>94.000000</td>
      <td>94.000000</td>
      <td>94.000000</td>
      <td>94.000000</td>
      <td>94.000000</td>
      <td>94.000000</td>
      <td>...</td>
      <td>94.000000</td>
      <td>94.000000</td>
      <td>94.000000</td>
      <td>94.000000</td>
      <td>94.000000</td>
      <td>94.000000</td>
      <td>94.000000</td>
      <td>94.000000</td>
      <td>94.000000</td>
      <td>94.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>2010.0</td>
      <td>1.938882e+06</td>
      <td>49.01383</td>
      <td>50.98617</td>
      <td>6.635106</td>
      <td>17.737234</td>
      <td>9.998936</td>
      <td>13.312766</td>
      <td>13.290426</td>
      <td>14.494681</td>
      <td>...</td>
      <td>3.145745</td>
      <td>62.535106</td>
      <td>37.464894</td>
      <td>207994.680851</td>
      <td>1567.510638</td>
      <td>474.659574</td>
      <td>47.091489</td>
      <td>52.908511</td>
      <td>863.808511</td>
      <td>4.962766</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.0</td>
      <td>2.580306e+06</td>
      <td>0.70993</td>
      <td>0.70993</td>
      <td>1.075105</td>
      <td>2.025323</td>
      <td>1.279742</td>
      <td>1.582786</td>
      <td>1.000760</td>
      <td>1.230383</td>
      <td>...</td>
      <td>2.636700</td>
      <td>7.357605</td>
      <td>7.357605</td>
      <td>106569.572779</td>
      <td>413.938901</td>
      <td>121.673594</td>
      <td>3.919174</td>
      <td>3.919174</td>
      <td>182.395781</td>
      <td>2.774887</td>
    </tr>
    <tr>
      <th>min</th>
      <td>2010.0</td>
      <td>4.945270e+05</td>
      <td>47.70000</td>
      <td>48.30000</td>
      <td>4.700000</td>
      <td>13.200000</td>
      <td>6.500000</td>
      <td>9.000000</td>
      <td>10.600000</td>
      <td>8.400000</td>
      <td>...</td>
      <td>0.600000</td>
      <td>44.300000</td>
      <td>25.300000</td>
      <td>80400.000000</td>
      <td>1029.000000</td>
      <td>320.000000</td>
      <td>36.600000</td>
      <td>43.100000</td>
      <td>588.000000</td>
      <td>0.900000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>2010.0</td>
      <td>6.685388e+05</td>
      <td>48.50000</td>
      <td>50.60000</td>
      <td>5.925000</td>
      <td>16.600000</td>
      <td>9.200000</td>
      <td>12.100000</td>
      <td>12.800000</td>
      <td>14.000000</td>
      <td>...</td>
      <td>1.600000</td>
      <td>57.375000</td>
      <td>31.150000</td>
      <td>142150.000000</td>
      <td>1286.500000</td>
      <td>395.500000</td>
      <td>44.650000</td>
      <td>50.225000</td>
      <td>734.250000</td>
      <td>3.400000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>2010.0</td>
      <td>9.362965e+05</td>
      <td>48.90000</td>
      <td>51.10000</td>
      <td>6.500000</td>
      <td>17.300000</td>
      <td>9.900000</td>
      <td>13.400000</td>
      <td>13.250000</td>
      <td>14.700000</td>
      <td>...</td>
      <td>2.250000</td>
      <td>64.100000</td>
      <td>35.900000</td>
      <td>173100.000000</td>
      <td>1470.500000</td>
      <td>449.000000</td>
      <td>47.750000</td>
      <td>52.250000</td>
      <td>826.500000</td>
      <td>4.700000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>2010.0</td>
      <td>2.118842e+06</td>
      <td>49.40000</td>
      <td>51.50000</td>
      <td>7.100000</td>
      <td>18.575000</td>
      <td>10.700000</td>
      <td>14.475000</td>
      <td>13.800000</td>
      <td>15.200000</td>
      <td>...</td>
      <td>3.725000</td>
      <td>68.850000</td>
      <td>42.625000</td>
      <td>225575.000000</td>
      <td>1678.500000</td>
      <td>524.750000</td>
      <td>49.775000</td>
      <td>55.350000</td>
      <td>917.500000</td>
      <td>6.175000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>2010.0</td>
      <td>1.891998e+07</td>
      <td>51.70000</td>
      <td>52.30000</td>
      <td>11.300000</td>
      <td>25.100000</td>
      <td>15.800000</td>
      <td>17.100000</td>
      <td>16.200000</td>
      <td>16.600000</td>
      <td>...</td>
      <td>14.200000</td>
      <td>74.700000</td>
      <td>55.700000</td>
      <td>631400.000000</td>
      <td>2974.000000</td>
      <td>951.000000</td>
      <td>56.900000</td>
      <td>63.400000</td>
      <td>1412.000000</td>
      <td>20.800000</td>
    </tr>
  </tbody>
</table>
<p>8 rows × 190 columns</p>
</div>





```python
df.head()
```





<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>MSA</th>
      <th>total_population</th>
      <th>gender_male</th>
      <th>gender_female</th>
      <th>age_under_5_years</th>
      <th>age_5_to_17_years</th>
      <th>age_18_to_24_years</th>
      <th>age_25_to_34_years</th>
      <th>age_35_to_44_years</th>
      <th>...</th>
      <th>1_01_or_more_occupants_per_room</th>
      <th>monthly_owner_costs_as_percentage_of_household_income_less_than_30_percent</th>
      <th>monthly_owner_costs_as_percentage_of_household_income_30_percent_or_more</th>
      <th>house_median_value_(dollars)</th>
      <th>house_median_selected_monthly_owner_costs_with_a_mortgage_(dollars)</th>
      <th>house_median_selected_monthly_owner_costs_without_a_mortgage_(dollars)</th>
      <th>gross_rent_as_percentage_of_household_income_less_than_30_percent</th>
      <th>gross_rent_as_percentage_of_household_income_30_percent_or_more</th>
      <th>median_gross_rent_(dollars)</th>
      <th>murder_per_100_k</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010</td>
      <td>Akron, OH</td>
      <td>702951</td>
      <td>48.6</td>
      <td>51.4</td>
      <td>5.6</td>
      <td>16.7</td>
      <td>10.6</td>
      <td>11.7</td>
      <td>12.5</td>
      <td>...</td>
      <td>1.0</td>
      <td>69.3</td>
      <td>30.7</td>
      <td>145000</td>
      <td>1279</td>
      <td>450</td>
      <td>48.0</td>
      <td>52.0</td>
      <td>702</td>
      <td>3.7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2010</td>
      <td>Albany-Schenectady-Troy, NY</td>
      <td>870832</td>
      <td>48.9</td>
      <td>51.1</td>
      <td>5.4</td>
      <td>15.9</td>
      <td>11.1</td>
      <td>12.1</td>
      <td>13.1</td>
      <td>...</td>
      <td>1.5</td>
      <td>69.7</td>
      <td>30.3</td>
      <td>199000</td>
      <td>1605</td>
      <td>558</td>
      <td>49.8</td>
      <td>50.2</td>
      <td>846</td>
      <td>1.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2010</td>
      <td>Albuquerque, NM</td>
      <td>892014</td>
      <td>49.0</td>
      <td>51.0</td>
      <td>6.8</td>
      <td>17.6</td>
      <td>9.8</td>
      <td>13.8</td>
      <td>12.9</td>
      <td>...</td>
      <td>2.8</td>
      <td>63.7</td>
      <td>36.3</td>
      <td>183300</td>
      <td>1305</td>
      <td>358</td>
      <td>50.9</td>
      <td>49.1</td>
      <td>748</td>
      <td>5.8</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2010</td>
      <td>Allentown-Bethlehem-Easton, PA-NJ</td>
      <td>822141</td>
      <td>48.8</td>
      <td>51.2</td>
      <td>5.7</td>
      <td>17.1</td>
      <td>8.8</td>
      <td>11.2</td>
      <td>13.4</td>
      <td>...</td>
      <td>1.2</td>
      <td>63.2</td>
      <td>36.8</td>
      <td>218700</td>
      <td>1653</td>
      <td>555</td>
      <td>44.6</td>
      <td>55.4</td>
      <td>848</td>
      <td>3.5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2010</td>
      <td>Atlanta-Sandy Springs-Marietta, GA</td>
      <td>5288302</td>
      <td>48.7</td>
      <td>51.3</td>
      <td>7.2</td>
      <td>19.3</td>
      <td>9.2</td>
      <td>14.5</td>
      <td>15.6</td>
      <td>...</td>
      <td>2.8</td>
      <td>60.7</td>
      <td>39.3</td>
      <td>175900</td>
      <td>1544</td>
      <td>448</td>
      <td>46.3</td>
      <td>53.7</td>
      <td>910</td>
      <td>6.1</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 191 columns</p>
</div>





```python
with sns.axes_style("whitegrid"):
    plt.hist(df.murder_per_100_k.values, bins=50)
    plt.axvline(df.murder_per_100_k.mean(), 0, 0.75, color='r', label='Mean')
    plt.xlabel("Murders Per 100k")
    plt.ylabel("Counts")
    plt.title("Murders Per 100k Histogram")
    plt.legend()
```



![png](eda1_files/eda1_9_0.png)




```python
def plot_column(x, y, title, i):    
    params = np.polyfit(x, y, 2)
    xp = np.linspace(x.min(), x.max(), 20)
    yp = np.polyval(params, xp)
    plt.figure(i)
    plt.plot(xp, yp, 'k', alpha=0.8, linewidth=1)
    plt.plot(x, y, 'o', markersize=8, alpha=0.5)
    sig = np.std(y - np.polyval(params, x))
    plt.fill_between(xp, yp - sig, yp + sig, color='k', alpha=0.2)
    plt.title(title);
```




```python
def plot_columns(df):
    y = df.murder_per_100_k
    for i in range(0, len(df.columns)):
        x = df.iloc[:, i]
        title = df.columns[i]
        plot_column(x, y, title, i)
```




```python
# drop column 145 because it contains blanks
df = df.drop(['poverty_married-couple_family_with_related_children_under_5_years_only'], axis=1)
```




```python
# scatter plot all features (except for year and MSA)
plot_columns(df.iloc[:, 2:])
```



![png](eda1_files/eda1_13_0.png)



![png](eda1_files/eda1_13_1.png)



![png](eda1_files/eda1_13_2.png)



![png](eda1_files/eda1_13_3.png)



![png](eda1_files/eda1_13_4.png)



![png](eda1_files/eda1_13_5.png)



![png](eda1_files/eda1_13_6.png)



![png](eda1_files/eda1_13_7.png)



![png](eda1_files/eda1_13_8.png)



![png](eda1_files/eda1_13_9.png)



![png](eda1_files/eda1_13_10.png)



![png](eda1_files/eda1_13_11.png)



![png](eda1_files/eda1_13_12.png)



![png](eda1_files/eda1_13_13.png)



![png](eda1_files/eda1_13_14.png)



![png](eda1_files/eda1_13_15.png)



![png](eda1_files/eda1_13_16.png)



![png](eda1_files/eda1_13_17.png)



![png](eda1_files/eda1_13_18.png)



![png](eda1_files/eda1_13_19.png)



![png](eda1_files/eda1_13_20.png)



![png](eda1_files/eda1_13_21.png)



![png](eda1_files/eda1_13_22.png)



![png](eda1_files/eda1_13_23.png)



![png](eda1_files/eda1_13_24.png)



![png](eda1_files/eda1_13_25.png)



![png](eda1_files/eda1_13_26.png)



![png](eda1_files/eda1_13_27.png)



![png](eda1_files/eda1_13_28.png)



![png](eda1_files/eda1_13_29.png)



![png](eda1_files/eda1_13_30.png)



![png](eda1_files/eda1_13_31.png)



![png](eda1_files/eda1_13_32.png)



![png](eda1_files/eda1_13_33.png)



![png](eda1_files/eda1_13_34.png)



![png](eda1_files/eda1_13_35.png)



![png](eda1_files/eda1_13_36.png)



![png](eda1_files/eda1_13_37.png)



![png](eda1_files/eda1_13_38.png)



![png](eda1_files/eda1_13_39.png)



![png](eda1_files/eda1_13_40.png)



![png](eda1_files/eda1_13_41.png)



![png](eda1_files/eda1_13_42.png)



![png](eda1_files/eda1_13_43.png)



![png](eda1_files/eda1_13_44.png)



![png](eda1_files/eda1_13_45.png)



![png](eda1_files/eda1_13_46.png)



![png](eda1_files/eda1_13_47.png)



![png](eda1_files/eda1_13_48.png)



![png](eda1_files/eda1_13_49.png)



![png](eda1_files/eda1_13_50.png)



![png](eda1_files/eda1_13_51.png)



![png](eda1_files/eda1_13_52.png)



![png](eda1_files/eda1_13_53.png)



![png](eda1_files/eda1_13_54.png)



![png](eda1_files/eda1_13_55.png)



![png](eda1_files/eda1_13_56.png)



![png](eda1_files/eda1_13_57.png)



![png](eda1_files/eda1_13_58.png)



![png](eda1_files/eda1_13_59.png)



![png](eda1_files/eda1_13_60.png)



![png](eda1_files/eda1_13_61.png)



![png](eda1_files/eda1_13_62.png)



![png](eda1_files/eda1_13_63.png)



![png](eda1_files/eda1_13_64.png)



![png](eda1_files/eda1_13_65.png)



![png](eda1_files/eda1_13_66.png)



![png](eda1_files/eda1_13_67.png)



![png](eda1_files/eda1_13_68.png)



![png](eda1_files/eda1_13_69.png)



![png](eda1_files/eda1_13_70.png)



![png](eda1_files/eda1_13_71.png)



![png](eda1_files/eda1_13_72.png)



![png](eda1_files/eda1_13_73.png)



![png](eda1_files/eda1_13_74.png)



![png](eda1_files/eda1_13_75.png)



![png](eda1_files/eda1_13_76.png)



![png](eda1_files/eda1_13_77.png)



![png](eda1_files/eda1_13_78.png)



![png](eda1_files/eda1_13_79.png)



![png](eda1_files/eda1_13_80.png)



![png](eda1_files/eda1_13_81.png)



![png](eda1_files/eda1_13_82.png)



![png](eda1_files/eda1_13_83.png)



![png](eda1_files/eda1_13_84.png)



![png](eda1_files/eda1_13_85.png)



![png](eda1_files/eda1_13_86.png)



![png](eda1_files/eda1_13_87.png)



![png](eda1_files/eda1_13_88.png)



![png](eda1_files/eda1_13_89.png)



![png](eda1_files/eda1_13_90.png)



![png](eda1_files/eda1_13_91.png)



![png](eda1_files/eda1_13_92.png)



![png](eda1_files/eda1_13_93.png)



![png](eda1_files/eda1_13_94.png)



![png](eda1_files/eda1_13_95.png)



![png](eda1_files/eda1_13_96.png)



![png](eda1_files/eda1_13_97.png)



![png](eda1_files/eda1_13_98.png)



![png](eda1_files/eda1_13_99.png)



![png](eda1_files/eda1_13_100.png)



![png](eda1_files/eda1_13_101.png)



![png](eda1_files/eda1_13_102.png)



![png](eda1_files/eda1_13_103.png)



![png](eda1_files/eda1_13_104.png)



![png](eda1_files/eda1_13_105.png)



![png](eda1_files/eda1_13_106.png)



![png](eda1_files/eda1_13_107.png)



![png](eda1_files/eda1_13_108.png)



![png](eda1_files/eda1_13_109.png)



![png](eda1_files/eda1_13_110.png)



![png](eda1_files/eda1_13_111.png)



![png](eda1_files/eda1_13_112.png)



![png](eda1_files/eda1_13_113.png)



![png](eda1_files/eda1_13_114.png)



![png](eda1_files/eda1_13_115.png)



![png](eda1_files/eda1_13_116.png)



![png](eda1_files/eda1_13_117.png)



![png](eda1_files/eda1_13_118.png)



![png](eda1_files/eda1_13_119.png)



![png](eda1_files/eda1_13_120.png)



![png](eda1_files/eda1_13_121.png)



![png](eda1_files/eda1_13_122.png)



![png](eda1_files/eda1_13_123.png)



![png](eda1_files/eda1_13_124.png)



![png](eda1_files/eda1_13_125.png)



![png](eda1_files/eda1_13_126.png)



![png](eda1_files/eda1_13_127.png)



![png](eda1_files/eda1_13_128.png)



![png](eda1_files/eda1_13_129.png)



![png](eda1_files/eda1_13_130.png)



![png](eda1_files/eda1_13_131.png)



![png](eda1_files/eda1_13_132.png)



![png](eda1_files/eda1_13_133.png)



![png](eda1_files/eda1_13_134.png)



![png](eda1_files/eda1_13_135.png)



![png](eda1_files/eda1_13_136.png)



![png](eda1_files/eda1_13_137.png)



![png](eda1_files/eda1_13_138.png)



![png](eda1_files/eda1_13_139.png)



![png](eda1_files/eda1_13_140.png)



![png](eda1_files/eda1_13_141.png)



![png](eda1_files/eda1_13_142.png)



![png](eda1_files/eda1_13_143.png)



![png](eda1_files/eda1_13_144.png)



![png](eda1_files/eda1_13_145.png)



![png](eda1_files/eda1_13_146.png)



![png](eda1_files/eda1_13_147.png)



![png](eda1_files/eda1_13_148.png)



![png](eda1_files/eda1_13_149.png)



![png](eda1_files/eda1_13_150.png)



![png](eda1_files/eda1_13_151.png)



![png](eda1_files/eda1_13_152.png)



![png](eda1_files/eda1_13_153.png)



![png](eda1_files/eda1_13_154.png)



![png](eda1_files/eda1_13_155.png)



![png](eda1_files/eda1_13_156.png)



![png](eda1_files/eda1_13_157.png)



![png](eda1_files/eda1_13_158.png)



![png](eda1_files/eda1_13_159.png)



![png](eda1_files/eda1_13_160.png)



![png](eda1_files/eda1_13_161.png)



![png](eda1_files/eda1_13_162.png)



![png](eda1_files/eda1_13_163.png)



![png](eda1_files/eda1_13_164.png)



![png](eda1_files/eda1_13_165.png)



![png](eda1_files/eda1_13_166.png)



![png](eda1_files/eda1_13_167.png)



![png](eda1_files/eda1_13_168.png)



![png](eda1_files/eda1_13_169.png)



![png](eda1_files/eda1_13_170.png)



![png](eda1_files/eda1_13_171.png)



![png](eda1_files/eda1_13_172.png)



![png](eda1_files/eda1_13_173.png)



![png](eda1_files/eda1_13_174.png)



![png](eda1_files/eda1_13_175.png)



![png](eda1_files/eda1_13_176.png)



![png](eda1_files/eda1_13_177.png)



![png](eda1_files/eda1_13_178.png)



![png](eda1_files/eda1_13_179.png)



![png](eda1_files/eda1_13_180.png)



![png](eda1_files/eda1_13_181.png)



![png](eda1_files/eda1_13_182.png)



![png](eda1_files/eda1_13_183.png)



![png](eda1_files/eda1_13_184.png)



![png](eda1_files/eda1_13_185.png)



![png](eda1_files/eda1_13_186.png)



![png](eda1_files/eda1_13_187.png)




```python
relevant_cols = ['family_households_married-couple_family',
                 'family_household_married_couple_family_with_own_children_under_18_years',
                 'family_households_female_householder_no_husband_present',
                 'family_households_female_householder_no_husband_present_with_own_children_under_18',
                 'now_married_except_separated',
                 'less_than_high_school_diploma',
                 'high_school_graduate_or_higher',
                 'unmarried_portion_of_women_15_to_50_years_who_had_a_birth_in_past_12_months',
                 'civilian_noninst_population_18_to_64_years_with_a_disability',
                 'civilian_noninst_population_65_years_and_older_with_a_disability',
                 'industry_transportation_and_warehousing_and_utilities',
                 'median_household_income_(dollars)',
                 'households_with_supplemental_security_income',
                 'households_with_food_stamp_snap_benefits',
                 'median_family_income_(dollars)',
                 'percentage_married-couple_family',
                 'percentage_female_householder_no_husband_present_family',
                 'poverty_all_families',
                 'poverty_all_families_with_related_children_under_18_years',
                 'poverty_all_families_with_related_children_under_18_years_with_related_children_under_5_years_only',
                 'poverty_all_people',
                 'poverty_65_years_and_over',
                 'no_telephone_service_available',
                 'house_median_value_(dollars)',
                 'murder_per_100_k']
```




```python
plot_columns(df[relevant_cols])
```



![png](eda1_files/eda1_15_0.png)



![png](eda1_files/eda1_15_1.png)



![png](eda1_files/eda1_15_2.png)



![png](eda1_files/eda1_15_3.png)



![png](eda1_files/eda1_15_4.png)



![png](eda1_files/eda1_15_5.png)



![png](eda1_files/eda1_15_6.png)



![png](eda1_files/eda1_15_7.png)



![png](eda1_files/eda1_15_8.png)



![png](eda1_files/eda1_15_9.png)



![png](eda1_files/eda1_15_10.png)



![png](eda1_files/eda1_15_11.png)



![png](eda1_files/eda1_15_12.png)



![png](eda1_files/eda1_15_13.png)



![png](eda1_files/eda1_15_14.png)



![png](eda1_files/eda1_15_15.png)



![png](eda1_files/eda1_15_16.png)



![png](eda1_files/eda1_15_17.png)



![png](eda1_files/eda1_15_18.png)



![png](eda1_files/eda1_15_19.png)



![png](eda1_files/eda1_15_20.png)



![png](eda1_files/eda1_15_21.png)



![png](eda1_files/eda1_15_22.png)



![png](eda1_files/eda1_15_23.png)



![png](eda1_files/eda1_15_24.png)




```python
def print_runtime():
    hours = int(str(end)[0:2])-int(str(start)[0:2])
    minutes = int(str(end)[3:5])-int(str(start)[3:5])
    seconds = int(str(end)[6:8])-int(str(start)[6:8])
    if hours < 0:
        hours = hours + 24
    if minutes < 0:
        minutes = minutes + 60
        hours = hours - 1
    if seconds < 0:
        seconds = seconds + 60
        minutes = minutes - 1
    print(hours, "hrs", minutes, "mins", seconds, "secs")
```




```python
end = datetime.datetime.time(datetime.datetime.now())
```




```python
print_runtime()
```


    0 hrs 4 mins 58 secs

