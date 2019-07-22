# People-smoking-in-restricted-places
Detecting People who smoke in restricted places(Non-Smoking Areas) and inform to corresponding officials.
### Step1 ###
Initially create darknet environment with GPU and OpenCV installed.\
You can follow detailed instructions at https://pjreddie.com/darknet/install/#cuda. But its so tedious.\
Instead you can use cloud GPU(Paperspace) which comes with default darknet environment.\ 
## Step 2 ###
Create your own cfg file(yolov3-tiny1) based on current objects(In our case Smoking and No_Smoking_Area).\
You have to edit yolov3-tiny.cfg.Change the number of filters to 21(classes+5)*3.\
Nu

