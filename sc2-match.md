---
layout: writeup
title: StarCraft2 Match Predict
subtitle: https://sc2predict.herokuapp.com/
image: /img/sc_gm_mid.PNG
gh-repo: https://github.com/mjh09/match-predict
---
  In the realm of StarCraft Esports and other sporting events abroad, predictions and betting go hand-in-hand.  With the help of community-sourced data of online and offline tournaments, I have created an app that enables users to generate predictions.

**Language:** Python(pandas, numpy, sklearn, xgboost)
**Framework:** Dash

### The Data
 **Aquisition and Formating:**<br/>
  The data source, [Aligulac](http://aligulac.com/), has a simple method of extraction: PostgreSQL database dump. Restoring the dump file to a local database and exporting relevant tables to CSV files was made easy by the pgAdmin GUI.

![](/img/psql_export.PNG)

  **Data Wrangling and Baseline Prediction:**<br/>
  Isolating a select feature set required a handful of useful Pandas operations. I filtered off games played before the LOTV expansion, created a new column to represent the winning player, and merged two tables to house the match and player rating information. A baseline classification prediction was made from the summary statistics.

![](/img/sc2_baseline_predict.PNG)

### The Model
**Training and Inference:**<br/>
The training and validation split was done at a 75/25 ratio. The data split was stratified across the target column to ensure equal distributions of classification values. To make inferences, an XGBClassier algorithm was chosen. Tuning the hyper-parameters of the model involved a round of randomized-search cross-validation using classification accuracy as the target evaluation metric. The trained model achieved an 82% accuracy score on the hold out data; a nearly 20% increase from the majority baseline.
 
 ![](/img/sc2_model_accuracy.PNG)
 
### Deployment
 **Dash and Heroku:**<br/>
  I trimmed the feature set by permutation importance, leaving the top two predictive features for the deployed model: Player A and B's smoothed rating. These features had roughly 3X the predictive power as any other stand-alone data column. The Dash library makes bootstrapping the front-end simple. Getting under Heroku's free-tier memory limit didn't cause problems with the pickled model. Check the links below for the deployed app(give Heroku time to spin-up the server).
  
 ![](/img/sc2_feature_importance.PNG)
  
### Restrospective
 **Hypothesis and TO-DO's:**<br/>
  Firstly, I'd like to implement a pipeline of varying model types. I'm curious about the circumstances that lead to a lesser rated player winning, whether it's more prevalent in a race v race scenario, and how the distribution looks across balance patches. Treating the data with a tighter time series window might also prove helpful. I can imagine a model trained with the most recent results having more predictive power. That being said, I've yet to test the model against new data.

  
Links: [Web App](https://sc2predict.herokuapp.com/) ---  [Github Repo](https://github.com/mjh09/aligulac_project)
