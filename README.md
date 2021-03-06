# SFND 2D Feature Tracking

<img src="images/keypoints.png" width="820" height="248" />

The idea of the camera course is to build a collision detection system - that's the overall goal for the Final Project. As a preparation for this, you will now build the feature tracking part and test various detector / descriptor combinations to see which ones perform best. This mid-term project consists of four parts:

* First, you will focus on loading images, setting up data structures and putting everything into a ring buffer to optimize memory load. 
* Then, you will integrate several keypoint detectors such as HARRIS, FAST, BRISK and SIFT and compare them with regard to number of keypoints and speed. 
* In the next part, you will then focus on descriptor extraction and matching using brute force and also the FLANN approach we discussed in the previous lesson. 
* In the last part, once the code framework is complete, you will test the various algorithms in different combinations and compare them with regard to some performance measures. 

See the classroom instruction and code comments for more details on each of these parts. Once you are finished with this project, the keypoint matching part will be set up and you can proceed to the next lesson, where the focus is on integrating Lidar points and on object detection using deep-learning. 

## Dependencies for Running Locally
* cmake >= 2.8
  * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1 (Linux, Mac), 3.81 (Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* OpenCV >= 4.1
  * This must be compiled from source using the `-D OPENCV_ENABLE_NONFREE=ON` cmake flag for testing the SIFT and SURF detectors.
  * The OpenCV 4.1.0 source code can be found [here](https://github.com/opencv/opencv/tree/4.1.0)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools](https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory in the top level directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./2D_feature_tracking`.

## Task MP0, Writeup

### MP.1 Data Buffer Optimization

Implement a vector for dataBuffer objects whose size does not exceed 2 to make a memory optimization. make a dataBuffer using `deque` by pushing in new elements on one end and removing elements on the other end.

### MP.2 Keypoint Detection

Implement differrent Features detectors HARRIS, FAST, BRISK, ORB, AKAZE, and SIFT using OpenCV and make them selectable by setting a string accordingly.

### MP.3 Keypoint Removal

Remove all keypoints outside of a pre-defined rectangle and only use the keypoints within the rectangle for further processing.

`if(!vehicleRect.contains(kaypoint.pt))`
`    remove keypoint`

### MP.4 Keypoint Descriptors

Implement descriptors BRIEF, ORB, FREAK, AKAZE and SIFT and make them selectable by setting a string accordingly.

### MP.5 Descriptor Matching

Implement FLANN matching as well as k-nearest neighbor selection.The function `matchDescriptors` in `matching2D_Student.cpp` contains the implementation for both methofs using the respective strings in the main function.

### MP.6 Descriptor Distance Ratio

Use the K-Nearest-Neighbor matching to implement the descriptor distance ratio test, which looks at the ratio of best vs. second-best match to decide whether to keep an associated pair of keypoints.
This distance ratio filter compares the distance (SSD) between two candidate matched keypoint descriptors. A threshold of `0.8` is applied and the stronger candidate (minimum distance) is selected as the correct match

### MP.7 Performance Evaluation 1

the number of keypoints on the preceding vehicle for all 10 images with all detectors and take note of the distribution of their neighborhood size. you can find it at `Task MP7.csv`

### MP.8 Performance Evaluation 2

 the number of matched keypoints for all 10 images using all possible combinations of detectors and descriptors. BF approach is used with the descriptor distance ratio set to 0.8. you can find it at `Taask MP8&MP9.csv`

### MP.9 Performance Evaluation 3

For overall performance relevant to this project, the top three combinations were:

FAST detectors and ORB descriptors
FAST detectors and BRIEF descriptors
FAST detectors and SIFT descriptors
