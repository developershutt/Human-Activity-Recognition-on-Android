# Human-Activity-Recognition-on-Android

__Note__:This repository is for training neural network classifier.

## Required packages

* pip3 install tensorflow==2.3.0
### or
* pip3 install tensorflow-gpu==2.3.0
* pip3 install keras==2.4.3
* pip3 install pandas
* pip3 install numpy==1.19.1
* pip3 install pyunpack
* pip3 install patool

## 0. I've made a video too with animated explanation and code for people who are lazy enough to read all text below.

[![yYoutube Video](https://github.com/developershutt/Human-Activity-Recognition-on-Android/blob/master/images/Thumbnail.png)](https://www.youtube.com/watch?v=_OJpKnFqUes)


## 1. About the dataset
* The dataset contains sensor values from Acceletometer, Linear Acceleration Sensor and Gyroscope sensor.
* For each timestamp the dataset contains activities as labels corresponding to each data point.
* The dataset has been recored on following activities: 
	* Walking
	* Standing
	* Jogging 
	* Sitting
	* Biking
	* Upstairs
	* Downstairs

* Download the dataset [here](https://www.utwente.nl/en/eemcs/ps/dataset-folder/sensors-activity-recognition-dataset-shoaib.rar)

## 2. Visualization of sensors data

* The visualizations below are plotted values of X-Y and Z axis with respect to activities.

__Note__: Since the dataset was large, I took only 100 samples from starting for each activity to demonstrate.

![during walking](https://github.com/developershutt/Human-Activity-Recognition-on-Android/blob/master/images/during_walking.jpg)

![during jogging](https://github.com/developershutt/Human-Activity-Recognition-on-Android/blob/master/images/during_jogging.jpg)

![during standing](https://github.com/developershutt/Human-Activity-Recognition-on-Android/blob/master/images/during_standing.jpg)

![during biking](https://github.com/developershutt/Human-Activity-Recognition-on-Android/blob/master/images/during_biking.jpg)

## 3. Data Preprocessing
	
__Step 1__: Since the dataset was divided into 10 files which was collected by 10 different people by using their devices, all those files concatenated into one single file

__Step 2__: Split the dataset into Train and Validation distribution.

__Step 3__: Encode the labels into numbers.

__Step 4__: Since the data collected by sensors on each timestamp are continous in nature, it's better to convert them into Time Series data so that it can fit as a sequence on a timestamp in LSTMs or GRUs (continous models). 

__Note__: We do not use any discrete modeling because the prediction cannot be made by just observing a single datapoint.

## 4: About Model
	
* The architecture of model is following:
__Layer 1__: The first layer is a LSTM layer for learning from sequence of 100 points at each timestamp are returns the sequence mapping as well.
__Layer 2__: Flatten layer is used to 2 dimensional (Number of timestamps, Number of features) output from above LSTM layer and convert it into 1-d vector
__Layer 3__: From this layer onwards the classifier part is starting which is a Dense layer that takes flatten output from above layer and pass it to __Layer 4__.
__Layer 4__: This is softmax layer taking input from __Layer 3__ and predict the probability corresponding to each activities.

* The model used __Categorical Crossentropy__ for loss measure and __Adam__ or __Adaptive Momemtum__ as a gradient descent optimizer.

* It has been trained for 5 __epochs__ with __ModelCheckpoint__ callback for saving best model while training.


## 5. Export to Proto Buffer file

* The reason behind exporting Hadoop (h5) format file to Proto Buffer file (.pb) is just because it is lightweight and supported by __Tensorflow Mobile__ for deployment in Android devices.

## 6. Deployment

* The model has been deployed on and Android Device using __Tensorflow Mobile__ for tracking human activities in real-time.

* If you want deployment of the model in Android. [See this repository](https://github.com/manish29071998/HAR_Android)

## Don't forget to leave a star if you liked it.
## PRs are welcome.
