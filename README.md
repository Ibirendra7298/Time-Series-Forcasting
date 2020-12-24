# Time-Series-Forcasting
Time series forcasting of traffic on JetRail.

## Introduction
Time Series is considered to be one of the less known skills in the data science space (Even I had little clue about it a couple of days back). I set myself on a journey to learn the basic steps for solving a Time Series problem and here I am sharing the same with you. These will definitely help you get a decent model in any future project you take up!.

## Table of Contents:
    1. What makes Time Series Special?
    2. Loading and Handling Time Series in Pandas
    3. How to Check Stationarity of a Time Series?
    4. How to make a Time Series Stationary?
    5. Forecasting a Time Series
    
## 1. What makes Time Series Special?
As the name suggests, TS is a collection of data points collected at constant time intervals. These are analyzed to determine the long term trend so as to forecast the future or perform some other form of analysis. But what makes a TS different from say a regular regression problem? There are 2 things:
  1. It is **time dependent**. So the basic assumption of a linear regression model that the observations are independent doesn’t hold in this case.
  2. Along with an increasing or decreasing trend, most TS have some form of **seasonality trends**, i.e. variations specific to a particular time frame. For example, if you see   the sales of a woolen jacket over time, you will invariably find higher sales in winter seasons.
  
Because of the inherent properties of a TS, there are various steps involved in analyzing it. These are discussed in detail below. Lets start by loading a TS object in Python. We’ll be using the popular AirPassengers data set.

## 2. Loading and Handling Time Series in Pandas
Pandas has dedicated libraries for handling TS objects, particularly the datatime64[ns] class which stores time information and allows us to perform some operations really fast. Lets start by firing up the required libraries:

> # importing required libraries
import pandas as pd
import numpy as np

# Now, we will load the data set and look at some initial rows and data types of the columns:
data = pd.read_csv('AirPassengers.csv')
print (data.head())
print ('\n Data Types:')
print (data.dtypes)

# The data contains a particular month and number of passengers travelling in that month. In order to read the data as a time series, we have to pass special arguments to the read_csv command:
dateparse = lambda dates: pd.datetime.strptime(dates, '%Y-%m')
data = pd.read_csv('AirPassengers.csv', parse_dates=['Month'], index_col='Month',date_parser=dateparse)
print ('\n Parsed Data:')
print (data.head())

