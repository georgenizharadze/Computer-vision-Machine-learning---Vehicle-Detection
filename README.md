# Computer vision and Machine learning - Vehicle Detection Project

## The goals / steps of this project are the following:

* Perform a Histogram of Oriented Gradients (HOG) feature extraction on a labeled training set of images and train a classifier Linear SVM classifier
* Optionally, apply a color transform and append binned color features, as well as histograms of color, to the HOG feature vector. 
* Note: for the first two steps it's important to normalize the features and randomize a selection for training and testing.
* Implement a sliding-window technique and use the trained classifier to search for vehicles in images.
* Run the pipeline on a video stream (start with the test_video.mp4 and later implement on full project_video.mp4) and create a heat map of recurring detections frame by frame to reject outliers and follow detected vehicles.
* Estimate a bounding box for vehicles detected.

## Here I will consider the project goals and steps individually and describe how I addressed each point in my implementation.

### Histogram of Oriented Gradients (HOG)

####1. Extraction of HOG features from the training images

I read in all the labeled vehicle and non-vehicle file names, with the use of the glob function, from the GTI Vehicle Image Database files. This gave a total of 8,792 and 3,900 vehicle and non-vehicle images, respectively. Below is an example of 
