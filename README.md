# Yolov5 for Smoke Detection
Smoke detection task aims to identify fire or flame in a video and put a bounding box around it. This repo includes a demo on how to build a smoke detection detector using YOLOv5. 

#### Install
Clone this repo and use the following script to install [YOLOv5](https://github.com/ultralytics/yolov5). 
```
# Clone
git clone https://github.com/eyalofekDB/TrainYolo5SmokeDetector
cd Yolov5-Fire-Detection

# Install yolov5
git clone https://github.com/ultralytics/yolov5  
cd yolov5
pip install -r requirements.txt
```


#### Training
```
python train.py --img 640 --batch 16 --epochs 10 --data ../fire_config.yaml --weights yolov5s.pt --workers 0
```
#### Prediction
If you train your own model, use the following command for detection:
```
python detect.py --source ../input.mp4 --weights runs/train/exp/weights/best.pt --conf 0.2
```
Or you can use the pretrained model located in ```models``` folder for detection as follows:
```
python detect.py --source ../input.mp4 --weights ../models/best.pt --conf 0.2
```

#### Prediction Results
The training dataset contains only a few hundreds of negative samples. We may fix such problem and further improve the performance of the model by adding images with non-labeled smoke objects as negative samples. The [authors](https://github.com/ultralytics/yolov5/wiki/Tips-for-Best-Training-Results) who created YOLOv5 recommend using about 0-10% background images to help reduce false positives. 

#### Feature Visualization
It is desirable for AI engineers to know what happens under the hood of object detection models. Visualizing features in deep learning models can help us a little bit understand how they make predictions. In YOLOv5, we can visualize features using ```--visualize``` argument as follows:

```
python detect.py --weights runs/train/exp/weights/best.pt --img 640 --conf 0.2 --source ../datasets/Smoke/valid/images/0.jpg --visualize
```

## Reference
I borrowed and modified [YOLOv5-Custom-Training.ipynb](https://github.com/ultralytics/yolov5/wiki/Train-Custom-Data) script for training YOLOv5 model on the fire dataset. For more information on training YOLOv5, please refer to its homepage.
* https://github.com/robmarkcole/fire-detection-from-images
* https://github.com/ultralytics/yolov5
* https://github.com/AlexeyAB/darknet
