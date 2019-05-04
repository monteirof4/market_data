# Market Data - ETL Project

## Summary
We are providing an ELT pipeline that enables Investment Analysts to make investment decisions on OTCmarkets listed companies.  We utilize a CSV of ALL listed companies that was provided by the Exchange, scraping the OTC markets web page for companies with the most actively traded companies, and finally scraping Yahoo Finance for some key metrics.

This data is going to be stored in a noSQL database (mongoDB) to allow for quick updates with minimal chances for conflicting data.  Since everything can be re-run on a daily basis we can quickly drop and generate new DBs using mongoDB to store only most recent/relevant information.

![Database_Diagram](img/OTC_market_db_diagram.png)

## Data Sources:
OTCmarkets.com
Yahoo Finance

## Extraction
- Data will be scraped from OTC ticker listing page 
- Link: https://www.otcmarkets.com/market-activity/current-market/ALL/active/)

    - Scraping this will require utilizing Selenium to click "MORE" to display all Tickers in one large table
    - From this table we will extract the Exchange the Ticker is listed on as well as the Ticker itself
    - Hardcoded extraction of 4,000 companies as well as only looking at the OTC companies listed on the OTC QX and OTC QB exchanges, as those are more reputable exchanges (https://www.otcmarkets.com/corporate-services/get-started)
    - The focus will be the most actively traded companies that are displayed as of the date the data is being scraped

- Using this data, we will run queries using Yahoo Finance to search for the top stories and key metrics
- Summary Link: https://finance.yahoo.com/quote/'TICKER'
    - From the Summary Link we will gather Key Metrics
        - Close Price
        - Average 3 Month Daily Trading Volume
        - Market Cap
        - Beta
        - Price to Earnings Ratio
        - 1 Year Price Estimate
        - Latest news link
        - Latest news article Header

- Profile Link: https://finance.yahoo.com/quote/'TICKER'/profile?p='TICKER'
    - From the Profile Link we will gather:
        - Sector
        - Industry
        - Number of Full-Time employees 

## Transforming
- The extracted ticker Symbols from OTCmarkets are going to be used in the Yahoo Finance scraper to prompt that scraper on what ticker Symbols to scrape key data from Yahoo Finance
- Within the Yahoo Finance web scraping file, we had to transform numerous datapoints to allow us to extract and store this data in a standardized format that will allow this data to be utilized in any way analysts desire
    - For example:
        - Converting Strings into Floats
        - Creating a new value for Market Cap as it was displayed as 151M, to denote 151000000, so removing commas, removing letters, and applying scaling
        - Dealing with Null values, requiring numerous try/except loops throughout so that the scraper will not be interrupted 


## Loading
- These combined tables will then be stored in a noSQL(mongoDB) database as it will be structured data that will be quickly queryable to return to analysts what they need to make investment decisions

- Utilizing this information our clients will be able to quickly assess the quality of the various OTC exchanges to make decisions on what companies to invest in


### Instructions to Run ETL Processes
1-Install Selenium (Reference Selenium_Installation.md in the Repo for instructions on this)
2-Start MongoDB database (mongod)
3-Open Terminal
    a-source activate PythonData
    b-Open jupyter notebook
4-Run notebooks in the order below
    a-OTC_market_scraper.ipynb
    b-OTC_market_csv_import.ipynb
    c-OTC_market_yahoo_scraper.ipynb
        - In this final Notebook on line 2 in the "Scrape Yahoo Page" block of code you can adjust how many companies you want the code to scrape, just the variable 'number_of_companies_to_run' needs to be adjusted
