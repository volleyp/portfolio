# IRIS data

Data consist of informatiom about **3** different species of iris flowers.

* Iris-setosa
* Iris-versicolor
* Iris-verginica



The data contains information about the dimensions of flowers, i.e., the length and width of both the petal and sepal. The task is to visualize the dataset and explore any connections between the dimensions of the petal and sepal. Let's create a plot for the length/width of the petal versus the length/width of the sepal. This way, we can investigate if there is any correlation between these two sets of dimensions.


```python
from IPython.display import HTML # So that we can convert tables to html properly
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns


pd.set_option('display.max_rows', 200)
data = pd.read_csv('IRIS.csv')



fig, axes = plt.subplots(1, 2, figsize=(12, 5))

sns.scatterplot(data=data, x="sepal_length", y="petal_length", hue="species" , ax = axes[0])
axes[0].set_title("Sepal_length vs Petal_length")
sns.scatterplot(data=data, x="sepal_width", y="petal_width", hue="species" , ax = axes[1])
axes[1].set_title("Sepal_width vs Petal_width")

plt.tight_layout()


for ax in axes:
    ax.grid(True)

plt.show
```




    <function matplotlib.pyplot.show(close=None, block=None)>




    
![png](HW3_files/HW3_1_1.png)
    



If you look at the length, you'll notice that all three species seem to have a positive correlation. However, the correlation is not as clear for Iris-setosa as for Iris-versicolor, Iris-virginica. If you then examine the width, the relationship appears more blurry. However, it seems to lean towards a positive correlation for Iris-versicolor, Iris-virginica, while Iris-setosa lacks a clear relationship. To investigate how these values are distributed, we can create boxplots and plot them close to each other for easier comparison.


```python
fig, axes = plt.subplots(2, 2, figsize=(12, 5))


sns.boxplot( y=data["sepal_width"], x=data["species"] , ax = axes[0,0], hue=data["species"])
sns.boxplot( y=data["sepal_length"], x=data["species"] , ax = axes[0,1], hue=data["species"])
sns.boxplot( y=data["petal_width"], x=data["species"] , ax = axes[1,0], hue=data["species"])
sns.boxplot( y=data["petal_length"], x=data["species"] , ax = axes[1,1], hue=data["species"])

plt.tight_layout()
plt.show()

```


    
![png](HW3_files/HW3_3_0.png)
    


### Conclusion 
From these boxplots we can conclude that the median for petal width is strict. The values or ordered as iris-setosa lowest , iris versicolor in the middle and iris virginica at the top. Same distribution is for petal_length and sepal length while sepal width has different distribution.dfdf 


```python
fig, axes = plt.subplots(1, 2, figsize=(12, 5))

sns.scatterplot(data=data, x="sepal_length", y="petal_length", hue="species" , ax = axes[0])
axes[0].set_title("Sepal_length vs Petal_length")


sns.scatterplot(data=data, x="sepal_width", y="sepal_length", hue="species" , ax = axes[1])
axes[1].set_title("Sepal_width vs Petal_width")

plt.tight_layout()


for ax in axes:
    ax.grid(True)

plt.show
```




    <function matplotlib.pyplot.show(close=None, block=None)>




    
![png](HW3_files/HW3_5_1.png)
    



```python
sns.pairplot(data, hue = "species")
```




    <seaborn.axisgrid.PairGrid at 0x255788afb50>




    
![png](HW3_files/HW3_6_1.png)
    


From this pairplot we can easily acces the distributions for petal/sepal length and width and see scatter plots for each variable combination. For instance if we look at:

* Sepal Width and petal length plot:
 For iris setosa for the approximatly same petal length the values of sepal width can varie quite a bit
 while for iris-versicolor there seems to be a positive correlation.

# Birdwatching




