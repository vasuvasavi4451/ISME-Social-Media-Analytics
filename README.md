# ISME-Social-Media-Analytics
import requests
from bs4 import BeautifulSoup
base_url="https://www.amazon.in/s?k="
search_query="boat+headsets"   ### my product is boat headsets
url= base_url+search_query
print(url)
search_response=requests.get(url)        ## status code 503 means amazon allows us to do scrapping
search_response.status_code
header={'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.70 Safari/537.36'}
search_response=requests.get(url,headers=header) 
search_response.status_code
def getAmazonSearch(search_query):
    url="https://www.amazon.in/s?k="+search_query
    print(url)
    page=requests.get(url,cookies=cookie,headers=header)
    if page.status_code==200:
        return page        ### creating function for the query(pass in to the getAmazonSearch function) 
    else:
        return "Error"
    #print(page.content)
    search_response=getAmazonSearch("boat+headsets")
    soup=BeautifulSoup(search_response.content) 
    soup.prettify 
    soup.find("span",attrs={'class':"a-size-medium a-color-base a-text-normal"})  
    product_list_tag=soup.findAll("span",attrs={'class':"a-size-medium a-color-base a-text-normal"})
    product_list_tag
    data_asin=[]
response=getAmazonSearch('boat+headsets')       ### for loop for data_asin of the product 
#beautifulsoup is a package
soup=BeautifulSoup(response.content)
for i in soup.findAll("div",{'class':"sg-col-20-of-24 s-result-item sg-col-0-of-12 sg-col-28-of-32 sg-col-16-of-20 sg-col sg-col-32-of-36 sg-col-12-of-16 sg-col-24-of-28"}):
     data_asin.append(i['data-asin'])
     data_asin 
     def foot(search_query):
    url="https://www.amazon.in/dp/"+search_query
    print(url)
    page=requests.get(url,cookies=cookie,headers=header)
    if page.status_code==200:###  get url if amazon page has content it prints
        return page
    else:
        return "Error"
    #print(page.content)
    link=[]
for i in range(len(data_asin)-1):    ## foot function pass data_asin value and get response
    response=foot(data_asin[i+1])   ## for loop foe all review links
#beautifulsoup is a package          ### review of the product ### pass class tag and a of the product and 
    soup=BeautifulSoup(response.content)
    for i in soup.findAll("a",{'data-hook':"see-all-reviews-link-foot"}):
        link.append(i['href'])
     def review(search_query):                     
    url="https://www.amazon.in"+search_query       ## review function pass serch_query
    #print(url)                                      ### get url
    page=requests.get(url,cookies=cookie,headers=header)   ### request to the amazon server
    if page.status_code==200:
        return page
    else:
        return "Error"
        
   revi=[]
for j in range(len(link)):
    for k in range(75):      ## for loop for review body(description)
        response=review(link[j]+'&pageNumber='+str(k))     ### pass link and page number  through review
#beautifulsoup is a package
        soup=BeautifulSoup(response.content)
        for i in soup.findAll("span",{'data-hook':"review-body"}):   ## class tag of the review body
            revi.append(i.text)
 len(revi) 
 import pandas as pd
r={'reviews':revi}       ###create dataframe
df=pd.DataFrame.from_dict(r)
df.to_csv('vasavi_web_scrapping.csv',index=False) 
len(df)

        
  
