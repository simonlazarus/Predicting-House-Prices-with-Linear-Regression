# Introduction

In 2021, the total value of US real estate grew by nearly 19% [to a value of $43.4 trillion](https://www.zillow.com/research/us-housing-market-total-value-2021-30615/).  Furthermore, a [plurality of US citizens](https://www.cnbc.com/2022/12/15/americans-say-real-estate-is-best-way-to-build-wealth.html) believe that investment in real estate is the best way to build personal wealth.  When considering investments in real estate, though, it is important to be able to predict the value of a property based on its characteristics.

In this project, we will build models to predict the sale prices of homes in Ames, Iowa using data on many features of those homes.  We will employ linear regressions to make good predictions while maintaining interpretability of our models.  Finally, we will employ regularized regressions to make even better predictions, but at the cost of interpretability.

Our data is taken from the Ames Housing Dataset, described [here](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt).  [Our training sample of this data](./datasets/train.csv) contains over 75 different variables recorded from each of over 2,000 homes sold between 2006 and 2010, including these homes' sale prices.  We also have a [test data set](./datasets/test.csv) containing the same data from 878 additional homes, but with sale prices excluded.  This test data set will only be used in the [Kaggle competition](https://www.kaggle.com/competitions/dsir-1128-project-2-regression-challenge/overview) associated with this project; during our modeling process we will reserve 15% of our "training" dataset as a way to validate our best models' performance on entirely new data.

The problem of predicting the prices of homes sold in Ames, Iowa between 2006 and 2010 is certainly less difficult than the problem of predicting the prices of homes sold across many locations and many points in time.  However, this former problem allows us to employ relatively simple techniques to great effect.


# Data Science Problem

A group of real estate investors and potential homeowners wants us to predict the prices of homes in Ames, Iowa based on measurable characteristics of those homes.  They care primarily about the accuracy of our predictions, but they would also like to be able to understand which features of homes contribute to higher sale price predictions, and by how much.

To answer this question, we will develop linear regression and regularized linear regression models that predict homes' sale prices based on a variety of features.  We will evaluate the success of our models using their $R^2$ (equivalently, mean squared error) and mean absolute error scores on the reserved test data; higher $R^2$ and lower MAE will be better.  We will also evaluate models based on their interpretability.


# Tehcniques Employed

In our regressions, we need a way to encode categorical features as numeric values.  When using regularized regression models (LASSO, Ridge and ElasticNet) in the [last notebook](./code/5_advanced_modeling.ipynb), we encode these features using one-hot encoding: each value of each categorical variable receives its own dummy variable.  However, when we are not employing regularization to fight overfitting, we must avoid including too many dummy variables in our models.  Therefore, we develop a method of encoding categorical variables as the values 1 ("above average"), 0 ("approximately average"), and -1 ("below average") that we call `above_below_mid` encoding.  See the [4th notebook](./code/4_modeling.ipynb) for details.

# Results

Our regularized regressions perform slightly better (in terms of $R^2$ and MAE on the reserved test data) than our non-regularized regressions.  However, our best non-regularized regression still performs quite well by these metrics, and it is quite plausibly interpretable: one can use the coefficients to read out the percentage changes in predicted home values associated with various features increasing or decreasing.  For this reason, we choose this well-performing non-regularized linear regression model as our production model.