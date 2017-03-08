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
[image5]: ./output_images/sliding_window_search.jpg 



### HOG feature extraction and Support Vector Classifier (SVC) training 

First, I used the glob function and read in the [vehicle](https://s3.amazonaws.com/udacity-sdc/Vehicle_Tracking/vehicles.zip) and  [non-vehicle](https://s3.amazonaws.com/udacity-sdc/Vehicle_Tracking/non-vehicles.zip) image file names sourced from the [GTI vehicle image database](http://www.gti.ssr.upm.es/data/Vehicle_database.html) and [KITTI vision benchmark suite](http://www.cvlibs.net/datasets/kitti/). I ended up with a total of 8,792 and 8,968 vehicle and non-vehicle image files, respectively. The code for this step is contained in the first section of my Vehicle-detection.ipynb Jupyter notebook. 

Below is an example of randomly selected vehicle and non-vehicle images:

![alt text][image1]

Below are example visualizations of HOG features extracted through the use of YCrCb, HSV and HLS color spaces, using 8 orientations, 8 pixels per cell and 2 cells per block. We can see by eye that the dominant gradients do give a meaningful indication of the presence of a vehicle, contrasted with the relatively uniform gradient pattern of the non-vehicle images. 

![alt text][image2]
![alt text][image3]
![alt text][image4]

I trained the SVC classifier on 90% of the vehicle (8,792) and non-vehicle (8,968) images mentioned above. The remaining 10% was held out for classifier testing. I tried various feature combinations and color spaces. The best accuracty results I obtained on the testing data was 99.2% for YCrCb space and 99.4% for LUV space. The rest of the parameters used were: 

* 9 orientation bins for HOG
* 8 pixels per cell 
* 2 cells per block 
* Used all HOG channels 
* Spatial size for color features: (16, 16) 
* Color histogram bins: 16   

With these parameters, the total number of features ended up at 6,108. All features were scaled / normalized at zero mean and unit variance prior to training. The classifier training and testing code can by found in section 2 (titled _Classifier Training_) of my Jupyter Notebook.

### Sliding window search

The functions which I used for sliding window search are defined under the section _Sliding Window Search_ in my Jupyter Notebook. These are three functions, `slide_window`, which inspects the image step by step by sliding a square window across and down, `search_windows`, which runs a class (vehicle vs. non-vehicle) prediction with the previously trained classifier on each area of the image delineated by the window and `draw_boxes`, which draws a rectangle around the window classified as a vehicle. 

I applied these functions and looped through the test images in the test\_images folder. I used an overlap value of 0.5 between windows. To optimize the classification process, I (i) restricted the search to the bottom half of the image, i.e. the road and (ii) simultaneously searched with three different window sizes, (64, 64), (96, 96) and (112, 112), to capture both closer and farther vehicles. Below are the results:

![alt text][image5]