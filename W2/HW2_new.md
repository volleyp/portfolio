```python
import pandas as pd
import numpy as np


data1 = pd.read_csv("Booli_sold.csv")
```


```python
data1.head()

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
      <th>listPrice</th>
      <th>rent</th>
      <th>livingArea</th>
      <th>rooms</th>
      <th>published</th>
      <th>constructionYear</th>
      <th>objectType</th>
      <th>booliId</th>
      <th>soldDate</th>
      <th>soldPrice</th>
      <th>...</th>
      <th>location.position.latitude</th>
      <th>location.position.longitude</th>
      <th>location.position.isApproximate</th>
      <th>location.region.municipalityName</th>
      <th>location.region.countyName</th>
      <th>location.distance.ocean</th>
      <th>source.name</th>
      <th>source.id</th>
      <th>source.type</th>
      <th>source.url</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3995000</td>
      <td>4467.0</td>
      <td>73.0</td>
      <td>3.0</td>
      <td>2018-10-15 13:33:18</td>
      <td>1935.0</td>
      <td>Lägenhet</td>
      <td>3263989</td>
      <td>2018-11-08</td>
      <td>3820000</td>
      <td>...</td>
      <td>59.371033</td>
      <td>18.054057</td>
      <td>NaN</td>
      <td>Stockholm</td>
      <td>Stockholms län</td>
      <td>260</td>
      <td>MOHV</td>
      <td>1901865</td>
      <td>Broker</td>
      <td>http://www.mohv.se/</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1995000</td>
      <td>1773.0</td>
      <td>36.0</td>
      <td>1.0</td>
      <td>2018-10-05 14:29:28</td>
      <td>1968.0</td>
      <td>Lägenhet</td>
      <td>3256231</td>
      <td>2018-10-19</td>
      <td>2355000</td>
      <td>...</td>
      <td>59.371242</td>
      <td>18.057821</td>
      <td>NaN</td>
      <td>Stockholm</td>
      <td>Stockholms län</td>
      <td>218</td>
      <td>Notar</td>
      <td>1566</td>
      <td>Broker</td>
      <td>http://www.notar.se/</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5100000</td>
      <td>3839.0</td>
      <td>81.0</td>
      <td>3.0</td>
      <td>2018-09-11 13:44:43</td>
      <td>1936.0</td>
      <td>Lägenhet</td>
      <td>3236660</td>
      <td>2018-09-27</td>
      <td>6110000</td>
      <td>...</td>
      <td>59.371617</td>
      <td>18.054716</td>
      <td>NaN</td>
      <td>Stockholm</td>
      <td>Stockholms län</td>
      <td>186</td>
      <td>Historiska Hem AB</td>
      <td>65645750</td>
      <td>Broker</td>
      <td>http://historiskahem.se/</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5495000</td>
      <td>4483.0</td>
      <td>107.0</td>
      <td>4.0</td>
      <td>2018-08-25 02:56:56</td>
      <td>1936.0</td>
      <td>Lägenhet</td>
      <td>3224374</td>
      <td>2018-09-06</td>
      <td>8050000</td>
      <td>...</td>
      <td>59.371480</td>
      <td>18.053880</td>
      <td>NaN</td>
      <td>Stockholm</td>
      <td>Stockholms län</td>
      <td>218</td>
      <td>Notar</td>
      <td>1566</td>
      <td>Broker</td>
      <td>http://www.notar.se/</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1995000</td>
      <td>1696.0</td>
      <td>29.0</td>
      <td>1.0</td>
      <td>2018-06-15 17:16:19</td>
      <td>1936.0</td>
      <td>Lägenhet</td>
      <td>3185496</td>
      <td>2018-06-18</td>
      <td>2400000</td>
      <td>...</td>
      <td>59.372160</td>
      <td>18.053542</td>
      <td>True</td>
      <td>Stockholm</td>
      <td>Stockholms län</td>
      <td>166</td>
      <td>Mäklarhuset</td>
      <td>204</td>
      <td>Broker</td>
      <td>http://www.maklarhuset.se/</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 27 columns</p>
</div>



### Apartment Prices

the ppsqm is **soldPrice / livingArea**  
We want then to add the new **ppsqm** column to the original table  .


```python
squareMeters = data1.loc[:, "livingArea"] #select all rows : and a specific column "livingArea"

