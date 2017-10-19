# rankwatch17_py_scraping

import urllib2
import csv
from bs4 import BeautifulSoup

url1='https://www.babynamesdirect.com'
# return html to variable page
page=urllib2.urlopen(url1)
# parse the html in 'page' and store in variable 'soup'
soup=BeautifulSoup(page,'html.parser') 
# find all links within page
all_link=soup.find_all("a")      

# open csv file in write mode
with open("abc.csv",'wb') as myfile:
    wr=csv.writer(myfile,delimiter=',',quoting=csv.QUOTE_MINIMAL)
    wr.writerow(['NAME','GENDER'])
    for link in all_link:
        # if in the class in link is boy
        if link.has_attr('class') and link['class'][0]=='boy': 
            name=link.text
            gender='boy'
            wr.writerow([name,gender])
        
        # if the class in link is girl
        elif link.has_attr('class') and link['class'][0]=='girl':  
            name=link.text
            gender='girl'
            wr.writerow([name,gender])
