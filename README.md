# People-smoking-in-restricted-places
Smoking cigarettes affects the respiratory system, the circulatory system, the reproductive system, the skin, and the eyes, and it increases the risk of many different cancers.Even non-smokers who live in area of smoker have a 20% to 30% increased risk for developing lung cancer.So I developed a system to safeguard non-smokers to some extent by identifying people who smoke in restricted places such as schools,hospitals etc and inform to coressponding officials.
### Step1 ###
Clone the darknet repository https://github.com/pjreddie/darknet and follow the steps as mentioned below. \
Create darknet environment which works with GPU.\
You can follow detailed instructions at https://pjreddie.com/darknet/install/#cuda. But its so tedious.\
Instead you can use cloud GPU(Paperspace) or Google colab which comes with default darknet environment.
### Step 2 ###
Create your own cfg file(yolov3-tiny1) based on current objects(In our case Smoking and No_Smoking_Area).\
You have to edit yolov3-tiny.cfg.Change the number of filters to 21(classes+5)*3.\
Number of classes to 2.You should change these two in two yolo layers.
### Step 3 ###
Create file obj.names in directory(darknet/data/)  with objects names - each in new line(labels)\
Create file obj.data  containing (where classes = number of objects):\
classes= 2 \
train  = data\train.txt \
valid  = data\test.txt \
names = data\obj.names \
backup = data\ 
### Step 4 ###
Put image-files(collected around 50 images of both classes) of your objects in the directory darknet\data\obj\ \
You should label each object on images from your dataset. Use this visual GUI-software for marking bounded boxes of objects and generating annotation files for Yolo v2 & v3: https://github.com/AlexeyAB/Yolo_mark \
It generates .txt file for every image.
### Step 5 ###
Download pre-trained weights.
Download default weights file for yolov3-tiny: https://pjreddie.com/media/files/yolov3-tiny.weights \
Get pre-trained weights yolov3-tiny.conv.15 using command: \
./darknet partial cfg/yolov3-tiny.cfg yolov3-tiny.weights yolov3-tiny.conv.15 15.
### Step 6 ###
Start training:   /.darknet detector train data/obj.data yolov3-tiny1.cfg yolov3-tiny.conv.15 \
You should stop training when the average loss is less than 1.I trained it for around 10,000 steps to get an average loss of 0.673.
The new weights of trained model get stored in data folder as mentioned above.
### Step 7 ###
Once the model is trained you can test with custom objects.I have taken weights after 40000 iterations from data folder.\
./darknet detector test data/obj.data yolov3-tiny1.cfg yolo-tiny1_40000.weights.All commands are based on Linux.
![GitHub Logo](/predictions/1.jpg)
