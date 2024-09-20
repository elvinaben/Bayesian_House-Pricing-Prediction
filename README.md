# Bayesian_House-Pricing-Prediction
Paris House Pricing Prediction Model Using Bayesian Method

**1. INTRODUCTION**
The prices of houses in Paris, along with relevant information for each, are available in the dataset from https://www.kaggle.com/datasets/mssmartypants/paris-housing-price-prediction. The objective of this project is to create a prediction model for house prices in Paris using Bayesian methods. The dataset has 17 columns, and all attributes are numeric variables. The target variable here is price. The data contains the information’s of size of a house in square meters, number of rooms in the house, does the house has a yard, does the house include a pool, how many floors that the house have, number of zip code, city’s part range (the higher the value, the more exclusive the neighbourhood is), numbers of previous owners, the year that the house was made, is the house new or renovated, does the house have a storm protector, the house’s basement size in meter, the house’s attic size in meter, the house’s garage size in meter, does the house have a storage room, does the house have a guest room, and the target variable, which is the house’s price. The prediction will be done with the information that the dataset provided.


**2. MODELS**
To find the best model, we will standardise the features and use Gaussian Multiple Linear Regression as stated with the assumption of normality of the data. The alpha is the intercept when there isn’t any features data. Beta is the slope of each feature which is then added all together.

<img width="153" alt="image" src="https://github.com/user-attachments/assets/cd61a7cd-ef19-46de-b3de-98ddd89dc619">