```python
data2 = pd.read_csv("artportalen.csv")
pd.set_option('display.max_columns', 30)
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
      <th>Id</th>
      <th>Taxonsorteringsordning</th>
      <th>Rödlistade</th>
      <th>Artnamn</th>
      <th>Vetenskapligt namn</th>
      <th>Auktor</th>
      <th>Antal</th>
      <th>Ålder/stadium</th>
      <th>Kön</th>
      <th>Aktivitet</th>
      <th>Lokalnamn</th>
      <th>Ostkoordinat</th>
      <th>Nordkoordinat</th>
      <th>Noggrannhet</th>
      <th>Diffusion</th>
      <th>Län</th>
      <th>Kommun</th>
      <th>Provins</th>
      <th>Församling</th>
      <th>Startdatum</th>
      <th>Starttid</th>
      <th>Slutdatum</th>
      <th>Sluttid</th>
      <th>Kommentar</th>
      <th>Biotop</th>
      <th>Rapportör</th>
      <th>Observatörer</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>97785066</td>
      <td>55235</td>
      <td>NaN</td>
      <td>Koltrast</td>
      <td>Turdus merula</td>
      <td>Linnaeus, 1758</td>
      <td>2</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Björnstigen 129,Bergshamra,Solna</td>
      <td>1626890</td>
      <td>6586736</td>
      <td>25</td>
      <td>0</td>
      <td>Stockholm</td>
      <td>Solna</td>
      <td>Uppland</td>
      <td>Solna</td>
      <td>2022-01-01</td>
      <td>NaN</td>
      <td>2022-01-01</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Björn Lindkvist</td>
      <td>Björn Lindkvist</td>
    </tr>
    <tr>
      <th>1</th>
      <td>97785067</td>
      <td>54989</td>
      <td>NaN</td>
      <td>Blåmes</td>
      <td>Cyanistes caeruleus</td>
      <td>(Linnaeus, 1758)</td>
      <td>2</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Björnstigen 129,Bergshamra,Solna</td>
      <td>1626890</td>
      <td>6586736</td>
      <td>25</td>
      <td>0</td>
      <td>Stockholm</td>
      <td>Solna</td>
      <td>Uppland</td>
      <td>Solna</td>
      <td>2022-01-01</td>
      <td>NaN</td>
      <td>2022-01-01</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Björn Lindkvist</td>
      <td>Björn Lindkvist</td>
    </tr>
    <tr>
      <th>2</th>
      <td>97785310</td>
      <td>55235</td>
      <td>NaN</td>
      <td>Koltrast</td>
      <td>Turdus merula</td>
      <td>Linnaeus, 1758</td>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Frösundavik</td>
      <td>1626094</td>
      <td>6585523</td>
      <td>100</td>
      <td>0</td>
      <td>Stockholm</td>
      <td>Solna</td>
      <td>Uppland</td>
      <td>Solna</td>
      <td>2022-01-01</td>
      <td>NaN</td>
      <td>2022-01-01</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Anders Eriksson</td>
      <td>Anders Eriksson</td>
    </tr>
    <tr>
      <th>3</th>
      <td>97786982</td>
      <td>54735</td>
      <td>NaN</td>
      <td>Sparvhök</td>
      <td>Accipiter nisus</td>
      <td>(Linnaeus, 1758)</td>
      <td>1</td>
      <td>NaN</td>
      <td>hona</td>
      <td>NaN</td>
      <td>Frösundavik</td>
      <td>1626094</td>
      <td>6585523</td>
      <td>100</td>
      <td>0</td>
      <td>Stockholm</td>
      <td>Solna</td>
      <td>Uppland</td>
      <td>Solna</td>
      <td>2022-01-01</td>
      <td>NaN</td>
      <td>2022-01-01</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Anders Eriksson</td>
      <td>Anders Eriksson</td>
    </tr>
    <tr>
      <th>4</th>
      <td>97786985</td>
      <td>54944</td>
      <td>NaN</td>
      <td>Skata</td>
      <td>Pica pica</td>
      <td>(Linnaeus, 1758)</td>
      <td>2</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Tivoli</td>
      <td>1626780</td>
      <td>6585860</td>
      <td>125</td>
      <td>0</td>
      <td>Stockholm</td>
      <td>Solna</td>
      <td>Uppland</td>
      <td>Solna</td>
      <td>2021-12-30</td>
      <td>15:57</td>
      <td>2022-01-01</td>
      <td>09:36</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Henrik Spovin</td>
      <td>Henrik Spovin</td>
    </tr>
  </tbody>
</table>
</div>




```python
data2['Antal'] = pd.to_numeric(data2['Antal'], errors='coerce') # Convert to numeric values and handle strings as NaN (if exists)

