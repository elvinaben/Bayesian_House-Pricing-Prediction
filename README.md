# Bayesian_House-Pricing-Prediction
Paris House Pricing Prediction Model Using Bayesian Method

1. INTRODUCTION
The prices of houses in Paris, along with relevant information for each, are available in the dataset from https://www.kaggle.com/datasets/mssmartypants/paris-housing-price-prediction. The objective of this project is to create a prediction model for house prices in Paris using Bayesian methods. The dataset has 17 columns, and all attributes are numeric variables. The target variable here is price. The data contains the information’s of size of a house in square meters, number of rooms in the house, does the house has a yard, does the house include a pool, how many floors that the house have, number of zip code, city’s part range (the higher the value, the more exclusive the neighbourhood is), numbers of previous owners, the year that the house was made, is the house new or renovated, does the house have a storm protector, the house’s basement size in meter, the house’s attic size in meter, the house’s garage size in meter, does the house have a storage room, does the house have a guest room, and the target variable, which is the house’s price. The prediction will be done with the information that the dataset provided.

2. MODELS
To find the best model, we will standardise the features and use Gaussian Multiple Linear Regression as stated with the assumption of normality of the data. The alpha is the intercept when there isn’t any features data. Beta is the slope of each feature which is then added all together.

<img width="153" alt="image" src="https://github.com/user-attachments/assets/cd61a7cd-ef19-46de-b3de-98ddd89dc619">

With Likelihood of Y<sub>i</sub> ~ 𝑁𝑜𝑟𝑚𝑎𝑙(α + &#8721;<sub>j=1</sub><sup>n</sup> 𝑋<sub>ij</sub>β<sub>j</sub>, σ<sup>2</sup>), where 𝑋<sub>ij</sub> being the value of each feature for 𝑗=1 each iteration of 𝑖 with Priors α ~ 𝑁𝑜𝑟𝑚𝑎𝑙(0, 1000), β<sub>j</sub> ~ 𝑁𝑜𝑟𝑚𝑎𝑙(0, 1000), and σ<sup>2</sup> ~ 𝐼𝑛𝑣𝐺𝑎𝑚𝑚𝑎(0. 1, 0. 1) and 𝑛 being the number of features.

Model 1 : In the 1st model, we will use Gaussian Multiple Linear Regression as stated with all of the features of the dataset.
Model 2 : In the 2nd model, we will use Gaussian Multiple Linear Regression as stated, but only using the features with strong correlations with the target feature based on the frequentist linear regression model found in Table 1.1 The indication of strong correlation here is taken from features with 3 significance stars.
Model 3 : In the 3rd model, we will utilize the features used in the 2nd model. However, the initial values for alpha and beta coefficients will be taken from the estimates of the frequentist linear model found in Table 2.
Model 4 : In the 4th model, the slope is still a fixed effect but the intercept will be treated as a mixed effect with random effect for the price. The Gaussian Linear Regression Model is :

<img width="239" alt="image" src="https://github.com/user-attachments/assets/5b24b546-8b92-42b0-a447-a0a4898886e8">

With Likelihood of Y<sub>i</sub> ~ 𝑁𝑜𝑟𝑚𝑎𝑙(α + 𝜃<sub>ei</sub> + &#8721;<sub>j=1</sub><sup>n</sup> 𝑋<sub>ij</sub>β<sub>j</sub>, σ<sup>2</sup>), where 𝑋<sub>ij</sub> being the value of each feature for each iteration of 𝑖 with Priors α ~ 𝑁𝑜𝑟𝑚𝑎𝑙(0, 1000), and σ<sup>2</sup> ~ 𝐼𝑛𝑣𝐺𝑎𝑚𝑚𝑎(0.1, 0.1) and double-exponential random effect 𝜃<sub>ei</sub> ~ 𝐷𝐸(0, σ<sup>2</sup>) and 𝑛 being the number of features.



