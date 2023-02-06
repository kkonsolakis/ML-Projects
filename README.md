# ML-Projects
Data Science and Analysis


### Overview

For this example, data from smarthpone sensors (placed on the hip) will be used to build a model for predicting locomotion and transportation activities. To that end, the [SHL dataset](http://www.shl-dataset.org/download/#shldataset-preview) will be used to predict the following activities: 
'Still', 'Walking','Run', 'Bike', 'Car', 'Bus', 'Train', and 'Subway'.

In order to build and evaluate an activity recognition system, a sequence of steps is required. 
These steps include data  acquisition,  data  processing,  data segmentation, features extraction, data imputation, features selection, classification, and validation. The following lines of code are performed with Python.

### Methodology

1. **Data Acquisition**: Based on literature, it is highly recommended to use sensor data related to accelerometer, gyroscpose and GPS location for predicting activities related to locomotion and transportation. Here, the focus will be on accelerometer, gyroscope, magnetometer, and GPS data obtained from the [SHL dataset](http://www.shl-dataset.org/download/#shldataset-preview).
2. **Data Processing**: Here data are cleaned and prepared for the next phases. Furthermore, GPS data features (i.e., speed and distance) are calculated based on the Haversine Distance of the GPS coordinates. 
3. **Data Segmentation**: here the sensor data are divided into different frames. Based on literature, it is recommended a window segment of ~5sec with 50% overlap. Here, a sliding window of size 6 seconds with half overlap is chosen to meet the criteria for sensor fusion (by merging motion data and GPS).
4. **Features Extraction**: different time and frequency domain features are extracted for each sensor recording. Based on literature, I decided to compute the following features. For the accelerometer
I computed mean, std, magnitude, fftfreq (peak frequencies based on fast fourier), signal power, entropy. For the gyroscope I computed mean, std, and magnitude. For the magnetomer I computed std, magnitude. For the GPS I computed the mean values. A description of these features can be found on the following section (see Reference [1](https://repository.tudelft.nl/islandora/object/uuid%3Aaf2e1786-ccc4-4592-afc8-b19819544f26)). Furthermore, missing GPS data are imputed. 
5. **Features Selection**: here non-informative features are excluded. At first highly correlated features (with an absolute correlation >=0.9) are removed. Then, a feature selection model (based on sklearn feature importance score) is also used to remove features with the lowest information gain.
6. **Classification**: The Random Forest is used to train the prediction model. Since the focus is not on how to optimise the classificaiton model, I will not focus on optimising the hyperparameters or on evaluating other algorithms.
7. **Validation**: The StratifiedShuffleSplit split from sklearn is used to split the data into 10 different train/test sets (10-fold cross- validation). Different metrics are used, such as precision, recall, f1-score, and confusion matrix.

### Background Information & Related Work
For this solution, different studies in literature were considered. Mainly, I focused on the followings:
1. [Physical Activity Recognition using Wearable Accelerometers in Controlled and Free-Living Environments](https://repository.tudelft.nl/islandora/object/uuid%3Aaf2e1786-ccc4-4592-afc8-b19819544f26) (my MSc thesis graduation project about activity recognition)
2. [A systematic review of smartphone-based human activity recognition methods for health research](https://www.nature.com/articles/s41746-021-00514-4)
3. [The University of Sussex-Huawei Locomotion and
Transportation Dataset for Multimodal Analytics
With Mobile Devices](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8418369)
