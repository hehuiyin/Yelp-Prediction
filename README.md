# Yelp-Prediction

## Background and Business Implication 

Yelp is a Multinational Corporation that publishes online reviews and ratings for many businesses since its foundation in 2004. With around 178 million unique users per month, Yelp has created tons of valuable information for both the business and individuals globally.

With the increases of Yelp users, we would like to help Yelp to improve their application and help the new businesses to increase their visibility in the app. As Yelp users ourselves, we wonder how Yelp assigns the dollar sign to the businesses. Based on the research we did online, we found out that the dollar sign is assigned based on users’ answers on how much they spend on the restaurant per person through the survey questions that pop out when users check in or after they drop a review. Yelp's formula in assigning dollar sign is: $= under $10, $$= $11-30, $$$= $31- 60, $$$$= over $61.

We found out that some new businesses don't have dollar signs which inspires us to make a prediction model to predict the dollar sign for the new businesses so that it will increase the visibility of these new businesses when users are filtering by dollar sign and improve Yelp’s app.

We also noticed that most of the expensive restaurants in Southern California are located in the expensive housing property areas (e.g. Beverly Hills, Laguna Beach, Newport Beach). We want to see if housing price is also an important attribute in affecting the yelp dollar sign so we combined the Yelp and Zillow dataset in this analysis. 

Through the project, we can help:
1. Yelp: this will help them improve their app. 

2.  New Businesses on yelp: the prediction will create more visibility by assigning dollar sign for the new businesses to make them filterable (by dollar sign).

#### Goal
To predict the restaurant pricing based on housing prices and other restaurant features and find out what kind of features are more
important in predicting the restaurant pricing.

## Data
1. Yelp API: https://www.yelp.com/dataset

 * The geographical focus for our analysis is focued on the restaurants in the U.S. After filtering on only the US restaurants, we ended up with a total of 38,261 rows and 14 columns. We first performed data pre-processing on this dataset, including:
    + convert the json format 
    + dummy the categorical attributes
    + pick the relevant categories

2. Zillow API: https://www.zillow.com/research/data/

 * The data pre-processing on this dataset includes:
  + create housing dollar signs: standardize the housing prices to make housing prices and restaurant dollars comparable by calculating the percentiles of housing prices for each state 
    + 1: 0 – 25% 
    + 2: 25% - 50% 
    + 3: 50%-75%
    + 4: 75% & above

3. Combined two dataset based on zipcode

## Modeling

### Model 1. Naive Bayes

<img width="497" alt="Screen Shot 2021-08-28 at 16 10 30" src="https://user-images.githubusercontent.com/73683982/131233155-8948fe5b-8837-4ec1-81cc-3050cb9b0e0d.png">


### Model 2. Random Forest

<img width="516" alt="Screen Shot 2021-08-28 at 16 10 42" src="https://user-images.githubusercontent.com/73683982/131233165-cb0bb1ce-9d1b-4e77-9536-cd04e2ff9ffc.png">

Random Forest works better with our data. Next, we can find out the Features Importance Score for the Random Forest model to see the importance of each attributes on our prediction result.

<img width="818" alt="Screen Shot 2021-08-28 at 16 12 33" src="https://user-images.githubusercontent.com/73683982/131233211-0e87f321-5163-4a5f-89ff-07cbd0b71853.png">

With postal code as one of the top attributes, we’re convinced that location will affect the dollar sign of a restaurant, even though there is no direct relationship between price of housing and restaurant dollar signs.

## Limitation

### Issue I. Imbalance Data

<img width="785" alt="Screen Shot 2021-08-28 at 16 14 35" src="https://user-images.githubusercontent.com/73683982/131233236-83fccf2b-bdab-41f5-b377-9dc2ff4a68f5.png">

We have an imbalance dataset. Data is heavily distributed on class 1 and 2 but a lot less on class 3 and 4. This imbalance issue might impact the prediction accuracy in our model since we have a very small amount of samples for class 3 and 4. We tried to solve this problem by oversampling the minority using SMOTE, but it worse off the accuracy. If we take a look at the precision for both Naïve Bayes and Random Forest, the precisions are lower for both class 3 and 4. We believe this happens due to the imbalance data.

<img width="406" alt="Screen Shot 2021-08-28 at 16 16 35" src="https://user-images.githubusercontent.com/73683982/131233272-1babca02-2813-4efc-961d-71525f94eb84.png">

### Issue II. Data doesn’t represent the whole United States

<img width="889" alt="Screen Shot 2021-08-28 at 16 18 23" src="https://user-images.githubusercontent.com/73683982/131233293-d78c7ae4-6a1d-42ec-9383-4df47e6cdd25.png">

Our data only represents several states and zip codes in the United States. This raises a red flag for our model because zip code/location of the restaurant is one of the important attributes on prediction. While our goal is to make the prediction for the entire United States, we realized that we need a better dataset that represent more zip codes.

The complete analysis can be found on: 
https://github.com/hehuiyin/Yelp-Prediction/blob/main/Yelp%20Prediction%20Project.ipynb
