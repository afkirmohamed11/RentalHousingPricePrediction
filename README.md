# Project Presentation 
## Project Overview
Project focuses on predicting rental prices for Moroccan properties using advanced ML techniques, addressing a classic regression problem. Additionally, aims to uncover key factors influencing rental prices across select Moroccan cities.



![image](https://github.com/afkir00/RentalHousingPricePrediction/assets/143105211/d9dacd8b-9404-40a0-a4d2-91724429a7c9)


## Data Collection
Our data:
 - was collected from the Moroccan website “Mubawab” on 
 - November 21 and 22, 2023.
 - Has in total 10,549 records. 
 - Concerns ten Moroccan cities: Agadir, Bouskoura, Casablanca, Dar-Bouazza, Kénitra, Marrakech, Mohammedia, Rabat, Salé, and Tangier.
 - Initially has 30 features, including Price, City, Type of Property, Area, Number of Rooms, Presence of a Garden, a TV, etc.


## Methodology
### Data Pre-processing, Transformation & Feature Engineering

#### Missing Values
- Features with more than 35% of null values:
"Floor type" and "orientation" were removed due to their minimal impact on pricing.
- A linear regression imputation strategy was used for the ‘’Floor” attribute.
- ‘Age of Rental’ was removed due to its highly negative correlation with ‘Rental Status’ feature.

#### Feature Transformation
- ’City ’’ attribute was one-hot encoded.

- EUR entries were converted to DH.

- Properties were categorized: apartments as '1', houses as ‘0’.

- Binary features were represented by ‘1’ if present and ‘0’ otherwise.

- ‘’Rental status‘’ was mapped: '2' for new properties, '1' for well-maintained ones.

- Duplicated entries were removed.

- Null values were dropped.

  #### Dataset before
![image](https://github.com/afkir00/RentalHousingPricePrediction/assets/143105211/bda2dbb0-62a8-4cb5-8b78-e519551831fb)

 #### Dataset after
![image](https://github.com/afkir00/RentalHousingPricePrediction/assets/143105211/855273a3-1c92-42b3-bc2b-0e60d49d1b20)

#### Outliers handling
We did not observe any influential outliers in the dataset, except in the “Price” and “Area” variables. By using the IQR method, we drop them with the exception of those that seem to be real.

##### Interquartile Range (IQR) Method :

x is an outlier if:

x < Q1 - 1.5  * IQR    OR    x >  Q3 + 1.5  * IQR       Where:
Q1   = 25th percentiles,  Q3   = 75th percentiles,      IQR = Q3   -  Q1

#### Rooms attribute Outliers
![image](https://github.com/afkir00/RentalHousingPricePrediction/assets/143105211/2fd0d466-0afa-426c-b779-37a26f3437aa)


#### Price & Area Outliers
![image](https://github.com/afkir00/RentalHousingPricePrediction/assets/143105211/b5f6a203-6aab-44d0-8d15-dc4b12d9392f)


#### Dataset With Outliers
![image](https://github.com/afkir00/RentalHousingPricePrediction/assets/143105211/7e377b28-aa68-4836-82fe-6d93e087f2df)

#### Dataset Without Outliers
![image](https://github.com/afkir00/RentalHousingPricePrediction/assets/143105211/ba4666a2-076d-408c-9fb1-dba680ae32b8)

#### Feature Selection by PCA Technique:
We applied the PCA technique for data reduction and experimented with different numbers of components. However, the explained variance ratio was insufficient, suggesting that PCA might not be suitable for our case. Therefore, we decided to retain all the features.

## Data Analysis

We started the Data Analsis stage by examing the correlation between the differennt variables.
- Correlation Between Numerical Features
![image](https://github.com/afkir00/RentalHousingPricePrediction/assets/143105211/e2697575-9250-4841-9dd4-0cf22febe1f5)

 We notice a considerable correlation between ‘’Price’’ and room attributes

- Correlation Between Binary Features
![image](https://github.com/afkir00/RentalHousingPricePrediction/assets/143105211/40744c47-c322-42d0-8f17-83b0f3d6fab3)

We identified strong correlations among 'TV’ , ’Refrigerator, ’ Oven'  and ‘Furnished' attributes.

### General Analysis of Single Factors
Regression models were used to analyze 'room attributes’, Floor', and Area' impact on rent. The 'room attributes' are a sum of Number of Rooms', ‘Number of Bedromms', and ‘Number of Bathrooms'. R² values for each regression are compared in the figure.

![image](https://github.com/afkir00/RentalHousingPricePrediction/assets/143105211/a8e629d2-75f3-4362-adfa-2cf7f5fad170)

### Effects of Different Cities
Regression models were used to analyze 'room attributes', 'Etage', and 'Surface' impact on rent. The 'room attributes' are a sum of 'Nombre de chambres', 'Nombres de pièces', and 'Nombre de Salles De Bains'. R² values for each regression are compared in the figure.

![image](https://github.com/afkir00/RentalHousingPricePrediction/assets/143105211/9f3a1e51-32f4-4387-a6d2-050aa0132bed)


## Model Selection

### Linear Regression
As a baseline measure, we performed a standard linear regression model with an Elastic Net loss function, after  the normalization pre-processing step.

### Decision Tree Regression
Decision Tree Regression (DTR) is a powerful supervised learning algorithm predominantly used for solving regression problems. It operates by partitioning the input space into regions, and then fitting a simple model (like a constant) in each one. Key parameters such as max_depth, min_samples_leaf and min_samples_split control the complexity and size of the tree, 

### Random Forest Regression
Random Forest Regression is a meta-estimator that fits a number of decision trees on various sub-samples of the dataset and uses averaging to improve the predictive accuracy and control overfitting.The key parameters of a Random Forest include n_estimators, criterion, max_depth, min_samples_split, and min_samples_leaf.

### Gradient Boosting Regression
Gradient Boosting is a technique that progressively builds a sophisticated regression model, referred to as H, by incorporating simple models in an iterative manner. Every additional simple model in the ensemble is designed to rectify the shortcomings of the existing ensemble.


## Results & Discussion

#### Hyperparameters tuning
For each of these models, we employ GridSearchCV from Scikit-Learn. This method allows us to systematically explore multiple combinations of parameters, cross-validate each one, and determine which configuration yields the best performance.

#### Evaluation Metrics
The evaluation metrics used in this study are the Root Mean Squared Error (RMSE) and the Coefficient of Determination, denoted as R². 

#### Model Comparison
##### R²
![image](https://github.com/afkir00/RentalHousingPricePrediction/assets/143105211/4ad6f998-b8b6-45c2-a9e6-bd9aa6ef03b6)

##### RMSE 
![image](https://github.com/afkir00/RentalHousingPricePrediction/assets/143105211/ccc9958e-5a31-4803-b398-b8bc53057f19)

#### Model Selection
![image](https://github.com/afkir00/RentalHousingPricePrediction/assets/143105211/774f18af-6edc-4e70-a6b1-0a9638577b75)
Comparison of Random Forest Regression’s predicted results and original test set

### Thanks for Your Attention

### project report on ResearchGate: https://shorturl.at/hBGOU