soldPrice = data1.loc[:, "listPrice"] #select all rows : and a specific column "soldPrice"

ppsqm = round(soldPrice / squareMeters) #Round the number to the nearest integer

data1["ppsqm"] = ppsqm #Adding the new columnt to the original data set
```


```python
data1.head()
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
      <th>listPrice</th>
      <th>rent</th>
      <th>livingArea</th>
      <th>rooms</th>
      <th>published</th>
      <th>constructionYear</th>
      <th>objectType</th>
      <th>booliId</th>
      <th>soldDate</th>
      <th>soldPrice</th>
      <th>...</th>
      <th>location.position.longitude</th>
      <th>location.position.isApproximate</th>
      <th>location.region.municipalityName</th>
      <th>location.region.countyName</th>
      <th>location.distance.ocean</th>
      <th>source.name</th>
      <th>source.id</th>
      <th>source.type</th>
      <th>source.url</th>
      <th>ppsqm</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3995000</td>
      <td>4467.0</td>
      <td>73.0</td>
      <td>3.0</td>
      <td>2018-10-15 13:33:18</td>
      <td>1935.0</td>
      <td>Lägenhet</td>
      <td>3263989</td>
      <td>2018-11-08</td>
      <td>3820000</td>
      <td>...</td>
      <td>18.054057</td>
      <td>NaN</td>
      <td>Stockholm</td>
      <td>Stockholms län</td>
      <td>260</td>
      <td>MOHV</td>
      <td>1901865</td>
      <td>Broker</td>
      <td>http://www.mohv.se/</td>
      <td>54726.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1995000</td>
      <td>1773.0</td>
      <td>36.0</td>
      <td>1.0</td>
      <td>2018-10-05 14:29:28</td>
      <td>1968.0</td>
      <td>Lägenhet</td>
      <td>3256231</td>
      <td>2018-10-19</td>
      <td>2355000</td>
      <td>...</td>
      <td>18.057821</td>
      <td>NaN</td>
      <td>Stockholm</td>
      <td>Stockholms län</td>
      <td>218</td>
      <td>Notar</td>
      <td>1566</td>
      <td>Broker</td>
      <td>http://www.notar.se/</td>
      <td>55417.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5100000</td>
      <td>3839.0</td>
      <td>81.0</td>
      <td>3.0</td>
      <td>2018-09-11 13:44:43</td>
      <td>1936.0</td>
      <td>Lägenhet</td>
      <td>3236660</td>
      <td>2018-09-27</td>
      <td>6110000</td>
      <td>...</td>
      <td>18.054716</td>
      <td>NaN</td>
      <td>Stockholm</td>
      <td>Stockholms län</td>
      <td>186</td>
      <td>Historiska Hem AB</td>
      <td>65645750</td>
      <td>Broker</td>
      <td>http://historiskahem.se/</td>
      <td>62963.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5495000</td>
      <td>4483.0</td>
      <td>107.0</td>
      <td>4.0</td>
      <td>2018-08-25 02:56:56</td>
      <td>1936.0</td>
      <td>Lägenhet</td>
      <td>3224374</td>
      <td>2018-09-06</td>
      <td>8050000</td>
      <td>...</td>
      <td>18.053880</td>
      <td>NaN</td>
      <td>Stockholm</td>
      <td>Stockholms län</td>
      <td>218</td>
      <td>Notar</td>
      <td>1566</td>
      <td>Broker</td>
      <td>http://www.notar.se/</td>
      <td>51355.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1995000</td>
      <td>1696.0</td>
      <td>29.0</td>
      <td>1.0</td>
      <td>2018-06-15 17:16:19</td>
      <td>1936.0</td>
      <td>Lägenhet</td>
      <td>3185496</td>
      <td>2018-06-18</td>
      <td>2400000</td>
      <td>...</td>
      <td>18.053542</td>
      <td>True</td>
      <td>Stockholm</td>
      <td>Stockholms län</td>
      <td>166</td>
      <td>Mäklarhuset</td>
      <td>204</td>
      <td>Broker</td>
      <td>http://www.maklarhuset.se/</td>
      <td>68793.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 28 columns</p>