most_prelevant = data2.groupby('Artnamn')['Antal'].sum().reset_index() #Sum the number of birds 
most_prevalent_sorted = most_prelevant.sort_values(by='Antal', ascending=False) #Sorting from high to low

most_prevalent_sorted 
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
      <th>Artnamn</th>
      <th>Antal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>42</th>
      <td>Grönsiska</td>
      <td>20211.0</td>
    </tr>
    <tr>
      <th>120</th>
      <td>Sothöna</td>
      <td>8308.0</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Gräsand</td>
      <td>7167.0</td>
    </tr>
    <tr>
      <th>132</th>
      <td>Storskrake</td>
      <td>6750.0</td>
    </tr>
    <tr>
      <th>168</th>
      <td>Vitkindad gås</td>
      <td>6345.0</td>
    </tr>
    <tr>
      <th>131</th>
      <td>Storskarv</td>
      <td>5281.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Björktrast</td>
      <td>3173.0</td>
    </tr>
    <tr>
      <th>61</th>
      <td>Koltrast</td>
      <td>2750.0</td>
    </tr>
    <tr>
      <th>166</th>
      <td>Vigg</td>
      <td>2375.0</td>
    </tr>
    <tr>
      <th>113</th>
      <td>Skrattmås</td>
      <td>2326.0</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Gråhäger</td>
      <td>2279.0</td>
    </tr>
    <tr>
      <th>148</th>
      <td>Talgoxe</td>
      <td>1967.0</td>
    </tr>
    <tr>
      <th>124</th>
      <td>Stare</td>
      <td>1911.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Blåmes</td>
      <td>1878.0</td>
    </tr>
    <tr>
      <th>115</th>
      <td>Skäggdopping</td>
      <td>1835.0</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Grågås</td>
      <td>1737.0</td>
    </tr>
    <tr>
      <th>94</th>
      <td>Pilfink</td>
      <td>1660.0</td>
    </tr>
    <tr>
      <th>35</th>
      <td>Gråkråka</td>
      <td>1619.0</td>
    </tr>
    <tr>
      <th>60</th>
      <td>Knölsvan</td>
      <td>1552.0</td>
    </tr>
    <tr>
      <th>37</th>
      <td>Gråsparv</td>
      <td>1485.0</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Fiskmås</td>
      <td>1417.0</td>
    </tr>
    <tr>
      <th>96</th>
      <td>Ringduva</td>
      <td>1392.0</td>
    </tr>
    <tr>
      <th>106</th>
      <td>Silltrut</td>
      <td>1291.0</td>
    </tr>
    <tr>
      <th>105</th>
      <td>Sidensvans</td>
      <td>1287.0</td>
    </tr>
    <tr>
      <th>58</th>
      <td>Knipa</td>
      <td>1095.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>Snatterand</td>
      <td>1082.0</td>
    </tr>
    <tr>
      <th>38</th>
      <td>Gråtrut</td>
      <td>1019.0</td>
    </tr>
    <tr>
      <th>109</th>
      <td>Skata</td>
      <td>996.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Bofink</td>
      <td>963.0</td>
    </tr>
    <tr>
      <th>56</th>
      <td>Kanadagås</td>
      <td>945.0</td>
    </tr>
    <tr>
      <th>111</th>
      <td>Skogsduva</td>
      <td>909.0</td>
    </tr>
    <tr>
      <th>55</th>
      <td>Kaja</td>
      <td>887.0</td>
    </tr>
    <tr>
      <th>46</th>
      <td>Gärdsmyg</td>
      <td>865.0</td>
    </tr>
    <tr>
      <th>125</th>
      <td>Steglits</td>
      <td>847.0</td>
    </tr>
    <tr>
      <th>40</th>
      <td>Grönfink</td>
      <td>807.0</td>
    </tr>
    <tr>
      <th>172</th>
      <td>Östersjötrut</td>
      <td>752.0</td>
    </tr>
    <tr>
      <th>100</th>
      <td>Rödhake</td>
      <td>737.0</td>
    </tr>
    <tr>
      <th>153</th>
      <td>Tofsvipa</td>
      <td>736.0</td>
    </tr>
    <tr>
      <th>136</th>
      <td>Större hackspett</td>
      <td>678.0</td>
    </tr>
    <tr>
      <th>85</th>
      <td>Nötväcka</td>
      <td>662.0</td>
    </tr>
    <tr>
      <th>147</th>
      <td>Sångsvan</td>
      <td>614.0</td>
    </tr>
    <tr>
      <th>150</th>
      <td>Taltrast</td>
      <td>567.0</td>
    </tr>
    <tr>
      <th>139</th>
      <td>Svarthätta</td>
      <td>521.0</td>
    </tr>
    <tr>
      <th>102</th>
      <td>Rödvingetrast</td>
      <td>501.0</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Bergfink</td>
      <td>487.0</td>
    </tr>
    <tr>
      <th>155</th>
      <td>Tornseglare</td>
      <td>480.0</td>
    </tr>
    <tr>
      <th>84</th>
      <td>Nötskrika</td>
      <td>471.0</td>
    </tr>
    <tr>
      <th>142</th>
      <td>Sädesärla</td>
      <td>453.0</td>
    </tr>
    <tr>
      <th>127</th>
      <td>Stenknäck</td>
      <td>437.0</td>
    </tr>
    <tr>
      <th>141</th>
      <td>Svartvit flugsnappare</td>
      <td>395.0</td>
    </tr>
    <tr>
      <th>43</th>
      <td>Grönsångare</td>
      <td>383.0</td>
    </tr>
    <tr>
      <th>158</th>
      <td>Trädkrypare</td>
      <td>329.0</td>
    </tr>
    <tr>
      <th>129</th>
      <td>Stjärtmes</td>
      <td>300.0</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Fisktärna</td>
      <td>290.0</td>
    </tr>
    <tr>
      <th>73</th>
      <td>Lövsångare</td>
      <td>287.0</td>
    </tr>
    <tr>
      <th>146</th>
      <td>Sånglärka</td>
      <td>285.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Brunand</td>
      <td>267.0</td>
    </tr>
    <tr>
      <th>66</th>
      <td>Kungsfågel</td>
      <td>266.0</td>
    </tr>
    <tr>
      <th>103</th>
      <td>Rörhöna</td>
      <td>263.0</td>
    </tr>
    <tr>
      <th>63</th>
      <td>Kricka</td>
      <td>260.0</td>
    </tr>
    <tr>
      <th>41</th>
      <td>Gröngöling</td>
      <td>260.0</td>
    </tr>
    <tr>
      <th>57</th>
      <td>Kattuggla</td>
      <td>259.0</td>
    </tr>
    <tr>
      <th>69</th>
      <td>Ladusvala</td>
      <td>259.0</td>
    </tr>
    <tr>
      <th>151</th>
      <td>Tamduva</td>
      <td>258.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>Smådopping</td>
      <td>228.0</td>
    </tr>
    <tr>
      <th>92</th>
      <td>Ormvråk</td>
      <td>223.0</td>
    </tr>
    <tr>
      <th>74</th>
      <td>Mellanskarv</td>
      <td>200.0</td>
    </tr>
    <tr>
      <th>80</th>
      <td>Måsfåglar</td>
      <td>200.0</td>
    </tr>
    <tr>
      <th>75</th>
      <td>Mindre flugsnappare</td>
      <td>189.0</td>
    </tr>
    <tr>
      <th>64</th>
      <td>Kråka</td>
      <td>185.0</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Rödstjärt</td>
      <td>180.0</td>
    </tr>
    <tr>
      <th>157</th>
      <td>Trädgårdssångare</td>
      <td>178.0</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Enkelbeckasin</td>
      <td>168.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>Småskrake</td>
      <td>152.0</td>
    </tr>
    <tr>
      <th>140</th>
      <td>Svartmes</td>
      <td>150.0</td>
    </tr>
    <tr>
      <th>110</th>
      <td>Skedand</td>
      <td>137.0</td>
    </tr>
    <tr>
      <th>62</th>
      <td>Korp</td>
      <td>136.0</td>
    </tr>
    <tr>
      <th>134</th>
      <td>Strandskata</td>
      <td>129.0</td>
    </tr>
    <tr>
      <th>50</th>
      <td>Havsörn</td>
      <td>118.0</td>
    </tr>
    <tr>
      <th>138</th>
      <td>Svarthakedopping</td>
      <td>115.0</td>
    </tr>
    <tr>
      <th>171</th>
      <td>Ärtsångare</td>
      <td>111.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Bläsand</td>
      <td>106.0</td>
    </tr>
    <tr>
      <th>133</th>
      <td>Storspov</td>
      <td>104.0</td>
    </tr>
    <tr>
      <th>76</th>
      <td>Mindre hackspett</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Drillsnäppa</td>
      <td>98.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Brandkronad kungsfågel</td>
      <td>95.0</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Grå flugsnappare</td>
      <td>91.0</td>
    </tr>
    <tr>
      <th>49</th>
      <td>Havstrut</td>
      <td>77.0</td>
    </tr>
    <tr>
      <th>65</th>
      <td>Kungsfiskare</td>
      <td>76.0</td>
    </tr>
    <tr>
      <th>108</th>
      <td>Sjöorre</td>
      <td>75.0</td>
    </tr>
    <tr>
      <th>152</th>
      <td>Tofsmes</td>
      <td>73.0</td>
    </tr>
    <tr>
      <th>83</th>
      <td>Näktergal</td>
      <td>71.0</td>
    </tr>
    <tr>
      <th>77</th>
      <td>Mindre korsnäbb</td>
      <td>68.0</td>
    </tr>
    <tr>
      <th>156</th>
      <td>Trana</td>
      <td>65.0</td>
    </tr>
    <tr>
      <th>121</th>
      <td>Sparvhök</td>
      <td>59.0</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Duvhök</td>
      <td>59.0</td>
    </tr>
    <tr>
      <th>86</th>
      <td>Ob. ansergås</td>
      <td>56.0</td>
    </tr>
    <tr>
      <th>128</th>
      <td>Stenskvätta</td>
      <td>54.0</td>
    </tr>
    <tr>
      <th>163</th>
      <td>Törnsångare</td>
      <td>54.0</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Fasan</td>
      <td>53.0</td>
    </tr>
    <tr>
      <th>95</th>
      <td>Prutgås</td>
      <td>40.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Bläsgås</td>
      <td>40.0</td>
    </tr>
    <tr>
      <th>149</th>
      <td>Tallbit</td>
      <td>39.0</td>
    </tr>
    <tr>
      <th>39</th>
      <td>Grönbena</td>
      <td>36.0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Gransångare</td>
      <td>36.0</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Gråsiska</td>
      <td>35.0</td>
    </tr>
    <tr>
      <th>144</th>
      <td>Sävsparv</td>
      <td>32.0</td>
    </tr>
    <tr>
      <th>104</th>
      <td>Rörsångare</td>
      <td>31.0</td>
    </tr>
    <tr>
      <th>143</th>
      <td>Sädgås</td>
      <td>30.0</td>
    </tr>
    <tr>
      <th>170</th>
      <td>Ängspiplärka</td>
      <td>28.0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Dubbeltrast</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>112</th>
      <td>Skogssnäppa</td>
      <td>24.0</td>
    </tr>
    <tr>
      <th>160</th>
      <td>Trädpiplärka</td>
      <td>20.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Domherre</td>
      <td>17.0</td>
    </tr>
    <tr>
      <th>78</th>
      <td>Mindre strandpipare</td>
      <td>17.0</td>
    </tr>
    <tr>
      <th>145</th>
      <td>Sävsångare</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>79</th>
      <td>Morkulla</td>
      <td>14.0</td>
    </tr>
    <tr>
      <th>87</th>
      <td>Ob. bo-/bergfink</td>
      <td>14.0</td>
    </tr>
    <tr>
      <th>165</th>
      <td>Vattenrall</td>
      <td>14.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>Snösparv</td>
      <td>13.0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Entita</td>
      <td>13.0</td>
    </tr>
    <tr>
      <th>88</th>
      <td>Ob. fisk-/silvertärna</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>91</th>
      <td>Ob. skarv</td>
      <td>11.0</td>
    </tr>
    <tr>
      <th>54</th>
      <td>Järnsparv</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>47</th>
      <td>Gök</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Buskskvätta</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>51</th>
      <td>Hussvala</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>68</th>
      <td>Kärrsångare</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>44</th>
      <td>Gulsparv</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>137</th>
      <td>Större korsnäbb</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>52</th>
      <td>Hämpling</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>114</th>
      <td>Skräntärna</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>162</th>
      <td>Törnskata</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>48</th>
      <td>Göktyta</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Doppingfåglar</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>33</th>
      <td>Gråhakedopping</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Grågås x kanadagås</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>53</th>
      <td>Härmsångare</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Europeisk skata</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Brun kärrhök</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>161</th>
      <td>Tundrasädgås</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>45</th>
      <td>Gulärla</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>107</th>
      <td>Silvertärna</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>67</th>
      <td>Kustlabb</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Fiskgjuse</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>82</th>
      <td>Nordsjösilltrut</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>81</th>
      <td>Nordlig gulärla</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>72</th>
      <td>Lärkfalk</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>71</th>
      <td>Ljungpipare</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>89</th>
      <td>Ob. gås</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>122</th>
      <td>Spetsbergsgås</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>126</th>
      <td>Stenfalk</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>59</th>
      <td>Knipskrake</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>159</th>
      <td>Trädlärka</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>167</th>
      <td>Vinterhämpling</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>169</th>
      <td>Ägretthäger</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>164</th>
      <td>Varfågel</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bivråk</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>70</th>
      <td>Lappsparv</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Bändelkorsnäbb</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>135</th>
      <td>Strömstare</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Gravand</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>97</th>
      <td>Rosenfink</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>154</th>
      <td>Tornfalk</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>98</th>
      <td>Röd glada</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>99</th>
      <td>Rödbena</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Forsärla</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Fjällvråk</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Ejder</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>123</th>
      <td>Spillkråka</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>130</th>
      <td>Storlom</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>93</th>
      <td>Ormvråk, underarten buteo</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>90</th>
      <td>Ob. korsnäbb</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
