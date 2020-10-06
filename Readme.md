------------------------------------
Project 4 - Major Leagues
------------------------------------

In this project, we are predicting the final score of a soccer team based on the team's and its opponent's characteristics.

---------------------
Data Exploration:
---------------------

I have performed some data exploration on both the SPI Global Rankings dataset and the SPI Matches datasets. The SPI Global Rankings dataset showed clear positive correlation between off and spi. And, we could find a clear negative correlation between def and spi. Offensive, defensive and SPI ratings are skewed to the left. This means that most of the teams have below average ratings. So, we can say that the dataset contains a higher number of teams with low ratings. At the same time, there are very few teams with very high ratings.

From the SPI Matches dataset, after exploring the probtie column with respect to a newly created column, we could see that the probtie was somewhat related to the difference between the team spi values. However, the probtie didn't show a correlation with the actual instance of tie. Therefore, the probtie didn't seem to be a true indicator of an actual tie.

---------------------
Feature Engineering:
---------------------

1. Scaled the features between 0 and 1 for convenient computation
2. Label encoded teams since those are categorical features
3. Since, I used the importance columns for the regression, I needed to impute the missing values for the importance features. I have used the mean of the respective columns for the imputation
4. As part of data cleaning, I have identified the outliers to be the ones having score1>5 or score2>5 since, 5 was greater than or equal to 3*standard deviations for the respective target variables. Then, I have removed the outliers.
5. I have created two relative spi feature for a team with respect to the opponent team. The rationale was to create a comparative index with respect to only the opponent. Then, I factored in the probability of winning and the probability of not having a tie.
6. Using the newly created relative features and some other numerical features, I have created a polynomial feature generator using the sklearn package. As a result, I could create numerous other features that could potentially have multicolinearity. So, I have used PCA to eliminate correlation within features by keeping the first few columns displaying the higher variance. Then, I have scaled the newly created polynomial features between 0 and 1.

-------------
Regression
-------------

I have used the XGBRegressor, Multioutput Ridge Regressor, and Neural Network MLPRegressor for predicting scores.

----------
Analysis
----------

The r2_score for the all of the models was close to 0 but positive. Getting positive r2_scores is promising in the direction of the objective. However, the better scores would be close to 1. Therefore, the models were not giving good performance.

The feature space doesn't seem to have much correlation with the output. Additional feature engineering can improve the situation.

Although I have tried various other feature transformations with inter-feature interactions, the performance didn't seem to improve at all. I had also tried the Polynomial Feature generator from sklearn. Then, I used PCA to reduce features so that we didn't have curse of dimensionality. But, even with these additional features, performance didn't seem to improve. I believe, the key to eliciting a good linear correlation between the feature space and the target variable could be through using a linear combination of features.