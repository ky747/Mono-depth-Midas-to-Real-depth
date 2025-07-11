# Mono-depth-Midas-to-Real-depth
This repository contains code to convert relative depth map to real depth map with [MiDaS](https://github.com/isl-org/MiDaS) and [YOLO](https://github.com/ultralytics/ultralytics)
___
## Feature of MiDaS
MiDaS deep learning model compute depth form a single image. But this model output only relative depth. because, stereo camera usesing different parallax like our eyes, but MiDaS only using single image.

So it can create **relative depth** map.

But I make this repository to overcome limits *(generate real depth)*
___
## Convert program pipline

1. get video from cv2
2. input YOLO & MiDaS
3. make bounding box & depth map form cam frame
4. compare average depth in **standard box**  with average depth in object detected **bounding box**
5. calcuate real depth(standard box real depth entered)



So I made a progream realtime depth estimateing progream by object detected. 
Not relying on the other sensor only camera. bottom right box on Yolo object detection screen, that contain real depth and compare other object’s depth everage with midas. 

bottom right box contain average depth(realdepth) with Midas, other object has relative depth but that can be chaged by avareage of depth detected. 

## Code
