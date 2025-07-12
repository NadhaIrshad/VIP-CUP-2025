# VIP-CUP-2025

## Task Description
This project addresses the 2025 IEEE VIP Cup Challenge: Infrared-Visual fusion for Enhanced Drone Detection, Tracking, and Payload Identification in Surveillance Videos. The goal is to detect and track drones in challenging real-world scenarios using both IR and RGB video data, distinguishing drones from birds and background clutter, and to determine whether each drone is approaching or receding from the camera’s field of view. The system must operate in real time and provide reliable tracking and direction analysis under adverse environmental conditions.

### Method Overview
Detection:
We use a YOLOv8-based object detector trained on the provided IR datasets to identify drones and birds in each video frame.
<img width="1712" height="711" alt="image" src="https://github.com/user-attachments/assets/b0c5aa74-6804-4480-a218-770785034173" />


Drone-Only Tracking:
Only detections classified as "drone" are passed to the DeepSORT multi-object tracker, ensuring that only drones are assigned unique IDs and tracked across frames.

Directional Analysis:
For each tracked drone, we analyze the change in bounding box area over time to determine if the drone is approaching or receding from the camera. Optionally, Lucas-Kanade optical flow can be used for more robust direction estimation.
<img width="958" height="425" alt="image" src="https://github.com/user-attachments/assets/a9675d08-f090-40df-9783-c3a6b18c25b5" />
<img width="960" height="424" alt="image" src="https://github.com/user-attachments/assets/99ab34ca-9142-4d37-b18c-57c65ffe49f1" />


Visualization:
The system overlays bounding boxes, unique track IDs, detection confidence, and real-time direction (“Approaching” or “Receding”) on the output video.

Metrics:
The code computes and reports tracking metrics required by the VIP Cup, including average IoU, tracking consistency, direction accuracy, and average FPS.

### Summary:
This solution combines robust deep learning-based detection with real-time tracking and direction analysis, tailored for drone surveillance in complex environments.

### How deepsort works?

<img width="850" height="339" alt="image" src="https://github.com/user-attachments/assets/a0061687-96eb-4b56-a055-418f802736e1" />
image ref: https://www.researchgate.net/figure/Architecture-of-Deep-SORT-Simple-online-and-real-time-tracking-with-deep-association_fig2_353256407 

DeepSORT (Deep Learning-based SORT) is an extension of the popular object tracking algorithm called SORT (Simple Online and Realtime Tracking). DeepSORT adds deep appearance feature extraction and a matching process to the original SORT algorithm to improve its tracking accuracy and robustness.
The architecture of DeepSORT can be broken down into the following steps:
1.	Detection: Use an object detection algorithm (such as YOLO) to detect objects in each frame of a video.
2.	Feature extraction: Extract a deep appearance feature vector for each detected object using a CNN-based feature extractor (such as ResNet).
3.	Data association: Associate the detected objects across frames using a matching algorithm (such as the Hungarian algorithm) that takes into account both the location and appearance of the objects.
4.	Track management: Manage the tracks by updating the state of each track (i.e., position and velocity) based on the associated objects and their appearance features.
5.	Track pruning: Remove tracks that have not been associated with any objects for a certain number of frames or that have low confidence scores.
The deep appearance features used in DeepSORT are learned during training from a large dataset of object images. By incorporating appearance features in addition to the location and motion information used by the original SORT algorithm, DeepSORT is able to handle situations where objects may temporarily disappear or occlude each other, leading to more accurate and robust object tracking.



### References
https://github.com/Utkal97/Object-Tracking/tree/main

https://learnopencv.com/understanding-multiple-object-tracking-using-deepsort/#Introduction-to-DeepSORT

https://arxiv.org/pdf/2207.12202v1 
