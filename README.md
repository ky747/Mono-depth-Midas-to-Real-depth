# Mono-depth-Midas-to-Real-depth
convert relative depth to real depth with Midas and Yolo
Midas mono depth estimation deep learning model output only relative depth. because, stereo camera as we can see at our eyes these are usesing different parallax.

but if we use this camera to read depthmap, occour some problems like sync each camera and hardware prise rising etc..

so if we want to get depth estimation image by only one camera, we have to use deep learning model. 

Intet develped MiDaS(depthestimation model) which is can estimate depth with only one 2D image. but this model use only 1 2D image so that can not estimate real depth.

So I made a progream realtime depth estimateing progream by object detected. 
Not relying on the other sensor only camera. bottom right box on Yolo object detection screen, that contain real depth and compare other object’s depth everage with midas. 

bottom right box contain average depth(realdepth) with Midas, other object has relative depth but that can be chaged by avareage of depth detected. 

## Code
