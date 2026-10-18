---
layout: post
title: "Predicting the Range per kWh of Electric Buses with Machine Learning"
date: 2025-08-13
tags: [Data Science]
---

*Data science term project (Hausarbeit), M.Sc. Business Informatics, Ostfalia University of Applied Sciences. Original language: German.*

**Files:** [Jupyter notebook (German)](https://github.com/HaDa99/HadiDahnoun.github.io/blob/main/assets/projects/ev-range-regression/EV_Reichweite_Regression.ipynb) · [Dataset (CSV)]({{ '/assets/projects/ev-range-regression/data/all_fused_vehicle_data.csv' | relative_url }})

---

## The question

How far can an electric vehicle drive per kilowatt-hour, and what drives that efficiency? This project builds regression models that predict **range per kWh** (miles per kWh) from trip conditions such as driving share, speed, ambient temperature and the individual vehicle.

The best model, a tuned random forest, explains about **75% of the variance** in range per kWh on unseen test data (R² = 0.75, MAE = 0.047 mi/kWh).

## The data

The dataset contains mostly numeric operating data from 36 electric vehicles, school buses and public transit buses in the US, with 19,922 trip records and 31 columns. The most important columns:

- **Total Distance** (miles), **Driving Time** and **Idling Time** (hours), **Total Run Time** (hours)
- **SOC Used** (state of charge used, %) and **Total Energy Consumption** (kWh)
- **Average Speed** (mph) and **Average Ambient Temperature** (°F)
- **Vehicle ID**

Two features were derived:

- **Range per kWh** = Total Distance ÷ Total Energy Consumption (the target)
- **Driving Time %** = Driving Time ÷ Total Run Time × 100

## Data preparation

1. **Missing values:** rows missing any of the key columns (SOC, idling and driving time, distance, speed, temperature, energy) were dropped rather than imputed, because too many values were missing for median or mean filling to make sense. 6,875 rows remained.
2. **Implausible trips:** only trips longer than 2 miles and with energy consumption between 1 and 500 kWh were kept. Very short trips give unreliable consumption values, and more than 500 kWh in a day points to a defect or a measurement error. 4,001 rows remained.
3. **Plausibility checks:** driving share (0–100%), average speed (0–45 mph), temperature (about 7–102 °F, i.e. −14 to 39 °C) and run times of up to 20+ hours (several driver shifts with breaks) were all plausible.
4. **Outliers in the target:** an IQR analysis found outliers in range per kWh, but no direct link to speed or driving share. Only the few extreme values below 0.2 or above 2 mi/kWh were removed; the remaining, still plausible outliers were kept for training. 3,971 rows remained.

## Exploration

![Range per kWh against speed, temperature, driving share, vehicle, distance and run time]({{ '/assets/img/ev-range/range-vs-features.png' | relative_url }})
*Range per kWh against the candidate features. Efficiency differs clearly between vehicles.*

A first observation: different vehicles do not consume the same amount of energy. The correlation matrix (excluding distance and energy, since the target is computed from them) shows moderate positive correlations of range per kWh with driving share (0.32), average speed (0.31), vehicle (0.30) and temperature (0.23), and a negative one with total run time (−0.22).

![Correlation matrix of range per kWh and the selected features]({{ '/assets/img/ev-range/correlation-heatmap.png' | relative_url }})

## Modelling

**Features:** Driving Time %, Average Speed, Average Ambient Temperature, Total Run Time and the vehicle. The vehicle was one-hot encoded so that linear regression doesn't misread vehicle numbers as quantities. **Split:** 80% training, 20% test (about 4,000 rows, so 20% gives a good balance between robust training and reliable evaluation).

Three model types were compared:

| Model | Test MAE (mi/kWh) | Test RMSE | Test R² |
|---|---|---|---|
| Linear regression (one-hot vehicle) | 0.058 | 0.082 | 0.633 |
| Decision tree (max depth 5) | 0.071 | 0.101 | 0.449 |
| Random forest, 100 trees (one-hot vehicle) | 0.050 | 0.074 | 0.704 |
| Random forest, 100 trees (vehicle as integer code) | 0.048 | 0.070 | 0.736 |
| **Random forest, tuned with GridSearchCV** | **0.047** | **0.068** | **0.747** |

Scaling the features in a pipeline did not change the linear regression results, as expected for ordinary least squares.

For the random forest, one-hot encoding the vehicle added 35 extra columns for 36 vehicles. The trees then needed many more splits to capture the same vehicle groups, which increased variance, so keeping the vehicle as a single integer code gave a better test score. The linear regression, by contrast, performed poorly with integer codes, so one-hot encoding stayed the right choice there.

**Hyperparameter tuning:** a 5-fold GridSearchCV over `n_estimators`, `max_depth`, `min_samples_split` and `min_samples_leaf` selected 200 trees, max depth 20, min samples split 2 and min samples per leaf 4.

![Tuned random forest: actual vs predicted range per kWh]({{ '/assets/img/ev-range/rf-actual-vs-predicted.png' | relative_url }})
*Tuned random forest on the test set. Predictions follow the ideal line well up to about 0.7 mi/kWh and underestimate the most efficient trips.*

## Out-of-sample predictions

Five hypothetical trips were scored with the tuned model. The predicted ranges fall in a plausible band of 0.32 to 0.77 mi/kWh. A higher share of driving time (less idling) and warmer temperatures increase the predicted range.

| Scenario | Driving time % | Avg speed (mph) | Temp (°F) | Run time (h) | Predicted range (mi/kWh) |
|---|---|---|---|---|---|
| Cold, slow, medium run time | 65 | 22 | 30 | 9.0 | 0.32 |
| Warm, fast, long run time | 80 | 50 | 96 | 12.0 | 0.77 |
| Shorter trip, slow, moderate | 50 | 27 | 65 | 6.5 | 0.44 |
| Very high driving share, efficient | 90 | 35 | 65 | 10.0 | 0.48 |
| Mostly idling, very cold | 30 | 35 | 10 | 5.0 | 0.48 |

Each scenario also uses a specific vehicle code. The "warm, fast" scenario's 50 mph lies above the highest average speed in the training data (about 42 mph), so that prediction is an extrapolation, which random forests handle only by falling back on the nearest values they have seen.

## Takeaways

- Range per kWh of electric buses can be predicted reasonably well from a few operational features; vehicle-specific differences matter a lot.
- Tree ensembles beat linear models here, and for random forests a compact integer encoding of the vehicle worked better than one-hot encoding.
- The model is weakest for the most efficient trips, where training data is sparse.
