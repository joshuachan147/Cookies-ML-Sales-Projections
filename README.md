# Cookies-ML-Sales-Projections
Abstract:
Cookies is an up-and-coming Cannabis startup centered in the California area. With 3 locations, hundreds of  brands, and a multitude of products, Cookies has been rapidly growing and “employed” us to aid their growing data needs. Cookies provided us with brand level data, including metrics such as total sales and products offered by each brand Cookies distributes for. Our team decided to take this brand level data and build out an optimized predictive regression model aiming to predict total sales. The goal was for Cookies to be able to use this model to predict the total sales for different brands in the future. To achieve this goal, my team first decided to subset the data we were given on 25 brands. We then merged the datasets together, keeping relevant features from each dataset such as the type of products offered by each brand, total sales, and average retail price of each product. The next step was augmenting some time series features relating to total sales, and then running our merged dataset through an imputation strategy and scaling our numerical data. Aftering running some basic statistical measurements like correlation plots, we then performed principal component analysis to simplify the number of features and find the best predictors for total sales. We then tested the data by running it through multiple models, including linear regression, knn, random forest, and others. After optimizing hyperparameters and splitting data using cross validation, we found the best performing model was linear regression with an average error rate of 14% - meaning the data is linearly separable and fairly consistent across time. Given this model, we hope Cookies can utilize our code to accurately predict sales for future months and different brands.

Background/Introduction:
With the dual barriers of legalization as well as public perception, cannabis historically has been an extremely volatile industry. In recent times, both barriers have been relaxed bringing new product potential and a much wider customer base. Worldwide sales have been projected to increase from 30 billion to 60 billion by 2026. Since the US is home to the largest cannabis market in the world (driven in large part by the legalization of marijuana by states like Oregon), Cookies focuses primarily on inter-country cannabis distribution but also is starting to expand to countries like Canada and Portugal. Particularly within California, Gavin Newsom deemed the cannabis industry essential in 2020 and local dispensaries took up that challenge with online ordering services and in-person display stores. Cookies has been working to improve their market share within the industry by learning more about other brand’s sales and methods of production. 

Methodology:
When we merged the original datasets, we decided to limit the number of features we kept from brand details, mostly involving product categoricals of each brand. After merging the initial datasets, our first step was to augment the Total Sales column to create additional time series features. Since our goal was to predict total sales, augmenting the Total Sales column would give our model more relevant information to use and hopefully improve performance. The augmented features we added were Previous Month, which keeps track of the previous month’s sales, and Rolling Average, which calculates the average sales from the previous three months. We also added 5 binary features: Inhalables, Concentrates, Vape, Flavored, and Edibles, which indicate whether or not a brand offers these types of products. Since our project goal involves time series data, the month and year for each data point was also an important part of our model. We dealt with date values by converting the month column from a string to a datetime object, then separating month and year into two different columns. Finally, we ran all of our data through a pipeline in order to standardize numerical features and encode categorical features. We used StandardScaler to transform all numerical features to have a mean of 0 and standard deviation of 1. This ensures that all features are on the same scale, and no one feature will dominate our predictive models. We used OrdinalEncoder to encode the year and month columns, as year and month can be considered categorical features with an inherent order. After running our data through this pipeline, we converted the outputted numpy array back into a pandas dataframe so that we could better interpret the data going forward. The last step in preparing the data was to encode the 25 brands. We accomplished this by using the pandas get_dummies function, which applies one-hot encoding and keeps the brands as column names. Once our data was fully prepared, we split it into training and testing data and experimented with multiple different machine learning models. The models that we tried were linear regression, lasso regression, ADA boosting, random forest, KNN, and SVR, and cross-validation showed that the best performing models were linear regression and KNN. Both had an error rate of approximately 14%. 


Statistics Results:
LR
Basic Linear Regression got an error rate of around 15%. We actually used lasso regularization because we dummy encoded brands and some of those brand columns wouldn't be used in random iterations of train/test data, therefore their coefficients would be random numbers. To avoid this problem, we used lasso regularization to drive those coefficients to 0. 

Ensemble Method
We employed two ensemble methods, random forest and ADA boost. Random forest was our best performing model with an error rate of 11%, but we found evidence it was overfitting on our data. ADA boost produced an error of 16%. 

GridSearch Optimization/Custom Model
Gridsearch was used in order to tune our hyperparameters of each model. An example of how we used gridsearch is attached below. 


Conclusion:
Essentially each of the 5 models that we tested had one primary goal: predicting the total sales for each brand as accurately as possible. Each model has a different way of achieving this prediction with varying results as can be seen. A 15% error rate means the model accurately predicted the total sales 85% of the time. That means our best performing models, knn and linear regression, can accurately predict total sales about 86% of the time. Cookies could leverage our model and results to predict total sales. Since Cookies is taking in new data monthly, they would only have to segment a new dataset for the month and brands they want to predict, then run the data with new brands through our model to predict new total sales for any given month. This type of machine learning and analytic work could be very valuable for the company to estimate their sales and please shareholders. With the growing cannabis industry in recent times, this project was aimed at helping Cookies expand into a greater piece of the cannabis market share. Through a detailed data science process involving cleaning data, merging/subsetting data, augmenting features, and building machine learning models, we have provided Cookies with the framework to predict their total sales as well as their competitors’ within the cannabis industry.
