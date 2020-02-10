---
layout: post
title:  "Web Scraper"
date:   2020-02-04 22:30:18 -0500
---

I've written my first Python code with the help of [Real Python](https://realpython.com/beautiful-soup-web-scraper-python/ "Web Scraper With Python"). 
It's far from efficient but will attempt to imporve it in the futher.

```python

!/usr/bin/env python

#import the library used to query a website
#import the Beautiful soup functions to parse the data returned from the website
import requests
from bs4 import BeautifulSoup
from datetime import datetime

def main():

    # specify the url
    url = 'https://www.indeed.com/jobs?q=senior+network+engineer&l=New+York%2C+NY'

    # query the website and return the html to the variable ‘page’
    page = requests.get(url)

    # parse the html using beautiful soup and store in variable `soup`
    soup = BeautifulSoup(page.content, 'html.parser')

    table = soup.find('table', id='pageContent').find('td',id="resultsCol")
    #print(table.prettify())

    #use re.findall to get all the links
    job_elems = table.find_all('div', class_="jobsearch-SerpJobCard unifiedRow row result")

    # get current time
    today = datetime.now().strftime('%d%b%Y')
    # loop through job_elems and write the results to a file
    
    with open(f'jobs_{today}.txt', 'w') as file:
        for job_elem in job_elems:
            title_elem = job_elem.find('a', title=True)
            location_elem = job_elem.find('div', class_="recJobLoc")
            link_elem = job_elem.find('a', href=True)
            company_elem = job_elem.find('span', class_='company')
            
            file.write(title_elem.text.strip() + '\n')
            file.write(company_elem.text.strip()+ '\n')
            file.write(location_elem.get('data-rc-loc').strip()+ '\n')
            file.write('http://indeed.com/' + link_elem.get('href').strip()+ '\n')
            file.write('\n')

if __name__ == '__main__':
    main()
```
