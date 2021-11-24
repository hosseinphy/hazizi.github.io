# <em>E-com</em> Fitness web application 
#### Capstone project (The Data Incubator Fellowship) - August 2021

<p><em>E-com Fitness</em> is a web-based application designed to forecast fitness product sales using data extracted from social media and time-series analysis of historical data</p>

_______

### Objective
- Create a web-based application to forecast product sales using data extracted from social media and time-series analysis
     - buyers habit trends
     - Outputs potential profit (average predicted sales)     
     - Provides negative feedback, modify sales strategies to gain customer retention
     - product success or failure

### Methodology

1. Data extraction:       
    - Scraping data from social media (e.g., posts, comments, reactions…etc.)
    - Scraping product history
    - Utilize new web scraping tools (Octoparse), crawling from different APIs
    - Scraped 10000 Facebook posts/tweets; form 100 top fitness pages; 10000 sold products from last three months on Ebay.ca; historical data from last three year 
    for 1000 unique products on Walmart, Canadian Tire, and Best buy
    Handling blocking and scrape from ajax websites


2. Data processing:
    - Analyze sentiments of social media feedback (map text to numerical values using an appropriate sentiment analysis algorithm)
    - Generate a dataset from (numerical) positive/negative/neutral feedbacks in time 
    - Adding appropriate features (e.g., timestamps) using explanatory data analysis    
    - Data cleansing for tabulated data
     * start with static data
    - Data ingestion using spark
    - Data validation (completeness, uniqueness and compliance with data constraints) ***
    

3. Construct a predictive model:
    - Train and benchmark ML-based algorithms (Random forest, Decision tree, ...) 
        - Train the model efficiently (GPU)
    - Feature engineering 
    - Cross validation
    - Run the trained model on a test data

4. Data visualizations
    - map of consumer satisfaction with a product
    - Display correlation between product profitability and consumer demographics
    - illustrate the implications of the pandemic (restrictions, curfew, COVID vaccination)
  

5. Model presentation and results
    - on an interactive website; deploying on Heroku using Flask

- Create a web-based app that utilizes customer feedback as well as tabulated data to accurately (?%) predict sales of a given product 
