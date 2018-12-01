

```python
import pandas as pd
import numpy as np
```

### Dropping unnecessary fields


```python
# Import the csv file and see the top values
df = pd.read_csv('datasets/BL-Flickr-Images-Book.csv')
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
      <th>Identifier</th>
      <th>Edition Statement</th>
      <th>Place of Publication</th>
      <th>Date of Publication</th>
      <th>Publisher</th>
      <th>Title</th>
      <th>Author</th>
      <th>Contributors</th>
      <th>Corporate Author</th>
      <th>Corporate Contributors</th>
      <th>Former owner</th>
      <th>Engraver</th>
      <th>Issuance type</th>
      <th>Flickr URL</th>
      <th>Shelfmarks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>206</td>
      <td>NaN</td>
      <td>London</td>
      <td>1879 [1878]</td>
      <td>S. Tinsley &amp; Co.</td>
      <td>Walter Forbes. [A novel.] By A. A</td>
      <td>A. A.</td>
      <td>FORBES, Walter.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>monographic</td>
      <td>http://www.flickr.com/photos/britishlibrary/ta...</td>
      <td>British Library HMNTS 12641.b.30.</td>
    </tr>
    <tr>
      <th>1</th>
      <td>216</td>
      <td>NaN</td>
      <td>London; Virtue &amp; Yorston</td>
      <td>1868</td>
      <td>Virtue &amp; Co.</td>
      <td>All for Greed. [A novel. The dedication signed...</td>
      <td>A., A. A.</td>
      <td>BLAZE DE BURY, Marie Pauline Rose - Baroness</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>monographic</td>
      <td>http://www.flickr.com/photos/britishlibrary/ta...</td>
      <td>British Library HMNTS 12626.cc.2.</td>
    </tr>
    <tr>
      <th>2</th>
      <td>218</td>
      <td>NaN</td>
      <td>London</td>
      <td>1869</td>
      <td>Bradbury, Evans &amp; Co.</td>
      <td>Love the Avenger. By the author of “All for Gr...</td>
      <td>A., A. A.</td>
      <td>BLAZE DE BURY, Marie Pauline Rose - Baroness</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>monographic</td>
      <td>http://www.flickr.com/photos/britishlibrary/ta...</td>
      <td>British Library HMNTS 12625.dd.1.</td>
    </tr>
    <tr>
      <th>3</th>
      <td>472</td>
      <td>NaN</td>
      <td>London</td>
      <td>1851</td>
      <td>James Darling</td>
      <td>Welsh Sketches, chiefly ecclesiastical, to the...</td>
      <td>A., E. S.</td>
      <td>Appleyard, Ernest Silvanus.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>monographic</td>
      <td>http://www.flickr.com/photos/britishlibrary/ta...</td>
      <td>British Library HMNTS 10369.bbb.15.</td>
    </tr>
    <tr>
      <th>4</th>
      <td>480</td>
      <td>A new edition, revised, etc.</td>
      <td>London</td>
      <td>1857</td>
      <td>Wertheim &amp; Macintosh</td>
      <td>[The World in which I live, and my place in it...</td>
      <td>A., E. S.</td>
      <td>BROOME, John Henry.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>monographic</td>
      <td>http://www.flickr.com/photos/britishlibrary/ta...</td>
      <td>British Library HMNTS 9007.d.28.</td>
    </tr>
  </tbody>
</table>
</div>



 In this scenario, we want data that is descriptive of the books themselves. Fields such as 'Corporate Author' and 'Former Owner' are not really relevant to the book or its contents so we will drop them. In reality, determing which fields are important will depend on what type of data/ insights you are trying to find from the data, and how much of the data for the field is present.


```python
to_drop = ['Edition Statement',
           'Corporate Author',
           'Corporate Contributors',
           'Former owner',
           'Engraver',
           'Contributors',
           'Issuance type',
           'Shelfmarks']

