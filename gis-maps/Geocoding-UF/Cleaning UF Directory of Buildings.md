

```python
import pandas as pd
import numpy as np

```


```python
df = pd.read_csv('listings-comma-delim.csv')
df.head()
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
      <th>code</th>
      <th>name</th>
      <th>coordinates__latitude</th>
      <th>coordinates__longitude</th>
      <th>address</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>AAF</td>
      <td>Academic Advisement - Farrior Hall</td>
      <td>29.650232</td>
      <td>-82.345639</td>
      <td>100 Fletcher Dr, Gainesville, FL 32611, United...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>AGRL</td>
      <td>Plant Pathology Research Lab 2</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>AND</td>
      <td>Anderson Hall</td>
      <td>29.651568</td>
      <td>-82.341890</td>
      <td>1507 W University Ave, Gainesville, FL 32611, ...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ANS</td>
      <td>Animal Sciences</td>
      <td>29.631197</td>
      <td>-82.351627</td>
      <td>Gainesville, FL 32608, United States</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ANSC</td>
      <td>Animal/Dairy Science Building</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



Issues:
+ Address column includes street address, city, state, and zip. I need to put these values into their own seperate columns.
+ The address column is not uniform. If I split the address by comma, for some entries, I will have 4 entries but not always.
+ There are missing values
+ Although there is extra information, I will leave it because there is no reason to discard it.
+ Also, it seems there are different dtypes in the address column. They all need to be strings.


```python
addr = df['address']
addr.head(10)
```




    0    100 Fletcher Dr, Gainesville, FL 32611, United...
    1                                                  NaN
    2    1507 W University Ave, Gainesville, FL 32611, ...
    3                 Gainesville, FL 32608, United States
    4                                                  NaN
    5    1600 SW Archer Rd, Gainesville, FL 32610, Unit...
    6    1389 Stadium Rd, Gainesville, FL 32611, United...
    7    Elmore Hall for Administrative Services, Gaine...
    8    333 Newell Dr, Gainesville, FL 32611, United S...
    9                                                  NaN
    Name: address, dtype: object




```python
def split_address(x):
    # Some entries in the address column are not strings
    # print(type(x))
    if (type(x) is str):
        arr = x.split(", ")
        #print(arr)
        return arr
    else:
        #print(x)
        return [x]

addr.map(split_address)
```




    0      [100 Fletcher Dr, Gainesville, FL 32611, Unite...
    1                                                  [nan]
    2      [1507 W University Ave, Gainesville, FL 32611,...
    3                 [Gainesville, FL 32608, United States]
    4                                                  [nan]
    5      [1600 SW Archer Rd, Gainesville, FL 32610, Uni...
    6      [1389 Stadium Rd, Gainesville, FL 32611, Unite...
    7      [Elmore Hall for Administrative Services, Gain...
    8      [333 Newell Dr, Gainesville, FL 32611, United ...
    9                                                  [nan]
    10            [Bartram Hall, Gainesville, FL 32603, USA]
    11                [Gainesville, FL 32603, United States]
    12                [Gainesville, FL 32611, United States]
    13        [Bruton-Geer Hall, Gainesville, FL 32603, USA]
    14     [365 Weil Hall, Gainesville, FL 32611, United ...
    15     [919 N Broad St, Brooksville, FL 34601, United...
    16     [1275 Center Dr, Gainesville, FL 32611, United...
    17     [Broward Hall, 680 Broward Dr, Gainesville, FL...
    18                [Gainesville, FL 32603, United States]
    19     [1384 Union Rd, Gainesville, FL 32611, United ...
    20     [2001 S Lincoln Ave, Urbana, IL 61802, United ...
    21                                                 [nan]
    22     [1475 Union Rd, Gainesville, FL 32611, United ...
    23      [Classroom Bldg 105, Gainesville, FL 32603, USA]
    24     [2033 Mowry Rd, Gainesville, FL 32608, United ...
    25                [Gainesville, FL 32611, United States]
    26     [125 Buckman Dr, Gainesville, FL 32611, United...
    27     [1600 SW Archer Rd, Gainesville, FL 32610, Uni...
    28     [687 McCarty Dr, Gainesville, FL 32603, United...
    29                                                 [nan]
                                 ...                        
    117    [1911 SW 34th St, Gainesville, FL 32608, Unite...
    118    [Rinker Hall, 573 Newell Dr, Gainesville, FL 3...
    119                                      [United States]
    120             [Rolfs Hall, Gainesville, FL 32603, USA]
    121               [Gainesville, FL 32611, United States]
    122    [1680 Union Rd, Gainesville, FL 32611, United ...
    123    [1545 W University Ave, University of Florida,...
    124               [Gainesville, FL 32603, United States]
    125    [Diamond Village Commons Bldg, 1402 Diamond Rd...
    126               [Gainesville, FL 32603, United States]
    127    [1478 Union Rd, Gainesville, FL 32611, United ...
    128    [157 Gale Lemerand Dr, Gainesville, FL 32601, ...
    129    [1454, 100 Stuzin Hall Union Rd, Gainesville, ...
    130      [13120 Vonn Rd, Largo, FL 33774, United States]
    131    [4645 NW 8th Ave, Gainesville, FL 32605, Unite...
    132               [Gainesville, FL 32611, United States]
    133    [330 Newell Dr, Gainesville, FL 32611, United ...
    134            [Ustler Hall, Gainesville, FL 32608, USA]
    135    [204 Van Fleet Hall, Gainesville, FL 32611, Un...
    136    [2015 SW 16th Ave, Gainesville, FL 32608, Unit...
    137    [Veterinary Medicine Academic Bldg, Gainesvill...
    138    [1489 Union Rd, Gainesville, FL 32611, United ...
    139    [1001 George Wallace Dr, Gadsden, AL 35903, Un...
    140                                                [nan]
    141                   [Lake Wauburg, Florida 32667, USA]
    142              [Weil Hall, Gainesville, FL 32603, USA]
    143            [Weimer Hall, Gainesville, FL 32603, USA]
    144               [Gainesville, FL 32611, United States]
    145    [Weed Sciences Field Bldg, Gainesville, FL 326...
    146               [Gainesville, FL 32608, United States]
    Name: address, Length: 147, dtype: object



Ideally we want something like this:
+ ['1368 Union Rd', 'Gainesville', 'FL 32611', 'United States']

but in many cases, we get something like this:
+ ['Health Professions', 'Nursing', 'Pharmacy Bldg', '1225 Center Dr', 'Gainesville', 'FL 32603', 'USA']
+ ['Hub', '1765 Stadium Rd', 'Gainesville', 'FL 32603', 'United States']  
+ ['Gainesville', 'FL 32611', 'United States']



```python
# Okay, lets split the address into different lists
street = []
city = []
state = []
zipcode = []

