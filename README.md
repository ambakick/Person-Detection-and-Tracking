# Person-Detection-and-Tracking

## Introduction
The Project is based on Person Detection and tracking and I am mainly focusing on the Person tracking, if you go through the output gif in the README.md or watch output.mp4 you will be able to see that each person will be provided with an idea as soon as he enters a frame and the number remains with his regardless of the detection happening in concurrent frames. So basically the project focuses on Person Detection and track him as long as he remains in the frame.

## For executing
### Run Person_det_track.py
Person_det_track.py detects and tracks the person using SSD and Kalman Filter

## Requirements
Please try to Stick on with the version provided as much as possible other-wise you will face compatibility issues. I have used the best combination possible during the time of coding.
* **opencv [v3.1]**
	* **Installation in linux:**
			For complete installation of opencv in ubuntu you can refer [here](http://www.pyimagesearch.com/2015/06/22/install-opencv-3-0-and-python-2-7-on-ubuntu/).
	* **Installation in windows**
			For complete installation of opencv in windows you can refer [here](https://putuyuwono.wordpress.com/2015/04/23/building-and-installing-opencv-3-0-on-windows-7-64-bit/)
      
* **Tensorflow [v1.5.0]** 
	* **Installation**
		Tensorflow has an amazing documentation [here](https://www.tensorflow.org/install/pip)
## Methodology / Approach
The method Proposed here is divided into 2 main parts

* Person Detection - The person detection in Real-time is done with the help of Single Shot MultiBox Detector. SSD achieves 75.1%
	mAP, outperforming a comparable state of the art Faster R-CNN model. and the SSD model is available in the Tensorflow detection
	zoo. The seamless integration of SSD with tensorflow helps in further optimization and implementation of the algorithm.
	The SSD object detection composes of 2 parts:
	* Extract feature maps, and 
	* Apply convolution filters to detect objects.
	Even though SSD is capable of detecting multiple objects in the frame, in this project I limited its detection to just human.

* Person Tracking - Bounding box can be achieved around the object/person by running the Object Detection model in every frame, but this is computationally expensive.
	The tracking algorithm used here is Kalman Filtering . The Kalman Filter has long been regarded as the optimal solution to many tracking and data prediction tasks. Its use in the analysis of visual motion. The purpose of Filtering is to extract the required information from a signal, ignoring everything else. In this project the Kalman Filter is fed with the velocity, position and direction of the person which helps it to predict the future location of the Person based on his previous data.

The tracking part still faces some problem at the time of an occlusion. (Working on it)

## Performance of Code
* The code was run on both CPU and GPU:	
	* Nvidia Quadro 4000  -  ~30FPS
	* Nvidia Jetson TX2   -  ~20FPS
	* Intel i5 CPU	      -  ~10FPS
## Output
![Alt Text](https://github.com/ambakick/Person-Detection-and-Tracking/blob/master/person%20detection%20and%20track.gif)

## Overview / Usage
The system consist of two parts first human detection and secondly tracking. Early research is biased to human recognition rather than tracking. Monitoring the movements of human being raised the need for tracking. Monitoring movements are of high interest in determining the activities of a person and knowing the attention of person. This project focuses on Person Detection and tracking.

Identity retrieval - Tracking of human being can be used as a prior step in biometric face recognition. Keeping continuous track
of person will allow to identify person at any time. Thus even if his face identification is not possible at a particular set of frames
his identity can be found out. This can be very useful in the case of anomaly detection as the person's face may not face to the
camera when an anomaly is detected. So with the help of tracking his identity can be revealed.

Reducing the computation power requirement - A normal objection detection algorithm just detects the Person but do not
assign an Id for an Person thus has to be run in every frame to get the bounding box. Tracking will help to reduce the number of
times the Detection algorithm has to be run i.e instead of running the Detection algorithm every frame we can run it once in
every 5 frames.

Object Detection model failure compensation - there might be some poses where SSD may not detect the person. Even occlusion can affect the detector to a significant level that is where tracking algorithm can be of great help to us.

By Neeraj Menon
