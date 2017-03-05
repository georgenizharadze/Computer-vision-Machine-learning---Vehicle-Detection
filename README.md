# Computer vision and Machine learning - Vehicle Detection Project


### The goals / steps of this project

The utlimate goal of this project is to write a software pipeline to detect vehicles in a video (start with the test_video.mp4 and later implement on full project_video.mp4). The more detailed goals and steps are as follows: 

* Perform a Histogram of Oriented Gradients (HOG) feature extraction on a labeled training set of images and train a Linear SVM classifier
* Optionally, a color transform can be performed and binned color features, as well as histograms of color, can be added to the HOG feature vector.
* Note: for the first two steps it's important to normalize the features and randomize a selection for training and testing.
* Implement a sliding-window technique and use the trained classifier to search for vehicles in images.
* Run the pipeline on a video stream (start with the test_video.mp4 and later implement on full project_video.mp4) and create a heat map of recurring detections frame by frame to reject outliers and follow detected vehicles.
* Estimate a bounding box for vehicles detected.
  
Below I will address each of the above points.

[//]: # (Image References)
[image1]: ./output_images/sample_car_not_car.jpg
[image2]: ./output_images/car_not_car_HOGs.jpg
[image3]: ./output_images/car_not_car_HOGs2.jpg
[image4]: ./output_images/car_not_car_HOGs3.jpg



### HOG feature extraction 

First, I used the glob function and read in the [vehicle](https://s3.amazonaws.com/udacity-sdc/Vehicle_Tracking/vehicles.zip) and  [non-vehicle](https://s3.amazonaws.com/udacity-sdc/Vehicle_Tracking/non-vehicles.zip) image file names sourced from the [GTI vehicle image database](http://www.gti.ssr.upm.es/data/Vehicle_database.html) only. I ended up with a total of 8,792 and 3,900 vehicle and non-vehicle image files, respectively. The code for this step is contained in the first section of my Vehicle-detection.ipynb Jupyter notebook. 

Below is an example of randomly selected vehicle and non-vehicle images:

![alt text][image1]

Below are the visualizations of several HOG features extracted through various color spaces, using 8 orientations, 8 pixels per cell and 2 cells per block: 

![alt text][image2]
![alt text][image3]
![alt text][image4]

