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
