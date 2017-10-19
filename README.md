# rankwatch17_py_scraping

import urllib2
import csv
from bs4 import BeautifulSoup

url1='https://www.babynamesdirect.com'
page=urllib2.urlopen(url1)      #return html to variable page 
soup=BeautifulSoup(page,'html.parser')      #parse the html in 'page' and store in variable 'soup'
all_link=soup.find_all("a")     #find all links within page 

with open("abc.csv",'wb') as myfile:     #open csv file in write mode
    wr=csv.writer(myfile,delimiter=',',quoting=csv.QUOTE_MINIMAL)
    wr.writerow(['NAME','GENDER'])
    for link in all_link:
        if link.has_attr('class') and link['class'][0]=='boy':  #if in the class in link is boy
            name=link.text
            gender='boy'
            wr.writerow([name,gender])
        
        elif link.has_attr('class') and link['class'][0]=='girl':   #if the class in link is girl
            name=link.text
            gender='girl'
            wr.writerow([name,gender])
