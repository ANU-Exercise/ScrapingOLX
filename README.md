# PricePredict_ScrapingOLX
This project is an exercise project to improve my skill to scrape data from e-commerce / website. After get the data, I will do data cleaning, EDA, and machine learning for predicting.

# Web Scraping

### The Plan
For this web scraping, I will try to extract mercedes benz used car data (specification and price) from https://olx.co.id. I will use beautifulsoup as the tool to extract olx html. This web scraping is multipage web scraping. From the "mercedes benz" search results, I will extract the title, price, and link to item specifications. After I get them, I will use the link from each of extracted datas to direct me to item pages to get the car specifications like year, km, varian, model, etc.

### About The Data
##### Mercedes Benz Search Result Page
Form the result pages, there is noted that olx has 1978 mercedes benz used car data. At the result page, we could see that each page has 20 items / cars. So, olx may has around 99 pages of mercedes benz used car. Each of item box, will direct us to items page that has detail / car specification. If the items do not have title/price/link they will not be extracted. The following below is olx mercedes benz search result page :
<center><img src="https://github.com/agunggnug/PricePredict_ScrapingOLX/blob/master/Pictures/Screen%20Shot%202020-06-03%20at%2009.48.54.png?raw=true" alt="" width="950" height="550"></center>

##### Mercedes Benz Item Page
At the item page we could find detail which means car specification. From this specifications, I will not take all of them. I only need to take some specifications which are 'Merek','Varian', 'Model', 'Tahun', 'Jarak tempuh', 'Tipe bahan bakar', 'Warna', 'Transmisi', and 'Kapasitas mesin'. If the item doesn't have all of that specifications, that item will not be extracted. The following below is olx car detail or specification page :
<center><img src="https://github.com/agunggnug/PricePredict_ScrapingOLX/blob/master/Pictures/Screen%20Shot%202020-06-03%20at%2009.51.11.png?raw=true" alt="" width="950" height="550"></center>