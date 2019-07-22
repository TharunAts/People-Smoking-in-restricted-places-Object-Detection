# People-smoking-in-restricted-places
Detecting People who smoke in restricted places(Non-Smoking Areas) and inform to corresponding officials.
### Step1 ###
Initially create darknet environment with GPU and OpenCV installed.\
You can follow detailed instructions at https://pjreddie.com/darknet/install/#cuda. But its so tedious.\
Instead you can use cloud GPU(Paperspace) which comes with default darknet environment.
### Step 2 ###
Create your own cfg file(yolov3-tiny1) based on current objects(In our case Smoking and No_Smoking_Area).\
You have to edit yolov3-tiny.cfg.Change the number of filters to 21(classes+5)*3.\
Number of classes to 2.U should change these two in 2 places at the yolo layer.
### Step 3 ###
Create file obj.names in directory(darknet/data/)  with objects names - each in new line(labels)\
Create file obj.data  containing (where classes = number of objects):\
classes= 2 \
train  = data\train.txt \
valid  = data\test.txt \
names = data\obj.names \
data = data\ 
### Step 4 ###
Put image-files (.jpg) of your objects in the directory darknet\data\obj\ \
You should label each object on images from your dataset. Use this visual GUI-software for marking bounded boxes of objects and generating annotation files for Yolo v2 & v3: https://github.com/AlexeyAB/Yolo_mark \
It generates .txt file for every image.
### Step 5 ###
Download pre-trained weights.
Download default weights file for yolov3-tiny: https://pjreddie.com/media/files/yolov3-tiny.weights \
Get pre-trained weights yolov3-tiny.conv.15 using command: darknet.exe partial cfg/yolov3-tiny.cfg yolov3-tiny.weights yolov3-tiny.conv.15 15.
### Step 6 ###
Start training: /.darknet detector train data/obj.data yolov3-tiny1.cfg yolov3-tiny.conv.15
You should stop training when the average loss is less than 1.I trained it for around 10,000 steps to get an average loss of 0.673
### Step 7 ###
Once the model is trained you can test with custom objects.
./darknet detector test data/obj.data yolov3-tiny1.cfg yolo-tiny1_40000.weights