</div>



Now the goal is to rank top 5 most expensive apartments w.r.t ppsqm. We want to sort the **ppsqm** by price and then see the 5 top candidates. Lets do that with the **sort** function and then print the head of our dataframe so that we can see top 5 candidates wrt ppsqm.




```python
table_sorted_by_ppsqm = data1.sort_values("ppsqm", ascending=False) 
table_sorted_by_ppsqm.head()
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
      <th>listPrice</th>
      <th>rent</th>
      <th>livingArea</th>
      <th>rooms</th>
      <th>published</th>
      <th>constructionYear</th>
      <th>objectType</th>
      <th>booliId</th>
      <th>soldDate</th>
      <th>soldPrice</th>
      <th>...</th>
      <th>location.position.longitude</th>
      <th>location.position.isApproximate</th>
      <th>location.region.municipalityName</th>
      <th>location.region.countyName</th>
      <th>location.distance.ocean</th>
      <th>source.name</th>
      <th>source.id</th>
      <th>source.type</th>
      <th>source.url</th>
      <th>ppsqm</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>2295000</td>
      <td>1743.0</td>
      <td>29.0</td>
      <td>1.0</td>
      <td>2018-05-05 04:43:36</td>
      <td>1935.0</td>
      <td>Lägenhet</td>
      <td>3125674</td>
      <td>2018-05-19</td>
      <td>2420000</td>
      <td>...</td>
      <td>18.054986</td>
      <td>True</td>
      <td>Stockholm</td>
      <td>Stockholms län</td>
      <td>136</td>
      <td>Mäklarhuset</td>
      <td>204</td>
      <td>Broker</td>
      <td>http://www.maklarhuset.se/</td>
      <td>79138.0</td>
    </tr>
    <tr>
      <th>50</th>
      <td>1890000</td>
      <td>1464.0</td>
      <td>24.0</td>
      <td>1.0</td>
      <td>2016-06-11 08:55:51</td>
      <td>1935.0</td>
      <td>Lägenhet</td>
      <td>2125576</td>
      <td>2016-06-21</td>
      <td>2450000</td>
      <td>...</td>
      <td>18.055270</td>
      <td>NaN</td>
      <td>Stockholm</td>
      <td>Stockholms län</td>
      <td>161</td>
      <td>HusmanHagberg</td>
      <td>1610</td>
      <td>Broker</td>
      <td>http://www.husmanhagberg.se/</td>
      <td>78750.0</td>
    </tr>
    <tr>
      <th>54</th>
      <td>1795000</td>
      <td>1374.0</td>
      <td>23.0</td>
      <td>1.0</td>
      <td>2016-04-15 19:10:49</td>
      <td>1935.0</td>
      <td>Lägenhet</td>
      <td>2078171</td>
      <td>2016-04-28</td>
      <td>2300000</td>
      <td>...</td>
      <td>18.055422</td>
      <td>True</td>
      <td>Stockholm</td>
      <td>Stockholms län</td>
      <td>135</td>
      <td>Notar</td>
      <td>1566</td>
      <td>Broker</td>
      <td>http://www.notar.se/</td>
      <td>78043.0</td>
    </tr>
    <tr>
      <th>49</th>
      <td>3495000</td>
      <td>3052.0</td>
      <td>47.0</td>
      <td>2.0</td>
      <td>2016-07-31 06:06:54</td>
      <td>NaN</td>
      <td>Lägenhet</td>
      <td>2145197</td>
      <td>2016-08-15</td>
      <td>3375000</td>
      <td>...</td>
      <td>18.053174</td>
      <td>True</td>
      <td>Stockholm</td>
      <td>Stockholms län</td>
      <td>171</td>
      <td>Notar</td>
      <td>1566</td>
      <td>Broker</td>
      <td>http://www.notar.se/</td>
      <td>74362.0</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2500000</td>
      <td>1400.0</td>
      <td>35.0</td>
      <td>1.0</td>
      <td>2017-09-08 15:22:24</td>
      <td>1936.0</td>
      <td>Lägenhet</td>
      <td>2405043</td>
      <td>2017-10-06</td>
      <td>2560000</td>
      <td>...</td>
      <td>18.053880</td>
      <td>NaN</td>
      <td>Stockholm</td>
      <td>Stockholms län</td>
      <td>218</td>
      <td>HusmanHagberg</td>
      <td>1610</td>
      <td>Broker</td>
      <td>http://www.husmanhagberg.se/</td>
      <td>71429.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 28 columns</p>
</div>



Now let us calculate the average ppsqm in Ekhagen. For this purpose we can just calculate the mean of the **ppsqw**. Note that the np.mean - function automatically ignores the missing values of ppsqw vector.


```python
ekhagen_mean = round(np.mean(ppsqm))