With Likelihood of Y<sub>i</sub> ~ 𝑁𝑜𝑟𝑚𝑎𝑙(α + &#8721;<sub>j=1</sub><sup>n</sup> 𝑋<sub>ij</sub>β<sub>j</sub>, σ<sup>2</sup>), where 𝑋<sub>ij</sub> being the value of each feature for 𝑗=1 each iteration of 𝑖 with Priors α ~ 𝑁𝑜𝑟𝑚𝑎𝑙(0, 1000), β<sub>j</sub> ~ 𝑁𝑜𝑟𝑚𝑎𝑙(0, 1000), and σ<sup>2</sup> ~ 𝐼𝑛𝑣𝐺𝑎𝑚𝑚𝑎(0. 1, 0. 1) and 𝑛 being the number of features.

Model 1 : In the 1st model, we will use Gaussian Multiple Linear Regression as stated with all of the features of the dataset.
Model 2 : In the 2nd model, we will use Gaussian Multiple Linear Regression as stated, but only using the features with strong correlations with the target feature based on the frequentist linear regression model found in Table 1.1 The indication of strong correlation here is taken from features with 3 significance stars.
Model 3 : In the 3rd model, we will utilize the features used in the 2nd model. However, the initial values for alpha and beta coefficients will be taken from the estimates of the frequentist linear model found in Table 2.
Model 4 : In the 4th model, the slope is still a fixed effect but the intercept will be treated as a mixed effect with random effect for the price. The Gaussian Linear Regression Model is :

<img width="239" alt="image" src="https://github.com/user-attachments/assets/5b24b546-8b92-42b0-a447-a0a4898886e8">

With Likelihood of Y<sub>i</sub> ~ 𝑁𝑜𝑟𝑚𝑎𝑙(α + 𝜃<sub>ei</sub> + &#8721;<sub>j=1</sub><sup>n</sup> 𝑋<sub>ij</sub>β<sub>j</sub>, σ<sup>2</sup>), where 𝑋<sub>ij</sub> being the value of each feature for each iteration of 𝑖 with Priors α ~ 𝑁𝑜𝑟𝑚𝑎𝑙(0, 1000), and σ<sup>2</sup> ~ 𝐼𝑛𝑣𝐺𝑎𝑚𝑚𝑎(0.1, 0.1) and double-exponential random effect 𝜃<sub>ei</sub> ~ 𝐷𝐸(0, σ<sup>2</sup>) and 𝑛 being the number of features.

**Table 1 - Frequentist Linear Regression Model (with all features)**
<img width="588" alt="image" src="https://github.com/user-attachments/assets/6e8c765b-3a59-41f5-82f1-df76a4d0fcbe">

**Table 2 - Frequentist Linear Regression Model (with strong correlation features)**
<img width="963" alt="image" src="https://github.com/user-attachments/assets/6e27eeed-c47d-41c9-a394-507ccc7d4cd2">


**3. COMPUTATION**
All models will be fitted using the JAGS package in R. For building all of the models the first 500 samples were discarded as burn in, and then for 1st, 2nd, 3rd model 2000 samples were drawn from each of the 3 chains with a thinning factor of 5 and for the 4th model 5000 samples were drawn with the same thinning factor and chain as the 1st model. On the 1st and 4th Model we are using all the independent features of the data. On the 2nd and 3rd Model we will only use seven selected features based on the frequentist linear regression model as shown on Table 2 and changing the initial values for the 3rd model with the result of the frequentist linear regression model on Table 2. The model convergence is assessed by examining the trace plot, the Gelman-Rubin statistic (where a value < 1.1 indicates convergence), and the effective sample size (where a value > 1000 indicates convergence). The trace plots illustrate that all parameters in all models have achieved convergence. Gelman-Rubin statistics are computed for each parameter in every model, yielding multivariate potential scale reduction factors (PSRF) of 1.02 for the 1st Model, 1.01 for 2nd, 3rd, and 4th Model. Additionally, the effective sample size (ESS) for all parameters in all models is calculated, and in every model, ESS exceeds 1000. Therefore, we can conclude that all models have achieved convergence.


**4. MODEL COMPARISON**
The model performances are compared using the Deviance Information Criterion (DIC) and the Watanabe-Akaike Information Criterion (WAIC). The comparisons of the four models based on these criteria are summarized in Table 3. Among the four models, the one with the lowest DIC and WAIC is Model 4. Therefore, we will use Model 4 to predict house prices in this project.

**Table 3 - Model comparisons**
<img width="509" alt="image" src="https://github.com/user-attachments/assets/65296983-4f81-46c7-8033-63ebd4222cef">


**5. RESULT**
Applying Model 4, the posteriors of the parameters are summarized in Table 4. All parameters are significant, so we can conclude that in the real estate market of Paris, France :
● An increase in the land size (squareMeter) of the house by 1 unit decreases its price by 0.081.
● Increasing the number of rooms in the house by 1 unit decreases its price by 0.296.
● Having a yard in the house increases its price by 0.1.
● Having a pool in the house decreases its price by 0.443.
● Increasing the number of floors in the house by 1 unit increases its price by 0.081.
● Increasing the city code (CityCode), which might relate to the location of the house, increases its price by 0.294.
● Increasing the number of previous owners (prevOwners) by 1 unit decreases its price by 0.153.
● Increasing the year the house was made (YearMade) by 1 unit increases its price by 0.473.
● If the house is newly built (isNewBuilt), it increases its price by 1.001.
● Having a storm protector in the house decreases its price by 0.711.
● Increasing the basement area (Basement) by 1 unit increases its price by 0.610.
● Increasing the attic area (Attic) by 1 unit increases its price by 0.095.
● Increasing the garage area (Garage) by 1 unit increases its price by 0.382.
● Having a storage room (Storage) decreases its price by 1.187.
● Having a guest room (Guest) decreases its price by 0.634.
● Increasing the city part range (CityPartRange) by 1 unit decreases its price by 0.432.

Thus, we can conclude that the price of a house mainly increased based on several key factors, including the presence of a yard, the number of floors, the city code indicating location, the year the house was made, the house being newly built, the spaciousness of the basement, the size of the attic area, and the size of the garage.

**Table 4 - Summary of the posteriors**
<img width="387" alt="image" src="https://github.com/user-attachments/assets/367d886e-e985-432f-9faa-db3b7a817c72">