def create_lists(x):
    # Split
    ret_val = split_address(x)

    if(len(ret_val) == 4):
        street.append(ret_val[0])
        city.append(ret_val[1])       

        # Split state and zipcode
        # print(ret_val[2])
        s, z = ret_val[2].split(' ')
        state.append(s)
        zipcode.append(z)

    else:
        street.append("fix!")
        city.append("fix!")
        state.append("fix!")
        zipcode.append("fix!")


addr.map(create_lists)
street_col = pd.Series(street)
city_col = pd.Series(city)
zip_col = pd.Series(zipcode)
state_col = pd.Series(state)
```


```python
# let's make a copy of the original dataframe and append our columns to it
new_df = df

new_df['address'] = street_col
new_df['city'] = city_col
new_df['zip'] = zip_col
new_df['state'] = state_col

new_df.head(20)
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
      <th>code</th>
      <th>name</th>
      <th>coordinates__latitude</th>
      <th>coordinates__longitude</th>
      <th>address</th>
      <th>city</th>
      <th>zip</th>
      <th>state</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>AAF</td>
      <td>Academic Advisement - Farrior Hall</td>
      <td>29.650232</td>
      <td>-82.345639</td>
      <td>100 Fletcher Dr</td>
      <td>Gainesville</td>
      <td>32611</td>
      <td>FL</td>
    </tr>
    <tr>
      <th>1</th>
      <td>AGRL</td>
      <td>Plant Pathology Research Lab 2</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>fix!</td>
      <td>fix!</td>
      <td>fix!</td>
      <td>fix!</td>
    </tr>
    <tr>
      <th>2</th>
      <td>AND</td>
      <td>Anderson Hall</td>
      <td>29.651568</td>
      <td>-82.341890</td>
      <td>1507 W University Ave</td>
      <td>Gainesville</td>
      <td>32611</td>
      <td>FL</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ANS</td>
      <td>Animal Sciences</td>
      <td>29.631197</td>
      <td>-82.351627</td>
      <td>fix!</td>
      <td>fix!</td>
      <td>fix!</td>
      <td>fix!</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ANSC</td>
      <td>Animal/Dairy Science Building</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>fix!</td>
      <td>fix!</td>
      <td>fix!</td>
      <td>fix!</td>
    </tr>
    <tr>
      <th>5</th>
      <td>ARB</td>
      <td>Academic Research - Health Sciences Center</td>
      <td>29.639944</td>
      <td>-82.343777</td>
      <td>1600 SW Archer Rd</td>
      <td>Gainesville</td>
      <td>32610</td>
      <td>FL</td>
    </tr>
    <tr>
      <th>6</th>
      <td>ARCH</td>
      <td>Architecture</td>
      <td>29.647776</td>
      <td>-82.340343</td>
      <td>1389 Stadium Rd</td>
      <td>Gainesville</td>
      <td>32611</td>
      <td>FL</td>
    </tr>
    <tr>
      <th>7</th>
      <td>ASF</td>
      <td>Elmore Hall</td>
      <td>29.643480</td>
      <td>-82.366179</td>
      <td>Elmore Hall for Administrative Services</td>
      <td>Gainesville</td>
      <td>32607</td>
      <td>FL</td>
    </tr>
    <tr>
      <th>8</th>
      <td>AUD</td>
      <td>University Auditorium</td>
      <td>29.649027</td>
      <td>-82.342843</td>
      <td>333 Newell Dr</td>
      <td>Gainesville</td>
      <td>32611</td>
      <td>FL</td>
    </tr>
    <tr>
      <th>9</th>
      <td>AWAX</td>
      <td>Aquatic Weed Annex</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>fix!</td>
      <td>fix!</td>
      <td>fix!</td>
      <td>fix!</td>
    </tr>
    <tr>
      <th>10</th>
      <td>BAR</td>
      <td>Bartram Hall</td>
      <td>29.643920</td>
      <td>-82.344409</td>
      <td>Bartram Hall</td>
      <td>Gainesville</td>
      <td>32603</td>
      <td>FL</td>
    </tr>
    <tr>
      <th>11</th>
      <td>BEC</td>
      <td>Beaty Commons</td>
      <td>29.644151</td>
      <td>-82.340485</td>
      <td>fix!</td>
      <td>fix!</td>
      <td>fix!</td>
      <td>fix!</td>
    </tr>
    <tr>
      <th>12</th>
      <td>BEN</td>
      <td>Benton Hall</td>
      <td>29.643633</td>
      <td>-82.354930</td>
      <td>fix!</td>
      <td>fix!</td>
      <td>fix!</td>
      <td>fix!</td>
    </tr>
    <tr>
      <th>13</th>
      <td>BGH</td>
      <td>Bruton-Geer Hall</td>
      <td>29.649232</td>
      <td>-82.359029</td>
      <td>Bruton-Geer Hall</td>
      <td>Gainesville</td>
      <td>32603</td>
      <td>FL</td>
    </tr>
    <tr>
      <th>14</th>
      <td>BLK</td>
      <td>Black Hall - Environmental Science</td>
      <td>29.648409</td>
      <td>-82.348414</td>
      <td>365 Weil Hall</td>
      <td>Gainesville</td>
      <td>32611</td>
      <td>FL</td>
    </tr>
    <tr>
      <th>15</th>
      <td>BME</td>
      <td>Broad Biomedical Engineering Building</td>
      <td>28.566394</td>
      <td>-82.377570</td>
      <td>919 N Broad St</td>
      <td>Brooksville</td>
      <td>34601</td>
      <td>FL</td>
    </tr>
    <tr>
      <th>16</th>
      <td>BMS</td>
      <td>Biomedical Sciences</td>
      <td>29.640633</td>
      <td>-82.345583</td>
      <td>1275 Center Dr</td>
      <td>Gainesville</td>
      <td>32611</td>
      <td>FL</td>
    </tr>
    <tr>
      <th>17</th>
      <td>BRO</td>
      <td>Broward Hall</td>
      <td>29.646535</td>
      <td>-82.342071</td>
      <td>fix!</td>
      <td>fix!</td>
      <td>fix!</td>
      <td>fix!</td>
    </tr>
    <tr>
      <th>18</th>
      <td>BRT</td>
      <td>Bryant Space Science Center</td>
      <td>29.648887</td>
      <td>-82.345749</td>
      <td>fix!</td>
      <td>fix!</td>
      <td>fix!</td>
      <td>fix!</td>
    </tr>
    <tr>
      <th>19</th>
      <td>BRY</td>
      <td>Bryan Hall</td>
      <td>29.651312</td>
      <td>-82.340238</td>
      <td>1384 Union Rd</td>
      <td>Gainesville</td>
      <td>32611</td>
      <td>FL</td>
    </tr>
  </tbody>
</table>
</div>



Even though we have properly split and asigned the different address components, there are still many fields that need to be fixed, and I will have no choice but to do that manually. All that is left to do is export this file to a csv.


```python
new_df.to_csv("uf-directory-of-listings.csv")
```