species_komun = data2.loc[data2['Artnamn'] == 'Koltrast', ['Artnamn', 'Kommun']] #Filtering the data so that we are using only the most prelevamnt species

sns.countplot(species_komun, x = "Kommun")
plt.title("Koltrast in Each Municipality")

```




    Text(0.5, 1.0, 'Koltrast in Each Municipality')




    
![png](HW3_files/HW3_11_1.png)
    



```python
species_accuracy = data2.loc[data2['Artnamn'] == 'Koltrast', ['Artnamn', 'Noggrannhet']] #Filtering the data so that we are using only the most prelevamnt species

accuracy = species_accuracy.loc[:,"Noggrannhet"] # Filtering

mean_accuracy = np.mean(accuracy) #Calculating mean
round(mean_accuracy)
np.median(accuracy)
```




    197.0




```python
total_observations = sum(most_prevalent_sorted.loc[:,"Antal"])

observation_of_interest = most_prevalent_sorted[most_prevalent_sorted['Artnamn'] == 'Grönsiska']
observation_of_interest1 = observation_of_interest.loc[:, "Antal"]
percent = round(100 * observation_of_interest1 / total_observations)
percent 
```




    42    17.0
    Name: Antal, dtype: float64




```python

```

##### Monthly distribution




```python
fig, ax = plt.subplots(1, 3, figsize = (12, 6))
x = data2[data2['Artnamn'] == 'Grönsiska']['Startdatum'].astype('datetime64[ns]')
y = data2[data2['Artnamn'] == 'Grönsiska']['Antal']

