# <center> SCRAPING WEBSITE DATA WITH PYTHON <center>

### <center> For this project i'll be using a Real Estate website to scrap data. <center>


```python
import requests
from bs4 import BeautifulSoup
```

# TO SCRAP ONE PAGE DATA ONLY


```python
l=[]
base_url = "https://www.century21.com/real-estate/austin-tx/LCTXAUSTIN/?p="
for page in range(1,30):        # to ilterate through all the pages
    r = requests.get(base_url+str(page))
    c = r.content
    soup = BeautifulSoup(c,"html.parser")
    all = soup.find_all("div",{"class":"property-card"})
    for item in all:
        d={}
        d["Price"] = item.find("a",{"class","listing-price"}).text.replace("\n","").replace(" ","") #price
        d["Address"] = item.find("div",{"class","property-address"}).text.replace("\n","").replace(" ","") #address
        d["City"] = item.find("div",{"class","property-city"}).text.replace("\n","").replace(" ","") # City
        try:
            d["bed"] = item.find("div",{"class","property-baths"}).find("strong").text.replace("\n","").replace(" ","") # bed
        except:
            d["bed"] = None
        try:
            d["bath"] = item.find("div",{"class","property-baths"}).find("strong").text.replace("\n","").replace(" ","") # bath
        except:
            d["bath"] = None
        try:
            d["SQFT"] = item.find("div",{"class","property-sqft"}).text.replace("\n","").replace(" ","") # square.ft
        except:
            d["SQFT"] = None

        l.append(d)
    
```

#### Now, arrange this data in pandas dataframe to export as a CV file


```python
len(l)
```




    353



#### So, We've scraped 352 Rows of data from the website

#### Now to export this data in the form of CSV file we use Pandas dataframe


```python
import pandas as pd
```


```python
df = pd.DataFrame(l)
```


```python
df
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
      <th>Price</th>
      <th>Address</th>
      <th>City</th>
      <th>bed</th>
      <th>bath</th>
      <th>SQFT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>$235,000</td>
      <td>512Eberhart#206</td>
      <td>AustinTX78745</td>
      <td>1</td>
      <td>1</td>
      <td>832sq.ft</td>
    </tr>
    <tr>
      <th>1</th>
      <td>$479,000</td>
      <td>10900MickelsonDr</td>
      <td>AustinTX78747</td>
      <td>3</td>
      <td>3</td>
      <td>None</td>
    </tr>
    <tr>
      <th>2</th>
      <td>$325,000</td>
      <td>11929GaelicDrive</td>
      <td>AustinTX78754</td>
      <td>2</td>
      <td>2</td>
      <td>None</td>
    </tr>
    <tr>
      <th>3</th>
      <td>$620,000</td>
      <td>12708TierraGrandeTrail</td>
      <td>AustinTX78732</td>
      <td>2</td>
      <td>2</td>
      <td>2,002sq.ft</td>
    </tr>
    <tr>
      <th>4</th>
      <td>$650,000</td>
      <td>1819PiedmontAvenue</td>
      <td>AustinTX78757</td>
      <td>2</td>
      <td>2</td>
      <td>None</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>348</th>
      <td>$105,000</td>
      <td>14502HuntersPASS</td>
      <td>AustinTX78734</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>349</th>
      <td>$95,000</td>
      <td>4102LowerDR</td>
      <td>AustinTX78725</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>350</th>
      <td>$95,000</td>
      <td>3802LowerDR</td>
      <td>AustinTX78725</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>351</th>
      <td>$95,000</td>
      <td>2502DouglasST</td>
      <td>AustinTX78741</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>352</th>
      <td>$80,000</td>
      <td>4808BrookCreekCV</td>
      <td>AustinTX78744</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
  </tbody>
</table>
<p>353 rows Ã— 6 columns</p>
</div>




```python
df.to_csv("Output_data.csv")
```

## Great :)

# PROJECT BY @YASIRKHANA


```python

```
