# How to Predict When There Are *Really* Few Positives? - Predictive Maintenance for Pumps
## What is it all about?
Here, you find an analysis of [pump_sensor_data](https://www.kaggle.com/nphantawee/pump-sensor-data/) posted on Kaggle. Its all about predicting pump breakdowns early on to have 
enough time for maintenance work. This will *reduce* downtimes and *costs* as complete breakdowns are harder to fix. The challenge is that there are only very few breakdowns to learn from. And, there are a great many sensor data of unknown type. They need to be translated into actionable signals that allow to minimize maintenance costs while keeping pumps healthy.
## Executive Summary
- Single sensors provide contradictory signals. 
- A composite indicator based on the number of sensors that significantly deviate from their normal behaviour would necessitate an objective rule that is hard to find and lead to many falls alarms. 
- Predicting breakdowns directly through an AI model is not reliable enough and testing is difficult as only few breakdowns are available. 
- An indicator based on the probabilities of the same predictions is promising.
## Resources 
**There is a slide show**! Obviously, there is a [notebook](https://github.com/dullibri/pump_sensor/blob/main/pump_sensors.ipynb) containing the steps and a [requirements.txt](https://github.com/dullibri/pump_sensor/blob/main/requirements.txt) to replicate the results. 
As a bonus, you also find an [html presentation](https://github.com/dullibri/pump_sensor/blob/main/pump_sensors.slides.html) produced with jupyter slides.
Make sure to download it to view it properly. For completeness, the [data](https://github.com/dullibri/pump_sensor/blob/main/pump_sensors.rar) are also uploaded here.
## The Set-up: 
- 53 sensors for one pump sending their measurements by the minute for about 153 days (~220k minutes). 
- The aim is to predict when a pump is down as early as possible to start maintenance.
- However, out of the 220k minutes it breaks only 7 minutes and is recovering 14.477 or 10 days in total.

## Approaches
### Looking at single indicators
![Is this a good indicator?](sensor_and_breakdowns.png?raw=true)

Note: Breakdowns are depicted with solid red lines, shaded areas indicate recovery periods.

**Points to consider**

- Unreliable and prone to false alarms.

## Indicator Approach

- When did sensors deviate significantly (5 %-level) from normal state.
- How many sensors deviated
- Here: Mean of rolling window of 2 days.

![Indicator](indicator_approach.png?raw=true)

**Points to consider**

- Many False Alarms
- There seems to be a time trend (age of pumps)
- An objective rule (still) needs to be developed, when to go looking after pumps.

## ML-Approach

### Predicting online

- is it possible to predict breakdowns online?
- Prediction horizon: 2 days.
- Simple Logistic Regression, untuned.
- split into 75 % Training (5 breakdowns), 25 % Test (2 breakdowns)

![](training_ml.png?raw=true)

- However, the test result only captures one of the two breakdowns.

![](test.png?raw=true)


## Early Warning Indicator

- Give maintenance staff an early indicator of 2d.
- Point forecasts of breakdowns failed so far.
- Probabilities of breakdown, however, serve as early warning indicator.

![](early_indicator.png?raw=true)

## Next Steps

- Use different ML-Models, including LSTM.
- Fine-tune models
- Use early-warning indicator and/or deviation-indicator in models.
- Use PCA to shrink number of regressors