print("The average ppsqm in Ekhagen is: " , ekhagen_mean )
```

    The average ppsqm in Ekhagen is:  54127
    

What i find interesting about the data is that some values for the living area are missing which will naturally lead to that some values of the ppsqw will be missing ( by a trivial reasons). However when calculating the mean of ppsqw we were able to preserve the sample size.

### The Swedish Election of 2018

Calculate the total number of legitimate votes (Giltiga Röster) in Stockholm during the election. That is, sum upp the number of legitimate votes for all municipalities (kommun) in Stockholm.


```python
data2 = pd.read_csv("2018_R_per_kommun.csv", sep = ";", decimal =",")
 
data2.head()
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
      <th>LÄNSKOD</th>
      <th>KOMMUNKOD</th>
      <th>LÄNSNAMN</th>
      <th>KOMMUNNAMN</th>
      <th>M</th>
      <th>C</th>
      <th>L</th>
      <th>KD</th>
      <th>S</th>
      <th>V</th>
      <th>...</th>
      <th>TRP</th>
      <th>VL-S</th>
      <th>ÖVR</th>
      <th>OGEJ</th>
      <th>BLANK</th>
      <th>OG</th>
      <th>RÖSTER GILTIGA</th>
      <th>RÖSTANDE</th>
      <th>RÖSTBERÄTTIGADE</th>
      <th>VALDELTAGANDE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>14</td>
      <td>Stockholms län</td>
      <td>Upplands Väsby</td>
      <td>23.11</td>
      <td>6.26</td>
      <td>5.66</td>
      <td>6.71</td>
      <td>26.97</td>
      <td>8.01</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.04</td>
      <td>0.69</td>
      <td>0.06</td>
      <td>25830</td>
      <td>26036</td>
      <td>30740</td>
      <td>84.70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>15</td>
      <td>Stockholms län</td>
      <td>Vallentuna</td>
      <td>28.29</td>
      <td>10.11</td>
      <td>7.73</td>
      <td>7.58</td>
      <td>18.91</td>
      <td>4.47</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>0.00</td>
      <td>0.02</td>
      <td>0.59</td>
      <td>0.08</td>
      <td>20952</td>
      <td>21099</td>
      <td>23438</td>
      <td>90.02</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>17</td>
      <td>Stockholms län</td>
      <td>Österåker</td>
      <td>29.68</td>
      <td>9.35</td>
      <td>7.48</td>
      <td>7.13</td>
      <td>19.71</td>
      <td>4.97</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.01</td>
      <td>0.03</td>
      <td>0.69</td>
      <td>0.13</td>
      <td>27711</td>
      <td>27947</td>
      <td>31309</td>
      <td>89.26</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>20</td>
      <td>Stockholms län</td>
      <td>Värmdö</td>
      <td>27.49</td>
      <td>9.76</td>
      <td>6.40</td>
      <td>5.89</td>
      <td>20.48</td>
      <td>6.02</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.01</td>
      <td>0.04</td>
      <td>0.67</td>
      <td>0.07</td>
      <td>28115</td>
      <td>28335</td>
      <td>31371</td>
      <td>90.32</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>23</td>
      <td>Stockholms län</td>
      <td>Järfälla</td>
      <td>23.96</td>
      <td>6.31</td>
      <td>6.04</td>
      <td>6.29</td>
      <td>27.68</td>
      <td>8.75</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>0.02</td>
      <td>0.04</td>
      <td>0.53</td>
      <td>0.07</td>
      <td>45654</td>
      <td>45948</td>
      <td>53230</td>
      <td>86.32</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 45 columns</p>
