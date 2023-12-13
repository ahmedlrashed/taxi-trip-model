![taxistand](figs/taxi_stand.jpg)
#  Taxi Fare Prediction Model
This project's goal is to build a regression model that predicts taxi cab fares before each ride based on distance, time of day, and any additional variables we find necessary.
### TLDR Presentation [LINK](https://docs.google.com/presentation/d/1I3PJeAL6wSCZCT8FXa4GtsFjZeRMaZ67nGlbKEv-jzA/edit?usp=sharing).
</br></br>

# Table of Contents

1. [Exploring the Dataset](#1-|-Exploring-the-Dataset)
1. [Statistical Analysis](#2-|-statistical-analysis)
1. [Building the Model](#3-|-Building-the-Model)
1. [Conclusions](#4-|-conclusions)
1. [Dependencies](#5-|-dependencies)
1. [Author](#6-|-author)
1. [License](#7-|-license)
1. [Acknowledgements](#8-|-acknowledgements)
</br></br>

# 1 | Exploring the Dataset
The goal of this first notebook is to perform a cursory inspection of  the 2017 Yellow Taxi Trip data.

After looking at the dataset, the two variables that are most likely to help build a predictive model for taxi ride fares are total_amount and trip_distance because those variables show a picture of a taxi cab ride.
</br></br>

# 2 | Statistical Analysis
The goal of this second notebook is to characterize and clean the 2017 Yellow Taxi Trip data set and to create a visualization to share to stakeholders.
- We will use box plots to determine outliers and where the bulk of the data points reside in terms of trip_distance and total_amount.
![tripbox](figs/trip_boxplot.jpg)
![totalbox](figs/total_boxplot.jpg)
</br></br>
- We will use histograms to visualize the trends and patters and outliers of critical variables, such as trip_distance and total_amount.
![triphist](figs/trip_histogram.jpg)
![totalhist](figs/totals_histogram.jpg)
</br></br>
- We will use bar charts to determine daily and monthly revenue and number of trips.
![revday](figs/revenue_daily.jpg)
![revmon](figs/revenue_monthly.jpg)
![rideday](figs/rides_daily.jpg)
![ridemon](figs/rides_monthly.jpg)
</br></br>

### EDA Presentation [LINK](https://docs.google.com/presentation/d/1I3PJeAL6wSCZCT8FXa4GtsFjZeRMaZ67nGlbKEv-jzA/edit?usp=sharing).
</br></br>

# 3 | Building the Model
Many of the features will not be used to fit our model, so the most important columns to check for outliers are likely to be:

- `trip_distance`
- `fare_amount`
- `duration`

#### Create `mean_distance` column

When deployed, the model will not know the duration of a trip until after the trip occurs, so we cannot train a model that uses this feature. However, we can use the statistics of trips we _do_ know to generalize about ones we do not know.

In this step, we will create a column called `mean_distance` that captures the mean distance for each group of trips that share pickup and dropoff points. To calculate this, we will first create a helper column called `pickup_dropoff`, which contains the unique combination of pickup and dropoff location IDs for each row. Then we will replace each unique pickup_dropoff KEY with its mean_distance VALUE.

#### Create `rush_hour` column

Define rush hour as:
* Any weekday (not Saturday or Sunday) AND
* Either from 06:00&ndash;10:00 or from 16:00&ndash;20:00

Create a binary `rush_hour` column that contains a 1 if the ride was during rush hour and a 0 if it was not.

#### Pre-process the data
Dummy encode categorical variables. Create training and testing sets. The test set should contain 20% of the total samples. 

#### Build and evaluate model
Instantiate our model and fit it to the training data. Evaluate our model performance by calculating the residual sum of squares and the explained variance score (R^2). Calculate the Mean Absolute Error, Mean Squared Error, and the Root Mean Squared Error.
</br></br>

## Observations & Patterns
- A/B Test analysis shows that there is a statistically significant difference between the fare_amount for the credit card payment_type vs the cash payment_type. This suggests there might be more profitable for the taxi company to encourage payments by credit card.

- However, this assumes that passengers were forced to pay one way or the other, and that once informed of this requirement, they always complied with it. The data was not collected this way; so the   randomly grouped data entries to perform an A/B test was based on   an assumption that might necessarily be true.

- This dataset does not account for other likely explanations. For example, riders might not carry lots of cash, so it's easier to pay for longer, long-distance trips with a credit card. In other words, it's far more likely that fare amount determines payment type, rather than vice versa.

- The model performance is high on both training and test sets, suggesting that there is little bias in the model and that the model is not overfit. In fact, the test scores were even better than the training scores. For the test data, an R2 of 0.868 means that 86.8% of the variance in the `fare_amount` variable is described by the model.
</br></br>

# 4 | Conclusions

As expected, the model shows a direct linear relationship between distance_traveled and fare_amount. For every 3.57 miles traveled, the fare increased by a mean of $7.13. Or, reduced: for every 1 mile traveled, the fare increased by a mean of $2.00.
</br></br>

# 5 | Dependencies
* python = "^3.10"
* numpy = "^1.25"
* pandas = "^2.0"
* matplotlib = "^3.8.0"
* seaborn = "^0.13.0"
* scipy = "^1.11.3"
* scikit-learn = "^1.3.1"
</br></br>

# 6 | Author
[Ahmed L Rashed](https://ahmedlrashed.github.io)
</br></br>

# 7 | License
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
</br></br>

# 8 | Acknowledgements
* [Coursera](https://www.coursera.org/) for hosting the dataset