y.groupby(x.dt.month_name(locale = 'English')).count().plot(kind =  'bar',
                                                            color = 'tab:green',
                                                            xlabel = 'Month',
                                                            ylabel =  'Quantity',
                                                            title = 'Monthly distribution for Grönsiska',
                                                            ax = ax[0])
x = data2[data2['Artnamn'] == 'Sothöna']['Startdatum'].astype('datetime64[ns]')
y = data2[data2['Artnamn'] == 'Sothöna']['Antal']
y.groupby(x.dt.month_name(locale = 'English')).count().plot(kind = 'bar',
                                                            color ='tab:blue',
                                                            xlabel = 'Month',
                                                            title = 'Monthly distribution for Sothöna',
                                                            ax = ax[1])
x = data2[data2['Artnamn'] == 'Gräsand']['Startdatum'].astype('datetime64[ns]')
y = data2[data2['Artnamn'] == 'Gräsand']['Antal']
y.groupby(x.dt.month_name(locale = 'English')).count().plot(kind =  'bar',
                                                            color = 'tab:red',
                                                            xlabel =  'Month',
                                                            title =  'Monthly distribution for Gräsand',
                                                            ax = ax[2])
```




    <Axes: title={'center': 'Monthly distribution for Gräsand'}, xlabel='Month'>




    
![png](HW3_files/HW3_16_1.png)
    


#### What are the most prevelant/rare species?

To find the most prelevant species one can simply sort and filter data in such a way that we have species in one column and number of species in other. One has then to sum up all the  From the plot one can se that the most prelevent species happens to be "Grönsiska" and the rearest species are "Ob. korsnäbb	". 

#### What are the monthly distrubution of 3 most prelevant species?


### Personal questions and answers

#### In what municipality are the Koltrast spicies prelevant?

    To answer this question we can make a count plot for the most prelevent species which is "Koltrast". 
    From the plot we can see that the most usual habitant for Koltrast is Stockholm kommun.
    
    
#### What is the mean accuracy for Koltrast?
    
    For this case one can create i dataframe with the most prelevent species and the accuracy values. 
    One can the easily calculate the accuracy by using the mean function and find out that its 265. 
    One should note that the mean is maybe not the best choise here because of the outliers. 
    The median = 197 might be a better choise
    
#### What is the ratio of the most prevalent species to the total number of observed species?
     To find this one can divide the total number of observed birds by the number of observed prelevant species. After doing 
     that we can see that its around 17 % 


```python

