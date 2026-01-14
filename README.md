# Predict stocks

Building AI course project

## Summary

The system predicts whether a stock's price will rise or decrease the following week. The user selects which stock will be predicted and, optionally, the characteristics of the data used to make the prediction.

## Background

* Stocks' prediction is valuable for profitable investments.
* It is very difficult to predict stocks only with stocks' data because their behaviour is highly random.
* The purpose of this system is to predict the movement of stocks only with stocks' data.

## How is it used?

The user-defines parameters for the data to use such as market, segment, sector, currency, and time-span. From these data the user select a stock to predict. On the last day of a given week the system will predict if at the beginning of the following week the stock's price will be higher or lower than at the beginning of the current week.

## Data sources and AI methods

The system collects stcoks' historical prices publicly available on the internet, from [https://www.nasdaq.com/european-market-activity/shares](Nasdaq's webpages for european activity). 
Then, it pre-processes the data to interpolate missing data with less consecutive missing points that 6 days per stock. Otherwise the data for the whole stock is removed. 
From the pre-processed data, features and outcomes are extracted. Features are prices for all stocks during one week. The outcome is whether the price on the first day of the following week is higher or lower/equal than the first day of the current week. This is done for all weeks.
The data is split into training and testing subsets. The training data is fed to an artificial neural network composed by two hidden layers with ReLU activation. The outcput layer is only one node, with sigmoid activation. The network is trained iteratively with the backpropagation technique, until it reaches the minimum error. The error is calculated with the "binary cross entropy" formula, which is appropriate for sigmoid activation. Also, the network is initialised with the Kaiming He technique, which is appropriate for ReLU. 

A proof of concept is provided, with two modules:
* [data collection](https://github.com/juigmend/Predict-stocks-with-vanilla-network/blob/main/Web_Scraping_Data_Nasdaq_Europe.ipynb)
* [training and testing](https://github.com/juigmend/Predict-stocks-with-vanilla-network/blob/main/ANN_predict_stocks_movement.ipynb)

Spoiler alert: The system is not able to predict :/

## Challenges

The described system was tested with different combinations of data (e.g., time-range, number and type of stocks, rescaling of prices) and network parameters (e.g., ReLU leak, nodes per hidden layer, learning rate), but it is not able to predict. It either converges in only ones, only zeros, or seemingly random outcomes. 

## What next?

The next step would be to do a literature review to search for better ways to do the stock prediction and implement methods that have been shown to be successful. A preliminary literature reviwe shows that there are published studies that have addressed the problem with some success (Ji, S. (2024). "Predict stock market price by applying ANN, SVM and Random Forest").
