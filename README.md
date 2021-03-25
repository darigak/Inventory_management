<p align="center">
   <img src='images/adi-goldstein-Hli3R6LKibo-unsplash.jpg'
>
</p>


# Inventory management for Etsy small business

A small business selling party supplies on Etsy needs help managing their inventory. They asked to review their sales for 2020 calendar year and analyze shop's top selling categories. The goal is to create a model that best forcasts quantities of each category sold 6 months in advance. 

1/1/2020 - 12/13/2020 sales data was provided by the small business owner. Additionally, detailed item descriptions were obtained from Etsy API.

Let's focus our analysis on category 1 for this part of the project.

# Methods

Time series analysis was used to order to predict the real estate prices.

1. For California, the best time series model is ARIMA(order=3,1,2)

2. For New York, the best time series model is ARIMA(order=0,1,2)

3. For Texas, the best time series model is ARIMA(order=1,1,1)

It is worth noting that during the train-test split analysis CA prediction was underestimated by 28.42%, NY prediction was underestimated by 14.64%, and TX prediction was underestimated by 20.17%.

# Results

<p align="center">
   <img src='images/RMSE_comparison.jpeg'
>
</p>   
    
#### 5-year investment example:
    1. CA: with initial investment of $746,329, in 5 years it is predicted to grow up to $774,866
        resulting in 3.82% return on investment
    2. NY: with initial investment of $384,161, in 5 years it is predicted to grow up to $443,348
        resulting in 15.41% return on investment
    3. TX: with initial investment of $198,030, in 5 years it is predicted to grow up to $239,229
        resulting in 20.8% return on investment
    
# Conclusions
Overall, I recommend investing in NY and TX homes over CA. Those states have lower home prices and higher expected returns. Although, please keep in mind that these predictions are averages for the whole state and are not expected to accurately predict by individual cities. Additionally, during the train-test split analysys, CA prediction was underestimated by 28.42%. Thus, it is possible for CA homes to have higher than predicted returns.

# Next Steps
- Update the dataset up to the current date
- Shift focus from states to cities or zip codes
- Add more models, such as SARIMA and/or SARIMAX

# Repository Structure
- **data** folder contains Zillow Research dataset.

- **images** folder contains images used in README.md and presentation.

- **Forecasting_real_estate_prices_presentation.pdf** contains the final presentation.

- **notebook_Final.ipynb** notebook contains the final modeling process.