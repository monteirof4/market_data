# Market Data - ETL Project

## Data Sources:
OTCmarkets.com
Yahoo Finance

## Extraction
- Data will be scraped from OTC ticker listing page 
- Link: https://www.otcmarkets.com/market-activity/current-market/ALL/active/)

    - Scraping this will require utilizing Splinter to click "More" to display all Tickers in one large table
    - From this table we will extract the Exchange the Ticker is listed on as well as the Ticker itself

- Using this data we will run queries using Yahoo Finance to search for the top stories
- Summary Link: https://finance.yahoo.com/quote/'TICKER'
    - From the Summary Link we will gather Key Metrics
        - Close Price
        - Average 3 Month Daily Trading Volume
        - Market Cap
        - Beta
        - Price to Earnings Ratio
        - 1 Year Price Estimate

- Profile Link: https://finance.yahoo.com/quote/'TICKER'/profile?p='TICKER'
    - From the Profile Link we will gather the Sector and Industry of each company 

## Transforming
- The tables of Ticker and OTC Exchange will then be combined with the financial data extracted from Yahoo Finance to paint a full picture of the ~18,000 companies on OTC markets

## Loading
- These combined tables will then be stored in a mySQL database as it will be structured data that will be quickly queriable to return to analysts what they need to make investment decisions

- Utilizing this information our clients will be able to quickly assess the quality of the various OTC exchanges to make decisions on what companies to invest in