# inplace=True tells Pandas to apply the drop to this dataframe instead of creating a new dataframe
#df.drop(to_drop, inplace=True, axis=1)
df.drop(columns=to_drop, inplace=True)
```


```python
# Inspect the new df
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
      <th>Identifier</th>
      <th>Place of Publication</th>
      <th>Date of Publication</th>
      <th>Publisher</th>
      <th>Title</th>
      <th>Author</th>
      <th>Flickr URL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>206</td>
      <td>London</td>
      <td>1879 [1878]</td>
      <td>S. Tinsley &amp; Co.</td>
      <td>Walter Forbes. [A novel.] By A. A</td>
      <td>A. A.</td>
      <td>http://www.flickr.com/photos/britishlibrary/ta...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>216</td>
      <td>London; Virtue &amp; Yorston</td>
      <td>1868</td>
      <td>Virtue &amp; Co.</td>
      <td>All for Greed. [A novel. The dedication signed...</td>
      <td>A., A. A.</td>
      <td>http://www.flickr.com/photos/britishlibrary/ta...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>218</td>
      <td>London</td>
      <td>1869</td>
      <td>Bradbury, Evans &amp; Co.</td>
      <td>Love the Avenger. By the author of “All for Gr...</td>
      <td>A., A. A.</td>
      <td>http://www.flickr.com/photos/britishlibrary/ta...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>472</td>
      <td>London</td>
      <td>1851</td>
      <td>James Darling</td>
      <td>Welsh Sketches, chiefly ecclesiastical, to the...</td>
      <td>A., E. S.</td>
      <td>http://www.flickr.com/photos/britishlibrary/ta...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>480</td>
      <td>London</td>
      <td>1857</td>
      <td>Wertheim &amp; Macintosh</td>
      <td>[The World in which I live, and my place in it...</td>
      <td>A., E. S.</td>
      <td>http://www.flickr.com/photos/britishlibrary/ta...</td>
    </tr>
  </tbody>
</table>
</div>



### Changing the Index of a Dataframe

Sometimes, we want to use a different index for our dataframe as opposed to the default 0-based index.


```python
# Indexes should always be unique for better performance
df['Identifier'].is_unique
True
```




    True




```python
# Set the Index to the Book Identifier number
df = df.set_index('Identifier')
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
      <th>Place of Publication</th>
      <th>Date of Publication</th>
      <th>Publisher</th>
      <th>Title</th>
      <th>Author</th>
      <th>Flickr URL</th>
    </tr>
    <tr>
      <th>Identifier</th>
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
      <th>206</th>
      <td>London</td>
      <td>1879 [1878]</td>
      <td>S. Tinsley &amp; Co.</td>
      <td>Walter Forbes. [A novel.] By A. A</td>
      <td>A. A.</td>
      <td>http://www.flickr.com/photos/britishlibrary/ta...</td>
    </tr>
    <tr>
      <th>216</th>
      <td>London; Virtue &amp; Yorston</td>
      <td>1868</td>
      <td>Virtue &amp; Co.</td>
      <td>All for Greed. [A novel. The dedication signed...</td>
      <td>A., A. A.</td>
      <td>http://www.flickr.com/photos/britishlibrary/ta...</td>
    </tr>
    <tr>
      <th>218</th>
      <td>London</td>
      <td>1869</td>
      <td>Bradbury, Evans &amp; Co.</td>
      <td>Love the Avenger. By the author of “All for Gr...</td>
      <td>A., A. A.</td>
      <td>http://www.flickr.com/photos/britishlibrary/ta...</td>
    </tr>
    <tr>
      <th>472</th>
      <td>London</td>
      <td>1851</td>
      <td>James Darling</td>
      <td>Welsh Sketches, chiefly ecclesiastical, to the...</td>
      <td>A., E. S.</td>
      <td>http://www.flickr.com/photos/britishlibrary/ta...</td>
    </tr>
    <tr>
      <th>480</th>
      <td>London</td>
      <td>1857</td>
      <td>Wertheim &amp; Macintosh</td>
      <td>[The World in which I live, and my place in it...</td>
      <td>A., E. S.</td>
      <td>http://www.flickr.com/photos/britishlibrary/ta...</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Access a book by its new index using loc.
df.loc[206]
```




    Place of Publication                                               London
    Date of Publication                                           1879 [1878]
    Publisher                                                S. Tinsley & Co.
    Title                                   Walter Forbes. [A novel.] By A. A
    Author                                                              A. A.
    Flickr URL              http://www.flickr.com/photos/britishlibrary/ta...
    Name: 206, dtype: object




```python
# To access a book using its 'position', use iloc.
df.iloc[0]
```




    Place of Publication                                               London
    Date of Publication                                           1879 [1878]
    Publisher                                                S. Tinsley & Co.
    Title                                   Walter Forbes. [A novel.] By A. A
    Author                                                              A. A.
    Flickr URL              http://www.flickr.com/photos/britishlibrary/ta...
    Name: 206, dtype: object



### Tidying Up Data

Now, it is time to ensure that data in each field has a consistent format.

To do this, it is important to understand dtypes (or data types) in Pandas. dtypes are things like int, float, datetime, and object. Not only does each entry in a column have a dtype but the column that contains them has a dtype as well. Typically, we would like to have the same dtype across all entries in a column.

Read more on [dtypes](http://pandas.pydata.org/pandas-docs/stable/basics.html#dtypes).


```python
# Note: there is no str dtype in pandas. This is simply an object dtype in Pandas
df.get_dtype_counts()
```




    object    6
    dtype: int64



One field where it makes sense to enforce a numeric value is the date of publication so that we can do calculations down the road:


```python
df.loc[1905:, 'Date of Publication'].head(10)
```




    Identifier
    1905           1888
    1929    1839, 38-54
    2836           1897
    2854           1865
    2956        1860-63
    2957           1873
    3017           1866
    3131           1899
    4598           1814
    4884           1820
    Name: Date of Publication, dtype: object



A particular book can have only one date of publication. Therefore, we need to do the following:

+ Remove the extra dates in square brackets, wherever present: 1879 [1878]  
+ Convert date ranges to their “start date”, wherever present: 1860-63; 1839, 38-54
+ Completely remove the dates we are not certain about and replace them with NumPy’s NaN: [1897?]
+ Convert the string nan to NumPy’s NaN value

Synthesizing these patterns, we can actually take advantage of a single regular expression to extract the publication year:


```python
extr = df['Date of Publication'].str.extract(r'^(\d{4})', expand=False)
extr.head()
```




    Identifier
    206    1879
    216    1868
    218    1869
    472    1851
    480    1857
    Name: Date of Publication, dtype: object



Not familiar with regex? You can [inspect the expression above](https://regex101.com/r/3AJ1Pv/1) at regex101.com and read more at the Python Regular Expressions [HOWTO](https://docs.python.org/3.6/howto/regex.html).

Now we will convert the series of extracted dates into numeric values that will replace their object counterparts. Basically, make the origianl 'Publication Date' column of dtype float.


```python
df['Date of Publication'] = pd.to_numeric(extr)
df['Date of Publication'].dtype
```




    dtype('float64')



Above, we replaced the original column with the column of extracted values. We did not replace the values that we did not result however. the percentage of missing publication date data is around 11%


```python
df['Date of Publication'].isnull().sum() / len(df)
```




    0.11717147339205986



### Combining str Methods with NumPy to Clean Columns

Now we will use a combination of pandas string methods and numpy where functions to clean the 'Place of Publication' field. 


```python
df['Place of Publication'].head(10)
```




    Identifier
    206                                  London
    216                London; Virtue & Yorston
    218                                  London
    472                                  London
    480                                  London
    481                                  London
    519                                  London
    667     pp. 40. G. Bryan & Co: Oxford, 1898
    874                                 London]
    1143                                 London
    Name: Place of Publication, dtype: object




```python
df.loc[4157862]
```




    Place of Publication                                  Newcastle-upon-Tyne
    Date of Publication                                                  1867
    Publisher                                                      T. Fordyce
    Title                   Local Records; or, Historical Register of rema...
    Author                      FORDYCE, T. - Printer, of Newcastle-upon-Tyne
    Flickr URL              http://www.flickr.com/photos/britishlibrary/ta...
    Name: 4157862, dtype: object




```python
df.loc[4159587]
```




    Place of Publication                                  Newcastle upon Tyne
    Date of Publication                                                  1834
    Publisher                                                Mackenzie & Dent
    Title                   An historical, topographical and descriptive v...
    Author                                              Mackenzie, E. (Eneas)
    Flickr URL              http://www.flickr.com/photos/britishlibrary/ta...
    Name: 4159587, dtype: object



For some of the entries made in London with extraneous information. In the above two examples, they reference the same place but one has hyphens in the name.


```python
pub = df['Place of Publication']
london = pub.str.contains('London')
london[:5]

```




    Identifier
    206    True
    216    True
    218    True
    472    True
    480    True
    Name: Place of Publication, dtype: bool




```python
oxford = pub.str.contains('Oxford')
```


```python
# Or we can use np
df['Place of Publication'] = np.where(london, 'London',
                                      np.where(oxford, 'Oxford',
                                               pub.str.replace('-', ' ')))
df['Place of Publication'].head()
```




    Identifier
    206    London
    216    London
    218    London
    472    London
    480    London
    Name: Place of Publication, dtype: object




```python
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
      <th>Place of Publication</th>
      <th>Date of Publication</th>
      <th>Publisher</th>
      <th>Title</th>
      <th>Author</th>
      <th>Flickr URL</th>
    </tr>
    <tr>
      <th>Identifier</th>
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
      <th>206</th>
      <td>London</td>
      <td>1879.0</td>
      <td>S. Tinsley &amp; Co.</td>
      <td>Walter Forbes. [A novel.] By A. A</td>
      <td>A. A.</td>
      <td>http://www.flickr.com/photos/britishlibrary/ta...</td>
    </tr>
    <tr>
      <th>216</th>
      <td>London</td>
      <td>1868.0</td>
      <td>Virtue &amp; Co.</td>
      <td>All for Greed. [A novel. The dedication signed...</td>
      <td>A., A. A.</td>
      <td>http://www.flickr.com/photos/britishlibrary/ta...</td>
    </tr>
    <tr>
      <th>218</th>
      <td>London</td>
      <td>1869.0</td>
      <td>Bradbury, Evans &amp; Co.</td>
      <td>Love the Avenger. By the author of “All for Gr...</td>
      <td>A., A. A.</td>
      <td>http://www.flickr.com/photos/britishlibrary/ta...</td>
    </tr>
    <tr>
      <th>472</th>
      <td>London</td>
      <td>1851.0</td>
      <td>James Darling</td>
      <td>Welsh Sketches, chiefly ecclesiastical, to the...</td>
      <td>A., E. S.</td>
      <td>http://www.flickr.com/photos/britishlibrary/ta...</td>
    </tr>
    <tr>
      <th>480</th>
      <td>London</td>
      <td>1857.0</td>
      <td>Wertheim &amp; Macintosh</td>
      <td>[The World in which I live, and my place in it...</td>
      <td>A., E. S.</td>
      <td>http://www.flickr.com/photos/britishlibrary/ta...</td>
    </tr>
  </tbody>
</table>
</div>



### Cleaning the Entire Dataset Using the applymap Function


```python
university_towns = []
with open('datasets/university_towns.txt') as file:
    for line in file:
        if '[edit]' in line:
            # Remember this `state` until the next is found
            state = line
        else:
            # Otherwise, we have a city; keep `state` as last-seen
            university_towns.append((state, line))

university_towns[:5]
```




    [('Alabama[edit]\n', 'Auburn (Auburn University)[1]\n'),
     ('Alabama[edit]\n', 'Florence (University of North Alabama)\n'),
     ('Alabama[edit]\n', 'Jacksonville (Jacksonville State University)[2]\n'),
     ('Alabama[edit]\n', 'Livingston (University of West Alabama)[2]\n'),
     ('Alabama[edit]\n', 'Montevallo (University of Montevallo)[2]\n')]




```python
towns_df = pd.DataFrame(university_towns,
                        columns=['State', 'RegionName'])

towns_df.head()
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
      <th>State</th>
      <th>RegionName</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alabama[edit]\n</td>
      <td>Auburn (Auburn University)[1]\n</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alabama[edit]\n</td>
      <td>Florence (University of North Alabama)\n</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Alabama[edit]\n</td>
      <td>Jacksonville (Jacksonville State University)[2]\n</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alabama[edit]\n</td>
      <td>Livingston (University of West Alabama)[2]\n</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alabama[edit]\n</td>
      <td>Montevallo (University of Montevallo)[2]\n</td>
    </tr>
  </tbody>
</table>
</div>




```python
def get_citystate(item):
    if ' (' in item:
        return item[:item.find(' (')]
    elif '[' in item:
        return item[:item.find('[')]
    else:
        return item
    
towns_df =  towns_df.applymap(get_citystate)
```


```python
towns_df.head()
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
      <th>State</th>
      <th>RegionName</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alabama</td>
      <td>Auburn</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alabama</td>
      <td>Florence</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Alabama</td>
      <td>Jacksonville</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alabama</td>
      <td>Livingston</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alabama</td>
      <td>Montevallo</td>
    </tr>
  </tbody>
</table>
</div>



"Technical Detail: While it is a convenient and versatile method, .applymap can have significant runtime for larger datasets, because it maps a Python callable to each individual element. In some cases, it can be more efficient to do vectorized operations that utilize Cython or NumPY (which, in turn, makes calls in C) under the hood."

### Renaming Columns and Skipping Rows

Sometimes its necessary to rename columns so that they are more readable and make more sense. In adition to those poorly named columns, there might be whole rows that contain unnecessary information that we might want to exclude from our dataframe.


```python
olympics_df = pd.read_csv('Datasets/olympics.csv')
olympics_df.head()
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
      <th>11</th>
      <th>12</th>
      <th>13</th>
      <th>14</th>
      <th>15</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>? Summer</td>
      <td>01 !</td>
      <td>02 !</td>
      <td>03 !</td>
      <td>Total</td>
      <td>? Winter</td>
      <td>01 !</td>
      <td>02 !</td>
      <td>03 !</td>
      <td>Total</td>
      <td>? Games</td>
      <td>01 !</td>
      <td>02 !</td>
      <td>03 !</td>
      <td>Combined total</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Afghanistan (AFG)</td>
      <td>13</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>13</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Algeria (ALG)</td>
      <td>12</td>
      <td>5</td>
      <td>2</td>
      <td>8</td>
      <td>15</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>15</td>
      <td>5</td>
      <td>2</td>
      <td>8</td>
      <td>15</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Argentina (ARG)</td>
      <td>23</td>
      <td>18</td>
      <td>24</td>
      <td>28</td>
      <td>70</td>
      <td>18</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>41</td>
      <td>18</td>
      <td>24</td>
      <td>28</td>
      <td>70</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Armenia (ARM)</td>
      <td>5</td>
      <td>1</td>
      <td>2</td>
      <td>9</td>
      <td>12</td>
      <td>6</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>11</td>
      <td>1</td>
      <td>2</td>
      <td>9</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>



There are many problems with this:
+ The row that should have been our column names is located on df.iloc[0]
+ NaN should actually be Country
+ Summer actually stands for summer games
+ 01 means Gold Medals

A dataset like this is hard to interperet without access to the source from where it came from which luckily, we have.  


```python
# We can skip the first row and set the second row as our header like this:
olympics_df = pd.read_csv('Datasets/olympics.csv', header=1)
olympics_df.head()
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
      <th>Unnamed: 0</th>
      <th>? Summer</th>
      <th>01 !</th>
      <th>02 !</th>
      <th>03 !</th>
      <th>Total</th>
      <th>? Winter</th>
      <th>01 !.1</th>
      <th>02 !.1</th>
      <th>03 !.1</th>
      <th>Total.1</th>
      <th>? Games</th>
      <th>01 !.2</th>
      <th>02 !.2</th>
      <th>03 !.2</th>
      <th>Combined total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan (AFG)</td>
      <td>13</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>13</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Algeria (ALG)</td>
      <td>12</td>
      <td>5</td>
      <td>2</td>
      <td>8</td>
      <td>15</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>15</td>
      <td>5</td>
      <td>2</td>
      <td>8</td>
      <td>15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Argentina (ARG)</td>
      <td>23</td>
      <td>18</td>
      <td>24</td>
      <td>28</td>
      <td>70</td>
      <td>18</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>41</td>
      <td>18</td>
      <td>24</td>
      <td>28</td>
      <td>70</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Armenia (ARM)</td>
      <td>5</td>
      <td>1</td>
      <td>2</td>
      <td>9</td>
      <td>12</td>
      <td>6</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>11</td>
      <td>1</td>
      <td>2</td>
      <td>9</td>
      <td>12</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Australasia (ANZ) [ANZ]</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
      <td>5</td>
      <td>12</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
      <td>5</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>



To rename the columns, we will make use of a DataFrame’s rename() method, which allows you to relabel an axis based on a mapping (in this case, a dict).

Let’s start by defining a dictionary that maps current column names (as keys) to more usable ones (the dictionary’s values):


```python
new_names =  {'Unnamed: 0': 'Country',
              '? Summer': 'Summer Olympics',
              '01 !': 'Gold',
              '02 !': 'Silver',
              '03 !': 'Bronze',
              '? Winter': 'Winter Olympics',
              '01 !.1': 'Gold.1',
              '02 !.1': 'Silver.1',
              '03 !.1': 'Bronze.1',
              '? Games': '# Games',
              '01 !.2': 'Gold.2',
              '02 !.2': 'Silver.2',
              '03 !.2': 'Bronze.2'}

```


```python
olympics_df.rename(columns=new_names, inplace=True)

```


```python
olympics_df.head()
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
      <th>Country</th>
      <th>Summer Olympics</th>
      <th>Gold</th>
      <th>Silver</th>
      <th>Bronze</th>
      <th>Total</th>
      <th>Winter Olympics</th>
      <th>Gold.1</th>
      <th>Silver.1</th>
      <th>Bronze.1</th>
      <th>Total.1</th>
      <th># Games</th>
      <th>Gold.2</th>
      <th>Silver.2</th>
      <th>Bronze.2</th>
      <th>Combined total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan (AFG)</td>
      <td>13</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>13</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Algeria (ALG)</td>
      <td>12</td>
      <td>5</td>
      <td>2</td>
      <td>8</td>
      <td>15</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>15</td>
      <td>5</td>
      <td>2</td>
      <td>8</td>
      <td>15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Argentina (ARG)</td>
      <td>23</td>
      <td>18</td>
      <td>24</td>
      <td>28</td>
      <td>70</td>
      <td>18</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>41</td>
      <td>18</td>
      <td>24</td>
      <td>28</td>
      <td>70</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Armenia (ARM)</td>
      <td>5</td>
      <td>1</td>
      <td>2</td>
      <td>9</td>
      <td>12</td>
      <td>6</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>11</td>
      <td>1</td>
      <td>2</td>
      <td>9</td>
      <td>12</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Australasia (ANZ) [ANZ]</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
      <td>5</td>
      <td>12</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
      <td>5</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>



### Recap

+ There are many useful methods for cleaning data. 
+ Knowing where the data comes from and what it is supposed to represent can help in the naming of columns, and the filtering of information by its relevance.
+ Minimize the amount of missing data and keep the data in each column uniform.
+ Python regex can be very helpful and I will sure to explore more of that in the future.
