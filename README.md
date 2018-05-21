# Python
Notes on the Python programming language

To add:
+ Beautiful soup techniques
+ array handling
+ loop handling
+ write to csv
+ getting data from webpage
+ file open/file close

Below notes on Beautiful Soup and writing to csv cribbed from this link and modified

https://medium.freecodecamp.org/how-to-scrape-websites-with-python-and-beautifulsoup-5946935d93fe
```python
# import libraries
import urllib2
import csv
from datetime import datetime
from bs4 import BeautifulSoup as soup

# specify the url
quote_page = ‘http://www.bloomberg.com/quote/SPX:IND'

# query the website and return the html to the variable ‘page’
page = urllib2.urlopen(quote_page)

# parse the html using beautiful soup and store in variable `soup_page`
soup_page = soup(page, ‘html.parser’)

# Take out the <div> of name and get its value
name_box = soup_page.find(‘h1’, attrs={‘class’: ‘name’})
name = name_box.text.strip()
# get the index price
price_box = soup_page.find(‘div’, attrs={‘class’:’price’})
price = price_box.text


# open a csv file with append, so old data will not be erased
with open(‘index.csv’, ‘a’) as csv_file:
 writer = csv.writer(csv_file)
 writer.writerow([name, price, datetime.now()])
```
 
 also can modify the above with a loop
``` python
#array of urls, can import from a file as well
quote_page = [‘http://www.bloomberg.com/quote/SPX:IND', ‘http://www.bloomberg.com/quote/CCMP:IND']
# for loop
data = []
for pg in quote_page:
 # query the website and return the html to the variable ‘page’
 page = urllib2.urlopen(pg)
# parse the html using beautiful soup and store in variable `soup_page`
 soup_page = soup(page, ‘html.parser’)
# Take out the <div> of name and get its value
 name_box = soup_page.find(‘h1’, attrs={‘class’: ‘name’})
 name = name_box.text.strip() # strip() is used to remove starting and trailing
# get the index price
 price_box = soup_page.find(‘div’, attrs={‘class’:’price’})
 price = price_box.text
# save the data in tuple
 data.append((name, price))
```


Basic Functions - can be in same module or separate imported module
``` python
def lastFirst(firstName, lastName):
    separator = ', '
    result = lastName + separator + firstName
    return result
    
def f(x):
    return x*x
```

possible interesting course series:
https://www.coursera.org/specializations/python#about

Some details on regression in Python:
https://medium.com/@dhwajraj/python-regression-analysis-part-4-multiple-linear-regression-ed09a0c31c74
Decent step by step breakdown and explanantion of results:
https://blog.datarobot.com/ordinary-least-squares-in-python
usage examples:
https://github.com/statsmodels/statsmodels/blob/master/examples/python/ols.py
nice scatterplot creation example:
https://lectures.quantecon.org/py/ols.html

Excellent walkthrough:
http://blog.rtwilson.com/regression-in-python-using-r-style-formula-its-easy/

below notes from the rtwilson notes above and this one:
https://www.learndatasci.com/tutorials/predicting-housing-prices-linear-regression-using-python-pandas-statsmodels/
``` python
import pandas as pd
import numpy as np

#need to create dataframe "df" first
root = 'https://raw.githubusercontent.com/LearnDataSci/article-resources/master/Housing%20Price%20Index%20Regression'

housing_price_index = pd.read_csv(root + '/monthly-hpi.csv')
unemployment = pd.read_csv(root + '/unemployment-macro.csv')
federal_funds_rate = pd.read_csv(root + '/fed_funds.csv')
shiller = pd.read_csv(root + '/shiller.csv')
gross_domestic_product = pd.read_csv(root + '/gdp.csv')

# merge dataframes into single dataframe by date
df = (shiller.merge(housing_price_index, on='date')
                    .merge(unemployment, on='date')
                    .merge(federal_funds_rate, on='date')
                    .merge(gross_domestic_product, on='date'))
                    
#to preview dataframe
df.head()

#to view correlations between columns
df.corr()

# again, invoke statsmodel's formula API using the below syntax
housing_model = ols("""housing_price_index ~ total_unemployed 
                                            + long_interest_rate 
                                            + federal_funds_rate
                                            + consumer_price_index 
                                            + gross_domestic_product""", data=df).fit()
# summarize our model
housing_model_summary = housing_model.summary()
HTML(housing_model_summary.as_html())

#can get specific results from model
housing_model.rsquared
housing_model.params #gives x coefficients, intercept
#create new predictions
housing_model.predict({'variable':value, 'variable':'value', .....})
```


