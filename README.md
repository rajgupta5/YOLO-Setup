# YOLO-Setup on MAC

![YOLOv3](https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcSsQfpSLmDtzLmpLJBb4i-BtU4l99IuHmRmoA&usqp=CAU)

- Official Website: - https://pjreddie.com/darknet/yolo/

- Download files from (some file have been uploaded in this repo)
  [https://drive.google.com/file/d/1GXYiJ7z3Egx9XiMlPzNLkMLZOGtQFFJg/view]

- Create a Project directory say on Desktop named "YOLO"
  cd YOLO
  git clone https://github.com/pjreddie/darknet
  cd darknet
  make

- Detection Using A Pre-Trained Model
  ./darknet detect cfg/yolov3.cfg yolov3.weights data/dog.jpg


- **Start Training**
  - Create a folder called "training" in the darknet directory
  - Then we copy the files train.txt, test.txt, objects.names, yolov3-tiny.cfg, and trainer.data inside the "training" folder .
  - Move dataset to darknet folder
  - Move generate.py to darknet folder
  - Run command : python generate.py (2 files will be created - train and text.txt)
  - Copy train and test.txt to training folder


- We will be working with Tiny Yolo
  Tiny Yolo Config File:- https://github.com/pjreddie/darknet/blob/master/cfg/yolov3-tiny.cfg
 
  - Changes to be done in Yolo COnfig File
 
   1. Uncomment the lines 5,6, and 7 and change the training batch to 64 and subdivisions to 2.
 
   2. Change the number of filters for convolutional layer "[convolution]" just before every yolo output "[yolo]" such that the number of filters= 3 x (5 +    #ofclasses)= 3x(5+1)= 18. The number 5 is the count of parameters center_x, center_y, width, height, and objectness Score. So, change the lines 127 and 171 to "filters=18".
 
   3. For every yolo layer [yolo] change the number of classes to 1 as in lines 135 and 177.
 
- Files Needed inside training folder:-
 
  1. Create a file object.names
    Insert the class name
    Rubiks Cube
 
  2. trainer.data
     Contents:-
     1. Number of classes.
     2. Locations of train.txt and test.txt files relative to the darknet main directory.
     3. Location of objects.names file relative to the darknet main directory.
     4. Location of the backup folder for saving the weights of training process, it is also relative to the darknet main directory
 
     Looks like:-

     classes= 1  
     train  = training/train.txt  
     valid  = training/test.txt  
     names = training/objects.names  
     backup = backup/
 
   3. yolov3-tiny.cfg 
     It contains the training parameters as batch size, learning rate, etc., and also the architecture of the network as number of layer, filters, type of  activation function, etc.
 
- Weights File Download Link :- https://pjreddie.com/media/files/darknet53.conv.74
  Copy this file inside darknet folder

- Training Command :- ./darknet detector train training/trainer.data training/yolov3-tiny.cfg darknet53.conv.74
 
Notes :-
Weights will be saved in the backup folder every 100 iterations till 900 and then every 10000.
Kill the training process once the average loss is less than 0.06, or once the avg value no longer increases.
 

 
- Once training is done, Do the prediction/testing via live cam
  1. conda create --name yolo python=3.6.10
  2. conda activate yolo
  3. #install the opencv package
     - conda install -c conda-forge opencv
     or
     - pip install opencv-python
 
  4. cd to project_directory
 
  5. python yolo_opencv.py -c training/yolov3-tiny.cfg -w backup/yolov3-tiny_100.weights -cl training/objects.names
 
 
 

**YOLO Setup on Windows**
- https://github.com/alexeyab/darknet
- https://github.com/AlexeyAB/darknet#how-to-compile-on-windows-legacy-way
- Follow steps in Yolo Darknet Installation.docx inside this repo
