# Social-Distance-Detection-using-OpenCV

With no doubt, the COVID-19 pandemic has put the world to a halt. The world we lived in a few months prior is completely different than what it is now. The virus is spreading quickly and is a danger to the human race. Seeing the necessity of the hour one must always take certain precautions of which one being social distancing. Maintaining social distancing during COVID-19 is a must to ensure a slowdown in the growth rate of new cases. Our manuscript focuses on detecting if the people around are maintaining social distancing or not. Using our own self developed model named SocialdistancingNet-19 for detecting the frame of a person and displaying labels, they are marked as safe or unsafe if the distance is less than a certain value. This system can be used for monitoring people via video surveillance in CCTV. 
<br />
<br />




## Set Up

Use the requirements.txt file to install the needed packages.
```
pip install -r requirements.txt
```

## Execute

Use the following command to execute the code.
```
python social_distance_detection.py --prototxt SSD_MobileNet_prototxt.txt --model SSD_MobileNet.caffemodel --labels class_labels.txt
```

## Model

The MobileNet SSD model can detect 20 objects. The objects that can be detected can be found in the [class_labels.txt](class_labels.txt) file.
Pre-trained model from Deep Learning frameworks like Caffe, Tensorflow, Torch and Darknet can also be loaded.


## Method
SSD is designed for object detection in real-time. Faster R-CNN uses a region proposal network to create boundary boxes and utilizes those boxes to classify objects. While it is considered the start-of-the-art in accuracy, the whole process runs at 7 frames per second. Far below what a real-time processing needs. SSD speeds up the process by eliminating the need of the region proposal network. To recover the drop in accuracy, SSD applies a few improvements including multi-scale features and default boxes. These improvements allow SSD to match the Faster R-CNN’s accuracy using lower resolution images, which further pushes the speed higher. 

Single Shot object Detection (SSD) using MobileNet and OpenCV were used to detect people. A bounding box is displayed around every person detected. 

To detect the distance of people from camera, triangle similarity technique was used. Let us assume that a person is at a distance D (in centimetres) from camera and the person's actual height is H (I have assumed that the average height of humans in 165 centimetres). Using the object detection code above, we can identify the pixcel height P of the person using the bounding box coordinates. Using these values, the focal length of the camera can be calculated using the below formula:

```
Eq 1: F = (P x D) / H
```
After calculating the focal length of the camera, we can use the actual height H of the person, pixcel height P of the person and focal length of camera F to calculate the distance of the person from camera. Distance from camera can be calculated using:

```
Eq 2: D' = (H x F) / P
```
Now that we know the depth of the person from camera, we can move on to calculate the distance between two people in a video. There can be n number of people detected in a video. So the Euclidean distance is calculated between the mid-point of the bounding boxes of all the people detected. By doing this, we have got our x and y values. These pixcel values are converted into centimetres using Eq 2.

We have the x, y and z (distance of the person from camera) coordinates for every person in cms. The Euclidean distance between every person detected is calculated using the (x, y, z) cordinates. If the distance between two people is less than 2 metres or 200 centimetres, a red bounding box is displayed around them indicating that they are not maintaining social distance. The object's distance from camera was converted to feet for visualization purpose. 

## Improvements

* Various object detection models like YOLO, Faster R-CNN can be used to improve the performance and accuracy of object detection.
* Video can be calibrated to get bird's eye view for more accurate distance estimation between objects.