</div>



Deriving stockholm and legit votes


```python
votes = data2.loc[:, ["LÄNSNAMN", "RÖSTER GILTIGA"]]

filtered_votes = votes[votes["LÄNSNAMN"].str.contains("Stockholms län", case=False, na=False)]

legit_votes_in_stockholm = filtered_votes.loc[:,"RÖSTER GILTIGA"]

legit_votes_in_stockholm_sum = sum(legit_votes_in_stockholm)

legit_votes_in_stockholm_sum
```




    1426237



In which municipality did the social democratic party (Social demokraterna, S) garner the hightest voting percentage?

We can approach this by simply filtering the data in such a way that we only se manucipalitys and precentage that S got. BY later filtering the data some more so that we rearang rows so that the highest ranks first etc we will be able to clearly see the first one. And we can also use almost the exact same approach for calculating the top 3 municipalitys and presenting it in a table after.


```python
s = data2.loc[:, ["KOMMUNNAMN","S"]].sort_values(by = "S", ascending = False) #sortering and filtering the data

s.head()
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
      <th>KOMMUNNAMN</th>
      <th>S</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>188</th>
      <td>Munkfors</td>
      <td>52.18</td>
    </tr>
    <tr>
      <th>286</th>
      <td>Piteå</td>
      <td>47.48</td>
    </tr>
    <tr>
      <th>196</th>
      <td>Hagfors</td>
      <td>47.46</td>
    </tr>
    <tr>
      <th>279</th>
      <td>Överkalix</td>
      <td>46.68</td>
    </tr>
    <tr>
      <th>280</th>
      <td>Kalix</td>
      <td>45.37</td>
    </tr>
  </tbody>
</table>
</div>




```python
valdeltagande = data2.loc[:, ["KOMMUNNAMN", "VALDELTAGANDE"]].sort_values(by ="VALDELTAGANDE", ascending = False)

valdeltagande.head(3)
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
      <th>KOMMUNNAMN</th>
      <th>VALDELTAGANDE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>103</th>
      <td>Lomma</td>
      <td>93.86</td>
    </tr>
    <tr>
      <th>59</th>
      <td>Habo</td>
      <td>93.35</td>
    </tr>
    <tr>
      <th>98</th>
      <td>Vellinge</td>
      <td>93.13</td>
    </tr>
  </tbody>
</table>
</div>




```python
!jupyter nbconvert --to markdown HW2_new.ipynb
```

    [NbConvertApp] Converting notebook HW2_new.ipynb to markdown
    [NbConvertApp] Writing 7532 bytes to HW2_new.md
    


```python

```
