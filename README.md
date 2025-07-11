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

___
## Code
*detail of code refer to comment I'll note here about cautions*

```py
# set base depth (input real depth in bottom right yello box)
REF_REAL_M = 15.0
```
you can set this num and reversion if you want

```py
 with torch.no_grad():
        fps = 1
        video = VideoStream(0).start()
        time_start = time.time()
        ...
```
This code using a usb camera for video input, `VideoStream(0)` you can select cam by list of connected camera.

If you want to change model here
```py
    yolo_model = YOLO("yolo11n.pt")
```
Yolo
```py
def run(input_path, output_path, model_path, model_type="dpt_levit_224", optimize=False, height=None):
    print("Initialize")
```
```py
    parser.add_argument('-t', '--model_type', default='dpt_levit_224')
```
Midas
```py
 if optimize and device == torch.device("cuda"):
```
```py
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
```
If you don't want using CUDA(enhance processing with GPU), changing `cuda` to `cpu`

## Example
![dpt_levit_224](C:\Project\MiDas\MiDaS-master\MiDaS-master\Mono-depth-Midas-to-Real-depth\Midas v3.1 dpt_levit_224.png)
![dpt_Swin2_L 384](C:\Project\MiDas\MiDaS-master\MiDaS-master\Mono-depth-Midas-to-Real-depth\Midas v3.1 Swin2-L 384.png)


So I made a progream realtime depth estimateing progream by object detected. 
Not relying on the other sensor only camera. bottom right box on Yolo object detection screen, that contain real depth and compare other object’s depth everage with midas. 

bottom right box contain average depth(realdepth) with Midas, other object has relative depth but that can be chaged by avareage of depth detected. 