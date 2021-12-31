# Collecting-Data-Using-Web-Scrapping-Lab
Hands-on Lab : Web Scraping
Estimated time needed: 30 to 45 minutes

Objectives
In this lab you will perform the following:

Extract information from a given web site
Write the scraped data into a csv file.
Extract information from the given web site
You will extract the data from the below web site:

#this url contains the data you need to scrape
url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DA0321EN-SkillsNetwork/labs/datasets/Programming_Languages.html"
The data you need to scrape is the name of the programming language and average annual salary.
It is a good idea to open the url in your web broswer and study the contents of the web page before you start to scrape.

Import the required libraries

# Your code here
from bs4 import BeautifulSoup
import requests
import pandas as pd
Download the webpage at the url

#your code goes here
url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DA0321EN-SkillsNetwork/labs/datasets/Programming_Languages.html"
Create a soup object

#your code goes here
data = requests.get(url).text
soup = BeautifulSoup(data, "html5lib")
Scrape the Language name and annual average salary.

#your code goes here
table = soup.find('table')
for row in table.find_all('tr'):
    cols = row.find_all('td')
    language_name = cols[1].getText()
    annual_average_salary = cols[3].getText()
    print("{}--->{}".format(language_name,annual_average_salary))
    
import pandas as pd
table_rows = table.find_all('tr')
l = []
for row in table.find_all('tr'):
    cols = row.find_all('td')
    language_name = cols[1].getText()
    average_salary = cols[3].getText()
    l.append({"Language Name":language_name,"Average Salary":average_salary})
df=pd.DataFrame(l, columns=["Language Name","Average Salary"])
df
Language--->Average Annual Salary
Python--->$114,383
Java--->$101,013
R--->$92,037
Javascript--->$110,981
Swift--->$130,801
C++--->$113,865
C#--->$88,726
PHP--->$84,727
SQL--->$84,793
Go--->$94,082
Language Name	Average Salary
0	Language	Average Annual Salary
1	Python	$114,383
2	Java	$101,013
3	R	$92,037
4	Javascript	$110,981
5	Swift	$130,801
6	C++	$113,865
7	C#	$88,726
8	PHP	$84,727
9	SQL	$84,793
10	Go	$94,082
