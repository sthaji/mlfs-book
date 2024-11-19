This laboration predicts pm25 values for St-eriksgatan, Stockholm, Sweden, based on weather data and up to three days previous pm25 values. 

Scripts: 
- 1_air_quality_feature_backfill.ipynb
    - Takes in historical weather data and pm values
    - Cleans data and creates new columns 
    - creates two feature groups saved in Hopsworks
- 2_air_quality_feature_pipeline.ipynb
    - Gets todays pm25 value, adds lagging values from previous days to new data row
    - Gets forecasted weather data
    - inserts new values into feature groups in Hopsworks
- 3_air_quality_batch_inference.ipynb
    - Creating a feature view by combining different columns from feature groups
    - creates a schema for a xgboost model
    - trains and tests the model
    - saves the model in a model registry in Hopsworks
- 4_air_quality_batch_inference.ipynb
    - Get weather forecast data and pm25 data from feature group
    - batch inference sequentially using weather forecast data + lagging values from each day before
    - Saving predictions to a feature group for monitoring 
    - based on monitored values, for those days we have both a predicted value and actual value, add to a hindcast graph (1 new data point added everyday)