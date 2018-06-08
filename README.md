# Python
Notes on the Python programming language

To add:  
+ file open/file close

### Python for Data Science Class notebooks:  
https://github.com/luonglearnstocode/python-4-data-science  
 - Original class: https://www.edx.org/course/python-data-science-uc-san-diegox-dse200x  
### Python for Machine Learning Bootcamp notebooks:  
https://github.com/juinc/python_data_science_and_machine_learning_bootcamp  
 - Original class: https://www.udemy.com/python-for-data-science-and-machine-learning-bootcamp/  


#### printing to line  
Interesting method, uses curly braces to call variables later in line - useful if using the same variable more than once, and use temp variables names  
``` python  
print('My number is: {one}, and my name is: {two}'.format(one=num,two=name))  
```  

#### Dictionaries
Can use for lookups, reference 
 - items in the dict can be lists that can be called by reference  
   - interesting possible use for lookups/cross references  
 ``` python
d = {'key1':'item1','key2':'item2'}  
d['key1'] #returns 'item1'  
  
d = {'key1':[1,2,3],'key2':'item2'}
d['key1'][1] #returns 1  
#Interesting uses
d.keys()
d.items()
d.values()

 ```

### Map function  
Performs a function on a range instead of using a loop  
``` python
def square(var):  
 return var**2  
nums = [1,2,3,4]
#to create a new list, where the function has been applied to the whole range of the first list
sqnums = list(map(square,nums))

```

### Lambda Function
 - AKA anonymous function
 - Allows to create a function on the fly
``` python
#using same example as map above
nums = [1,2,3,4]
sqnums = list(map(lambda num: num**2,nums))
```
 ### Filter Function
 - Allows to quickly filter out certain values
 - Requires a True/False criteria to test
 ``` python
 seq = [1,2,3,4,5]
 #to return only 2 and 4, ie modulus is 0
 list(filter(lambda item: item%2 == 0,seq))
 ```

### Beautiful Soup, read from web page, writing to csv  
Below notes on Beautiful Soup and writing to csv cribbed from this link and modified  
https://medium.freecodecamp.org/how-to-scrape-websites-with-python-and-beautifulsoup-5946935d93fe
``` python
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
 
 Alternatively, there may be more than one entry and need to put results into a list (array)
 ``` python
Containers = page_soup.findall(“div”,{“class”:”item-container”})

#Then can work with a certain entry, or loop through all
Container = Containers[0]

#Once have a specific container, run through tags like:
Container.div.div.a.img
#Then attributes like:
Attribute_title = Container.div.div.a.img[“title”]

#To find something by class name:, in this case “item-title”:
Title_container = container.findAll(“a”, {“class”:”item-title”})
#Then to get the actual on screen text
Title_container[0].text
 ```
 
 also can modify the above with a **__loop__**
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


### Basic Functions  
can be in same module or separate imported module
``` python
def lastFirst(firstName, lastName):
    separator = ', '
    result = lastName + separator + firstName
    return result
    
def f(x):
    return x*x
```

### This is a good data method, turnig categorics variables into Dummy variables  
cribbed from: https://github.com/juinc/python_data_science_and_machine_learning_bootcamp/blob/master/Machine%20Learning%20Sections/Decision-Trees-and-Random-Forests/Decision%20Trees%20and%20Random%20Forest%20Project%20-%20Solutions.ipynb  
"In[36]" is where it starts - have a pandas dataframe "loans" with "purpose" as a categorical variable  
Creates a "final_data" dataframe with new category flags  
``` python
cat_feats = ['purpose']
final_data = pd.get_dummies(loans,columns=cat_feats,drop_first=True)
```





### NumPy  
NumPy arrays work intuitively like spreadsheets. 
 - There are also plenty ot functions to seed them with values
   - random numbers, normal distribution, random within a range, a series of evenly spaced numbers
   - can easily get min/max and/or their locations
 - note arrays start at [0,0]   
``` python
# to reference a 2d array, can use two types of reference
arr[1][2]
#or
arr[1,2]
```

possible interesting course series:  
https://www.coursera.org/specializations/python#about  

### Regression
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

# Jupyter   
Shift-Enter: runs that cell  
Alt-Enter: Inserts a cell below the current cell  
Navigate to directory you want to start from before starting jupyter notebook   