```

# Predicting Strokes


```python
data3 = pd.read_csv("stroke-data.csv")

data3
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
      <th>id</th>
      <th>gender</th>
      <th>age</th>
      <th>hypertension</th>
      <th>heart_disease</th>
      <th>ever_married</th>
      <th>work_type</th>
      <th>Residence_type</th>
      <th>avg_glucose_level</th>
      <th>bmi</th>
      <th>smoking_status</th>
      <th>stroke</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>9046</td>
      <td>Male</td>
      <td>67.0</td>
      <td>0</td>
      <td>1</td>
      <td>Yes</td>
      <td>Private</td>
      <td>Urban</td>
      <td>228.69</td>
      <td>36.6</td>
      <td>formerly smoked</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>51676</td>
      <td>Female</td>
      <td>61.0</td>
      <td>0</td>
      <td>0</td>
      <td>Yes</td>
      <td>Self-employed</td>
      <td>Rural</td>
      <td>202.21</td>
      <td>NaN</td>
      <td>never smoked</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>31112</td>
      <td>Male</td>
      <td>80.0</td>
      <td>0</td>
      <td>1</td>
      <td>Yes</td>
      <td>Private</td>
      <td>Rural</td>
      <td>105.92</td>
      <td>32.5</td>
      <td>never smoked</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>60182</td>
      <td>Female</td>
      <td>49.0</td>
      <td>0</td>
      <td>0</td>
      <td>Yes</td>
      <td>Private</td>
      <td>Urban</td>
      <td>171.23</td>
      <td>34.4</td>
      <td>smokes</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1665</td>
      <td>Female</td>
      <td>79.0</td>
      <td>1</td>
      <td>0</td>
      <td>Yes</td>
      <td>Self-employed</td>
      <td>Rural</td>
      <td>174.12</td>
      <td>24.0</td>
      <td>never smoked</td>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>5105</th>
      <td>18234</td>
      <td>Female</td>
      <td>80.0</td>
      <td>1</td>
      <td>0</td>
      <td>Yes</td>
      <td>Private</td>
      <td>Urban</td>
      <td>83.75</td>
      <td>NaN</td>
      <td>never smoked</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5106</th>
      <td>44873</td>
      <td>Female</td>
      <td>81.0</td>
      <td>0</td>
      <td>0</td>
      <td>Yes</td>
      <td>Self-employed</td>
      <td>Urban</td>
      <td>125.20</td>
      <td>40.0</td>
      <td>never smoked</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5107</th>
      <td>19723</td>
      <td>Female</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>Yes</td>
      <td>Self-employed</td>
      <td>Rural</td>
      <td>82.99</td>
      <td>30.6</td>
      <td>never smoked</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5108</th>
      <td>37544</td>
      <td>Male</td>
      <td>51.0</td>
      <td>0</td>
      <td>0</td>
      <td>Yes</td>
      <td>Private</td>
      <td>Rural</td>
      <td>166.29</td>
      <td>25.6</td>
      <td>formerly smoked</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5109</th>
      <td>44679</td>
      <td>Female</td>
      <td>44.0</td>
      <td>0</td>
      <td>0</td>
      <td>Yes</td>
      <td>Govt_job</td>
      <td>Urban</td>
      <td>85.28</td>
      <td>26.2</td>
      <td>Unknown</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>5110 rows × 12 columns</p>
