A time series is a collection of continuous data points recorded over time. A time series is recorded in intervals such as hourly, daily, weekly, minutes, monthly, and yearly.

Examples of time series are the annual budgets, company sales, weather records, air traffic, covid-19 caseloads, forex exchange rates, and stock prices. The time-series data are recorded in minutes, hours, days, weeks, or years.

For example in stock prices, we can observe the daily closing stock prices of a company for a week. A time series model can then analyze these closing stock prices to identify hidden patterns. Eventually, the model predicts future stock prices based on previously observed closing prices.

In this tutorial, we will build on a multivariate time series model that uses multiples variables in training. We create the model using [Auto ARIMA](https://alkaline-ml.com/pmdarima/modules/generated/pmdarima.arima.auto_arima.html). 

### Table of contents
- [Prerequisites](#prerequisites)
- [Getting started with Auto ARIMA](#getting-started-with-auto-arima)
- [Understanding the ARIMA model](#understanding-the-arima-model)
- [How to remove non-stationarity components in a time series](#how-to-remove-non-stationarity-components-in-a-time-series)
- [Explaining ARIMA initials](#explaining-arima-initials)
- [Why do we use Auto ARIMA?](#why-do-we-use-auto-arima)
- [Energy consumption dataset](#energy-consumption-dataset)
- [Plotting the 'demand' column](#plotting-the-demand-column)
- [Plotting subplots](#plotting-subplots)
- [Checking for missing or null values](#checking-for-missing-or-null-values)
- [Imputing missing values](#imputing-missing-values)
- [Dataset resampling](#dataset-resampling)
- [Implementing the Auto ARIMA model](#implementing-the-auto-arima-model)
- [Initialize 'auto_arima()' function](#initialize-autoarima-function)
- [Splitting the time series dataset](#splitting-the-time-series-dataset)
- [Fitting the Auto ARIMA model](#fitting-the-auto-arima-model)
- [Using the Auto ARIMa model to make predictions](#using-the-auto-arima-model-to-make-predictions)
- [Making prediction on the test data frame](#making-prediction-on-the-test-data-frame)
- [Making prediction on the unseen future values](#making-prediction-on-the-unseen-future-values)
- [Plotting the future predicted values](#plotting-the-future-predicted-values)
- [Conclusion](#conclusion)
- [References](#references)

### Prerequisites
For a reader to understand the time series concepts explained in this tutorial, they should understand the following concepts:

- [Introduction to time series](/engineering-education/introduction-to-time-series/)
- [Time Series Decomposition](/engineering-education/time-series-decomposition-in-python/)
- [Building a simple time series application](/engineering-education/building-a-time-series-weather-forecasting-application-in-python/)
- Know how to run the Python code in [Google Colab](https://research.google.com/colaboratory/)

### Getting started with Auto ARIMA
[Auto ARIMA](https://alkaline-ml.com/pmdarima/modules/generated/pmdarima.arima.auto_arima.html) is a time series library that automates the process of building a model using ARIMA. Auto ARIMA applies the concepts of [ARIMA](https://otexts.com/fpp2/arima.html) in modeling and forecasting.

Auto ARIMA automatically finds the best parameters of an ARIMA model. To easily understand this tutorial you have to understand the concepts of the ARIMA model. But Let's discuss the ARIMA model briefly so that a beginner can also easily follow and understand this tutorial.

### Understanding the ARIMA model
Auto-Regressive Integrated Moving Average(ARIMA) is a time series model that identifies hidden patterns in time series values and makes predictions.

For example, an ARIMA model can predict future stock prices based on analyzing previous stock prices. Also, an ARIMA model assumes that the time series data is stationary. For an ARIMA model to work we always have to remove the non-stationarity components in the time series.

### How to remove non-stationarity components in a time series
Removing non-stationarity in a time series will make it stationary and therefore apply the ARIMA model. A non-stationary time series is a series whose properties changes change over time. A non-stationary time series has trends and seasonality components.

The properties of time series that should remain constant are variance and mean. Making these properties constant will remove the trend and seasonal components. We remove non-stationarity in a time series through differencing.

Differencing technique subtracts the present time series values from the past time series values. We may have to repeat the process of differencing multiple times until we output a stationary time series.

An ARIMA model is made up of three initials: AR, I, and MA. These initials represent the three sub-models that are combined to form a single uniform model.

Let's explain these initials.

### Explaining ARIMA initials
AR stands for Auto Regression. I stand for Integrated. MA stands for Moving average. 

They have the following functionalities.

- Auto Regression sub-model
This sub-model uses the past values to make future predictions.

- Integrated sub-model
This submodel performs differencing to remove any non-stationarity in the time series.

- Moving Average sub-model
It uses past errors to make a prediction.

These sub-models are then added to the overall ARIMA model as parameters. The parameters have unique notations as follows:

- p: It is the order of the Auto Regression (AR) sub-model. It refers to the number of past values to be used to make predictions. 

- d: It is the number of differencing done to remove the non-stationary components.

- q: It is the order of the Moving Average (MA) sub-model. It refers to the number of past errors that an ARIMA Model can have when making predictions.

### Why do we use Auto ARIMA?
In an ARIMA model, we need to pass the p,d, and q values. We use statistical plots and techniques to find the optimal values of these parameters. We use statistical plots such as [Partial Autocorrelation Function plots](https://online.stat.psu.edu/stat510/lesson/2/2.2) and [AutoCorrelation Function plot](https://www.dummies.com/article/technology/information-technology/data-science/big-data/autocorrelation-plots-graphical-technique-for-statistical-data-141241/). 

The process of using statistical plots is usually hectic and time-consuming. Many people have difficulties in interpreting these plots to find the optimal parameter values. Wrong interpretation leads to wrong p,d, and q values and it affects the ARIMA model performance. 

Auto ARIMA automatically generates the optimal parameter values (p,d, and q). The generated values are the best and will help the model to give accurate forecast results. So basically Auto ARIMA will simplify the process of building a time series model using the ARIMA model.

Now we know how an ARIMA works and how Auto ARIMA applies its concepts. Let's now start exploring the time series dataset.

### Energy consumption dataset
We will use the energy consumption dataset to build the Auto ARIMA model. The dataset shows the energy demand from 2012 to 2017 which is recorded in an hourly interval. 

Download the time series dataset using this [link](https://drive.google.com/file/d/1l5MhAnlBYdp5Dk7EvcxzfGJFpvrwbbuw/view?usp=sharing). After downloading the time series dataset, let's load it using Pandas.

```python
import pandas as pd
```
To load the energy consumption dataset, run this code:

```python
df = pd.read_csv('energy_consumption.csv')
```

To visualize the dataset, use this code:

```python
df
```
Energy consumption dataset output:

![Energy consumption dataset](/engineering-education/multivariate-time-series-using-auto-arima/energy-consumption-dataset.png)

From this output, the `timeStamp`, `demand`, `precip` and `temp` columns. The columns are the variables that will build the time series model. The time series is multivariate since it has three-time dependent variables (`demand`, `precip` and `temp`)

The `timestamp` column shows the time the data point was recorded. The `demand` column shows the hourly energy consumption. The `precip` and `temp` columns correlate with the `demand` column. 

#### Converting the `timestamp` column
We need to explicitly convert the `timestamp` column to the DateTime format. It will enable us to perform time-series analysis and operations on this column. 

We will use the `pd.to_datetime` function.

```python
df['timeStamp']=pd.to_datetime(df['timeStamp'])
```
### Plotting the 'demand' column
Since we are forecasting the `demand`, we plot it to visualize the data points. It will enable us to check for trends or seasonality in the time series.

We will use the Plotly Express Python module to plot the line chart. Let's import the Plotly Express Python module.

```python
import plotly.express as px
```
We plot using the following code:

```python
fig = px.line(df, x='timeStamp', y='demand', title='Energy Consumption')

fig.update_xaxes(
        ])
    )
)
fig.show()
```
It plots the following line chart:

![Energy consumption plot](/engineering-education/multivariate-time-series-using-auto-arima/energy-consumption-plot.png)

From the image the dataset has seasonality. Repetitive cycles or spikes occur during the same period in the dataset. Since the dataset has seasonality, we can say it is non-stationary. But still, we need to perform an [Augmented Dickey-Fuller (ADF) test](https://www.machinelearningplus.com/time-series/augmented-dickey-fuller-test/) to check for stationarity in our dataset. The test will help us to statistically check the dataset.

If we find the dataset is non-stationary after the ADF test, we will have to perform differencing to make it stationary. Auto ARIMA will perform this process automatically. 

Let's set the `timeStamp` to be our index column. 

```python
el_df=df.set_index('timeStamp')
```
We set the `timeStamp` to be our index column for better interaction with the data frame. The Auto ARIMA model also expects the `timeStamp` to be the index column.

### Plotting subplots
The subplots will show the time-dependent variables in the dataset. We will visualize the `demand`, `precip`, and `temp` columns.

```python
el_df.plot(subplots=True)
```
It produces the following subplots.

![Subplots](/engineering-education/multivariate-time-series-using-auto-arima/sub-plots.png)

### Checking for missing or null values
We need to check for missing values in the dataset. Missing values affects the model and leads to inaccurate forecast results.

```python
print ("\nMissing values :  ", df.isnull().any())
```
Output:

![Checking missing values](/engineering-education/multivariate-time-series-using-auto-arima/check-missing-values.png)

From the output, all the columns have missing values. We have to have imputed the missing values so that we have a complete-time series dataset.

### Imputing missing values
We will first impute the missing values in the `demand` column. We will use the `fillna` method to impute the missing values in each of the columns.
 
#### Imputing 'demand' column
```python
df['demand']=df['demand'].fillna(method='ffill')
```
#### Imputing 'temp' column
```python
df['temp']=df['temp'].fillna(method='ffill')
```
#### Imputing 'precip' column
```python
df['temp']=df['precip'].fillna(method='ffill')
```
To learn more on how to impute missing values in time series, go through this [article](/engineering-education/missing-values-in-time-series/)

Let's check again for missing values. It will enable us to know if we have imputed the missing values in the time series. 

```python
print ("\nMissing values :  ", df.isnull().any())
```
![Checking missing values](/engineering-education/multivariate-time-series-using-auto-arima/rechecking-missing-values.png)

From the output, we have imputed the missing values in the time series.

### Dataset resampling
The time series has many data points which may be difficult to analyze and visualize each data point. We need to resample the time by compressing and aggregating it to monthly intervals. We will have fewer data points that are easier to work with. 

The `resample` method will aggregate all the data points in the time series and change them to monthly intervals. 

```python
el_df.resample('M').mean()
```
Dataset resampling output:

![Dataset resampling](/engineering-education/multivariate-time-series-using-auto-arima/dataset-resampling.png)

Let's plot new subplots of the resampled dataset.

### Plotting new subplots
We plot the new subplot as follows:
```pyton
el_df.resample('M').mean().plot(subplots=True)
```
![New subplots](/engineering-education/multivariate-time-series-using-auto-arima/new-subplots.png)

From these new subplots, we have resampled the dataset and have plotted fewer data points. It will easier to model these fewer data points. Let's save the resampled dataset in a new variable.

#### Saving the resampled dataset
We save the resampled dataset as follows:

```python
final_df=el_df.resample('M').mean()
```
This is the dataset we will use to train the time series model. We can now start implementing the Auto ARIMA model.

### Implementing the Auto ARIMA model
We implement the Auto ARIMA model using the [`pmdarima`](https://pypi.org/project/pmdarima/) time-series library. This library provides the `auto_arima()` function which automatically generates the optimal parameter values. 

Let's install the `pmdarima` using this command:

```bash
! pip install pmdarima
```
After installing, let's import it.

```python
import pmdarima as pm
```
The next step is to initialize the  `auto_arima()` function.

### Initialize 'auto_arima()' function
We initialize the  `auto_arima()` function as follows:

```python
model = pm.auto_arima(final_df['demand'], 
                        m=12, seasonal=True,
                      start_p=0, start_q=0, max_order=4, test='adf',error_action='ignore',  
                           suppress_warnings=True,
                      stepwise=True, trace=True)
```
In the `auto_arima()` function we pass the `final_df` which is our resampled dataset. We select the `demand` column since this is what the model wants to predict. 

The function can either use the [Grid Search technique](/engineering-education/grid-search/), or [Random Search technique](/engineering-education/random-search-hyperparameters/) to find the optimal parameter values. It tries multiple combinations of p,d,q and then selects the optimal one.

The `auto_arima()` function also has the following important parameters:
 
- `m=12`
It represents the number of months in a year.

- `start_p=0`
It is the start `p` value that can be selected during the random search.

- `start_q=0`
It is the start `q` value that can be selected during the random search.

- `max_order=4`
It is the maximum `p`, `d`, and `q` values that can be selected during the random search.

- `test='adf'`
It is an Augmented Dickey-Fuller (ADF) test to check for stationarity in our dataset. 

If the dataset is non-stationary after the ADF test, the `auto_arima()` function will automatically generate the `d` value for differencing. If the dataset will be stationary, then the function sets d=0 (no need for differencing).

- `suppress_warnings=True`
It ignores the warnings during the parameter searching. 

- `stepwise=True`
It will run the Random Search to find the optimal parameters. Grid Search is more exhaustive since it tries all the parameters combinations but it is slow. We opt to use Random Search which is faster.

When you run this code, the function will randomly search the parameters and produce the following output:

![Auto ARIMA output](/engineering-education/multivariate-time-series-using-auto-arima/model-output.png)

From this output, the best model is `ARIMA(1,0,1)`. p=1, d=0 and q=1. The function automatically sets d=0 because the ADF test found the dataset to be stationary.

We had previously observed the time series dataset plots to have seasonality. We, therefore, thought the time series dataset was non-stationary hence a need for differencing. 

But using the ADF test, which is a statistical test, found the seasonality to be insignificant. That is why the function sets d=0 and there is no need for differencing.

After initializing the `auto_arima()` function, the next step is to split the time series dataset. 

### Splitting the time series dataset
We split the time series dataset into a training data frame and a test data frame as follows:

```python
train=final_df[(final_df.index.get_level_values(0) >= '2012-01-31') & (final_df.index.get_level_values(0) <= '2017-04-30')]
```
The code selects the data points from 2012-01-31 to 2017-04-30 for model training. Let's select the data points for model testing.

```python
test=final_df[(final_df.index.get_level_values(0) > '2017-04-30')]
```
The data points from 2017-04-30 are for model testing. To display the test data points, use this code:

```python
test
```
![Test data frame](/engineering-education/multivariate-time-series-using-auto-arima/test-data-frame.png)

From the output, the test data frame has four data points. 

Let's fit the Auto ARIMA model to the train data frame.

### Fitting the Auto ARIMA model
Fitting the Auto ARIMA model to the train data frame will enable the model to learn from the time-series dataset. The final model after training will make future predictions.

```python
model.fit(train['demand'])
```
After training, it produces the following output:

![Auto ARIMA training](/engineering-education/multivariate-time-series-using-auto-arima/model-training.png)

The model is trained using the train data frame. It also uses the p,d, and q values that the `auto_arima()` function generates. Let's use the trained model to make predictions.

### Using the Auto ARIMA model to make predictions
The Auto ARIMA model will predict using the test data frame and the unseen future values. For prediction using the test data frame, we will have the actual energy demand and the predicted energy demand. 

#### Predicting the test data frame
We predict the test data frame as follows:

```python
forecast=model.predict(n_periods=4, return_conf_int=True)
```
- `n_periods=4`: Is the number of the data points in the test data frame that the model will predict. To see the predicted values use this code:

```python
forecast
```
![Predicted values](/engineering-education/multivariate-time-series-using-auto-arima/predicted-values.png)

We need to convert the predicted values to a Pandas data frame. It will easier to plot the Pandas data frame using Matplotlib.

```python
forecast_df = pd.DataFrame(forecast[0],index = test.index,columns=['Prediction'])
```
To see the Pandas data frame, run this code:

```python
forecast_df
```
It produces this output:

![Pandas data frame](/engineering-education/multivariate-time-series-using-auto-arima/pandas-data-frame.png)

Let's plot the Pandas data frame using Matplotlib.

#### Plotting the Pandas data frame
We import Matplotlib as follows:

```python
import matplotlib.pyplot as plt
```
We plot the line chart as follows:

```python
pd.concat([final_df['demand'],forecast_df],axis=1).plot()
```
It produces the following line chart:

![Line chart](/engineering-education/multivariate-time-series-using-auto-arima/test-data-frame-predictions.png)

From the line chart above:
- The blue line is the actual energy demand.
- The orange line is the predicted energy demand. 

The Auto ARIMA model has performed well, it has made accurate predictions. The blue and orange lines are close to each other. 

We can now use this model to predict the unseen future values.

#### Predict the unseen future values
To predict the unseen future values use this code:

```python
forecast1=model.predict(n_periods=8, return_conf_int=True)
forecast_range=pd.date_range(start='2017-05-31', periods=8,freq='M')
```
- `n_periods=8`
Is the number of data points the model will predict in the future. The future dates are from 2017-05-31. We also need to convert the predicted values to a Pandas data frame.

```python
forecast1_df = pd.DataFrame(forecast1[0],index =forecast_range,columns=['Prediction'])
```
Finally, let's plot the future predicted values using Matplotlib

#### Plotting the future predicted values
We plot the future predicted values as follows:

```python
pd.concat([final_df['demand'],forecast1_df],axis=1).plot()
```
It produces the following line chart:

![Prediction line chart](/engineering-education/multivariate-time-series-using-auto-arima/unseen-future-predictions.png)

From the line chart above:
- The blue line represents the actual energy demand.
- The orange line represents the predicted energy demand. 

The orange line also shows the unseen future predictions. The Auto ARIMA model has performed well, the orange line maintains the general pattern. 

### Conclusion
In this tutorial, We have learned how to build a multivariate time series model with AutoARIMA. We explored how the Auto ARIMA model works and how it automatically finds the best parameters of an ARIMA model. 

Finally, we implemented the Auto ARIMA model. We used the Auto ARIMA model to find the `p`, `d`, and `q` values. We used the trained Auto ARIMA model to predict the energy demand on the test data frame and the unseen future values. The final model made accurate predictions as observed in the plotted line chart.

You can get the full implementation of this tutorial in Google Colab [here](https://colab.research.google.com/drive/1X10JHyXMkUAWz_Z2wPngfa7PXUjzuVvf?usp=sharing)

### References
- [Auto ARIMA documentation](https://alkaline-ml.com/pmdarima/modules/generated/pmdarima.arima.auto_arima.html)
- [Pmdarima documentation](https://pypi.org/project/pmdarima/)
- [What is auto ARIMA?](https://medium.com/featurepreneur/what-is-auto-arima-b8025c6d732d)
- [ARIMA Model time series forecasting](https://www.machinelearningplus.com/time-series/arima-model-time-series-forecasting-python/)
- [ARIMA model definition](https://www.investopedia.com/terms/a/autoregressive-integrated-moving-average-arima.asp)
- [Hyperparameter Tuning](/engineering-education/hyperparameter-tuning-of-machine-learning-model-in-python)
- [Random Search technique](/engineering-education/random-search-hyperparameters/)
- [Grid Search technique](/engineering-education/grid-search/)
- [ARIMA model guide](https://machinelearningmastery.com/arima-for-time-series-forecasting-with-python/)
- [ARIMA models](https://otexts.com/fpp2/arima.html)
