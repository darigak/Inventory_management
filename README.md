# Kings County Housing Project

The goal is to create a model that best predicts the prices of homes sold in the Seattle, WA area (Kings County). Column Names and descriptions for Kings County Data Set provided below.


## Repo organization

- **data_files** folder contains testing data, training data and predictions created using the final modeling process.

- **Modeling_process.ipynb** notebook contains the final modeling process.  

- **pickle_files** folder contains the final modeling coefficients and additional information.  

- **Predict_holdout.ipynb** notebook contains the prediction process using the final modeling coefficients.

- **images** folder contains images used in README.md.

- **Archive** folder contains prior versions of modeling process notebook.


## Modeling process

Begin analysis by reviewing correlation matrix between the dataset columns. With the threshold of 0.8, we can see that 'sqft_above' column is highly correlated with 'sqft_living' and can be removed from our analysis.

<p align="center">
   <img width="900" height="700" src=images/correlation.png>
</p> 

To account for extreme values, we need to cap the following columns:
- **sqft_living** at 8,000
- **sqft_lot** at 800,000
- **sqft_basement** at 2,000


Some properties have erroneous 0 bedroom and 0 bathroom information. To account for that, but not overwrite 0 bedrooms for studio apartments:
- set bedrooms equal to the number of floors minus 1 for properties with 0 bedrooms
- set bathrooms equal to the number of floors for properties with 0 bathrooms


To account for non-linear relationship, we need to transform the following columns into categorical variables:
- **condition** into low/mid/high
- **grade** into low/mid_1/mid_2/high
- **zipcodes** into zipcode groups
- **sqft_basement** into has basement or not
- **number of bedrooms** into 5&more and 2.5&less
- **number of bathrooms** into 2.75&more


Generate new feature called **"comp"** based on the following information: zipcode, 5&more bedrooms, 2.5&less bedrooms and 2.75&more bathrooms. Additionally, generate new features: **year sold**, **years since update** and **year built in relation to 1958**.


**The best model** starts with excluding grade, condition, zipcode, longitude and year sold columns. Then takes the second degree polynomial with no categorical interactions and selects 130 best features using F-test. In this case, 130 is chosen, becacuse it is approximately equal to the square root of the number of observations.


**The final list of the selected columns is**: 'bedrooms','bathrooms', 'sqft_living', 'floors', 'waterfront', 'view', 'sqft_basement', 'lat', 'sqft_living15', 'condition_text_low', 'grade_text_low', 'bedrooms^2', 'bedrooms bathrooms', 'bedrooms sqft_living', 'bedrooms sqft_lot', 'bedrooms floors', 'bedrooms waterfront', 'bedrooms view', 'bedrooms sqft_basement', 'bedrooms yr_built', 'bedrooms yr_renovated', 'bedrooms lat', 'bedrooms sqft_living15', 'bedrooms condition_text_low', 'bedrooms grade_text_low', 'bathrooms^2', 'bathrooms sqft_living', 'bathrooms sqft_lot', 'bathrooms floors', 'bathrooms waterfront', 'bathrooms view', 'bathrooms sqft_basement', 'bathrooms yr_built', 'bathrooms yr_renovated', 'bathrooms lat', 'bathrooms sqft_living15', 'bathrooms sqft_lot15', 'bathrooms condition_text_low', 'bathrooms condition_text_mid', 'bathrooms grade_text_low', 'sqft_living^2', 'sqft_living sqft_lot', 'sqft_living floors', 'sqft_living waterfront', 'sqft_living view', 'sqft_living sqft_basement', 'sqft_living yr_built', 'sqft_living yr_renovated', 'sqft_living lat', 'sqft_living sqft_living15', 'sqft_living sqft_lot15', 'sqft_living condition_text_low', 'sqft_living condition_text_mid', 'sqft_living grade_text_low', 'sqft_lot floors', 'sqft_lot waterfront', 'sqft_lot view', 'sqft_lot sqft_basement', 'sqft_lot sqft_living15', 'sqft_lot condition_text_low', 'sqft_lot grade_text_low', 'floors^2', 'floors waterfront', 'floors view', 'floors sqft_basement', 'floors yr_built', 'floors yr_renovated', 'floors lat', 'floors sqft_living15', 'floors condition_text_low', 'floors grade_text_low', 'waterfront^2', 'waterfront view', 'waterfront sqft_basement', 'waterfront yr_built', 'waterfront yr_renovated', 'waterfront lat', 'waterfront sqft_living15', 'waterfront sqft_lot15', 'waterfront condition_text_low', 'waterfront condition_text_mid', 'waterfront grade_text_low', 'view^2', 'view sqft_basement', 'view yr_built', 'view yr_renovated', 'view lat', 'view sqft_living15', 'view sqft_lot15', 'view condition_text_low', 'view condition_text_mid', 'view grade_text_low', 'sqft_basement^2', 'sqft_basement yr_built', 'sqft_basement yr_renovated', 'sqft_basement lat', 'sqft_basement sqft_living15', 'sqft_basement sqft_lot15', 'sqft_basement condition_text_low', 'sqft_basement condition_text_mid', 'sqft_basement grade_text_low', 'yr_built sqft_living15', 'yr_built condition_text_low', 'yr_built grade_text_low', 'yr_renovated sqft_living15', 'yr_renovated condition_text_low', 'lat^2', 'lat sqft_living15', 'lat condition_text_low', 'lat grade_text_low', 'sqft_living15^2', 'sqft_living15 sqft_lot15', 'sqft_living15 condition_text_low', 'sqft_living15 condition_text_mid', 'sqft_living15 grade_text_low', 'sqft_lot15 condition_text_low', 'condition_text_low^2', 'condition_text_low condition_text_mid', 'condition_text_low grade_text_low', 'grade_text_low^2', 'grade_text_mid_1', 'grade_text_mid_2', 'has_basement', 'zipcode_text_n_2', 'zipcode_text_n_3', 'zipcode_text_n_6', 'zipcode_text_n_7', 'bedrooms_5plus', 'bathrooms_2.75plus', 'bedrooms_2.5minus'.


# Column Names and descriptions for Kings County Data Set
* **id** - unique ID for a house
* **date** - Date day house was sold
* **price** - Price is prediction target
* **bedrooms** - Number of bedrooms
* **bathrooms** - Number of bathrooms
* **sqft_living** - square footage of the home
* **sqft_lot** - square footage of the lot
* **floors** - Total floors (levels) in house
* **waterfront** - Whether house has a view to a waterfront
* **view** - Number of times house has been viewed
* **condition** - How good the condition is (overall)
* **grade** - overall grade given to the housing unit, based on King County grading system
* **sqft_above** - square footage of house (apart from basement)
* **sqft_basement** - square footage of the basement
* **yr_built** - Year when house was built
* **yr_renovated** - Year when house was renovated
* **zipcode** - zip code in which house is located
* **lat** - Latitude coordinate
* **long** - Longitude coordinate
* **sqft_living15** - The square footage of interior housing living space for the nearest 15 neighbors
* **sqft_lot15** - The square footage of the land lots of the nearest 15 neighbors