</div>



#### Questions that gives good insight into the data:
* What is the distribution for the smoking status among people with heart disease?
* What is the ratio for heart decease amongs men and women?
* How does the smoking status differs depending on worktype?
To answer those question one can oobserve the following

#### What is the distribution for the smoking status among people with heart disease?
Lets filter our data first by the people that had the heart disease and the plot the smoking status for those
to see the distrubution.


```python
data3_cleaned = data3[data3['heart_disease'] == 1]

plt.figure(figsize=(8, 6))
sns.countplot(x= 'smoking_status', data=data3_cleaned)
plt.title(' Smoking status distribution for heart disease cases')
plt.xlabel(' Smoking status')
plt.ylabel(' count')

plt.show()
```


    
![png](HW3_files/HW3_23_0.png)
    


#### What is the ratio for heart decease amongs men and women?



```python
info = data3.loc[:,["gender", "heart_disease"]]

gender_heart_disease_counts = info.groupby(['gender', 'heart_disease']).size().reset_index(name='count')

men_data = gender_heart_disease_counts[gender_heart_disease_counts['gender'] == 'Male']
women_data = gender_heart_disease_counts[gender_heart_disease_counts['gender'] == 'Female']


ratio_men = round(men_data[men_data['heart_disease'] == 1]['count'].sum() / men_data['count'].sum(), 2) * 100
ratio_women = round(women_data[women_data['heart_disease'] == 1]['count'].sum() / women_data['count'].sum(),2) * 100


print("Ratio of heart disease for Men:", ratio_men, " %")
print("Ratio of heart disease for Women:", ratio_women, " %")
```

    Ratio of heart disease for Men: 8.0  %
    Ratio of heart disease for Women: 4.0  %
    

