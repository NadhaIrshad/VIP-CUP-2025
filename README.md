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


### References
https://github.com/Utkal97/Object-Tracking/tree/main

https://learnopencv.com/understanding-multiple-object-tracking-using-deepsort/#Introduction-to-DeepSORT

https://arxiv.org/pdf/2207.12202v1 
