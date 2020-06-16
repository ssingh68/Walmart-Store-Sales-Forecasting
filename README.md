# Walmart-Store-Sales-Forecasting

Walmart provided historic data from February 2010 to October 2012 with a task to predict the department wide weekly store sales.
Given the competition took place 5years ago; we wanted to rank amongst the top 100 on the leader board and if possible, outperform the winner. Certainly, there are some changes/improvements in the data science field over the last five years in term of the
tools and modelling techniques.

Overall approach stems from EDA to find patterns (correlation, outliers, trends, seasonality etc) in the provided datasets followed by data pre-processing before applying appropriate modelling techniques, which we then validate through submission to Kaggle.
Given the additional variables captured in the ‘features.csv’ dataset, I felt compelled to try out some machine learning models to see how well they can fit the test data and validate their performance on Kaggle instead of just applying time-series forecasting
models. I captured below the models adopted to forecast the weekly sales:

#### First Models
ML Models - Linear Regressor, Elastic Net Regressor, Neural Network (MLP), KNN, Gradient Boosting, Random Forest, Extra Tree Classifier

#### Final Models
Forecasting Models - SVD (ETS/STLF), SVD (ARIMA/STLF), SVD (Seasonal ARIMA), STLF ARIMA, Standard Scaling (ETS+STLF), Non Seasonal ARIMA, Average Simple Models (Regression, Seasonal, Naive)

#### Best Model
I tried ensembling with different models, resulting in the below model.

1. SVD + STLF/ETS: SVD was applied on the training data as a pre-processing step
followed by forecasting each series with STLF using using an exponential smoothing
model (ets) for the non-seasonal forecast.

2. SVD + STLF/ARIMA: Same as the above model but instead of ETS, ARIMA was used to
capture non seasonal forecast.

3. Standard Scaling+ STLF/ETS + averaging: Just like model 1, instead of SVD pre-
processing Standard scaling was used and a correlation matrix was computed. Then
forecasts were made and several of the closely correlated series were averaged
together, before restoring the original scale

4. SVD + seasonal ARIMA: We know that ARIMA doesn’t perform well on seasonal data,
so we used seasonal ARIMA along with SVD to capture Seasonal information,
“auto.arima()” from forecast package was used.

5. non-seasonal ARIMA with Fourier series terms as regressors: Here we used non
seasonal ARIMA to capture more detailed non seasonal information and regressors
were used to capture the seasonal information as well.

6. Averaging simple models
• A linear regression model with seasonal(weekly) dummy variables,
• A seasonal naive model,
• A product model, which predicts a weekly average time a store average

### My final model i.e Averaging across all the model predictions, outperformed the existing best solution, scoring us highest on the leader board.