#### How does the smoking status differs depending on worktype?




```python
df_cleaned1 = data3.dropna(subset=['work_type', 'smoking_status'])


plt.figure(figsize=(12, 6))
sns.countplot(x='work_type', hue='smoking_status', data=df_cleaned1, palette='Set2')
plt.title('Distribution of Smoking Status by Work Type')
plt.xlabel('Work Type')
plt.ylabel('Count')
plt.legend(title='Smoking Status', bbox_to_anchor=(1.05, 1), loc='upper left')

plt.show()
```


    
![png](HW3_files/HW3_27_0.png)
    


We can see that for all 3 work sectors in this data set most people never smoked.


```python
!jupyter nbconvert --to markdown HW3.ipynb
```

    [NbConvertApp] Converting notebook HW3.ipynb to markdown
    [NbConvertApp] Support files will be in HW3_files\
    [NbConvertApp] Making directory HW3_files
    [NbConvertApp] Making directory HW3_files
    [NbConvertApp] Making directory HW3_files
    [NbConvertApp] Making directory HW3_files
    [NbConvertApp] Making directory HW3_files
    [NbConvertApp] Making directory HW3_files
    [NbConvertApp] Making directory HW3_files
    [NbConvertApp] Making directory HW3_files
    [NbConvertApp] Writing 34710 bytes to HW3.md
    


```python

```


```python

```
