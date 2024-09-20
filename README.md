# Bayesian_House-Pricing-Prediction
Paris House Pricing Prediction Model Using Bayesian Method

1. INTRODUCTION
The prices of houses in Paris, along with relevant information for each, are available in the dataset from https://www.kaggle.com/datasets/mssmartypants/paris-housing-price-prediction. The objective of this project is to create a prediction model for house prices in Paris using Bayesian methods. The dataset has 17 columns, and all attributes are numeric variables. The target variable here is price. The data contains the information’s of size of a house in square meters, number of rooms in the house, does the house has a yard, does the house include a pool, how many floors that the house have, number of zip code, city’s part range (the higher the value, the more exclusive the neighbourhood is), numbers of previous owners, the year that the house was made, is the house new or renovated, does the house have a storm protector, the house’s basement size in meter, the house’s attic size in meter, the house’s garage size in meter, does the house have a storage room, does the house have a guest room, and the target variable, which is the house’s price. The prediction will be done with the information that the dataset provided.

2. MODELS
To find the best model, we will standardise the features and use Gaussian Multiple Linear Regression as stated with the assumption of normality of the data. The alpha is the intercept when there isn’t any features data. Beta is the slope of each feature which is then added all together.

![Gaussian Multiple Linear Regression Formula]<img width="153" alt="image" src="https://github.com/user-attachments/assets/cd61a7cd-ef19-46de-b3de-98ddd89dc619">

With Likelihood of <img width="313" alt="image" src="https://github.com/user-attachments/assets/b246a07f-2853-48b0-8f5e-08f0727afb41">, where X<sub>ij</sub> being the value of each feature for 𝑗=1 each iteration of 𝑖 with Priors α ~ 𝑁𝑜𝑟𝑚𝑎𝑙(0, 1000), β<sub>j</sub> ~ 𝑁𝑜𝑟𝑚𝑎𝑙(0, 1000), and 




