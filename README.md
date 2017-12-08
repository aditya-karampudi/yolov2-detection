# Yolov2 for custom object detection

This repo consists installation guidance for YOLOV2 on linux/windows and training for custom object detection.

The procedure for executing darknet in linux and windows is almost identical except the installation.

First I will provide the guidance for installation of darknet in both OS and then I will dive into execution part.

This repo supports darknet for:

    •	both Windows and Linux

    •	both OpenCV 3.x and OpenCV 2.4.13

    •	both cuDNN 5 and cuDNN 6

    •	CUDA >= 7.5

    •	also create SO-library on Linux and DLL-library on Windows

## Installation of darknet in LINUX (GPU version):

    •	Open new linux terminal in aws or google cloud which should have the following packages installed.

Note: Choose aws AMI:Deep Learning Base AMI (Ubuntu) Version 1.0 - ami-a1e534d9 which has built in packages..

o  CUDA 8.0: https://developer.nvidia.com/cuda-downloads


      o Instructions to install CUDA: http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html


o	Install either of the opencv:


      o	OpenCV 3.x: https://www.pyimagesearch.com/2016/10/24/ubuntu-16-04-how-to-install-opencv/


      o	OpenCV 2.4.13: find the attachment opencv2.4_instructions.txt to install in linux.

 
o	GPU CC >= 3.0 if you use cuDNN + CUDA: 

    o	Download cudnn by registering in nvidia: https://developer.nvidia.com/rdp/cudnn-download

    o	Instructions to install cudnn: http://docs.nvidia.com/deeplearning/sdk/cudnn-install/index.html


•	Once the installation is done open linux and type the following commands:

    o	sudo apt-get update
    o	sudo apt-get dist-upgrade
    o	git clone https://github.com/AlexeyAB/darknet.git  #this will get the darknet data into linux
    o	Now we have the data in linux it is time to execute Makefile which will install necessary dependencies in linux
    o	Go to darknet folder by cd ./darknet and type ‘vi Makefile’
    o	In the file change the first six lines to:
              o	GPU=1
              o	CUDNN=1
              o	OPENCV=1
              o	DEBUG=0
              o	OPENMP=1
              o	LIBSO=0
    Save it by pressing ESC and then :wq! and press ENTER
    o	Type ‘make’ in the directory where Makefile is present. It should compile all the computations and should show build successful. If it doesn’t happen then search the errors in web.

*Now the darknet is ready for training custom images.*


## Installation of darknet in Windows (GPU and No-GPU version):
                                        
    o	To download darknet first install gitbash which is found here  https://git-scm.com/download/win 
    o	Open gitbash and type git clone https://github.com/AlexeyAB/darknet.git. 
    
    This should download the darknet and save it in C:\Users\mohanaditya\ (the name should be your system name). 
    
 ![alt text](https://github.com/aditya-karampudi/yolov2-detection/blob/master/image/Captureas.JPG?raw=true)
    
    
 Make sure you have the following dependencies installed (skip CUDA and Cudnn if you don’t have GPU):
 
 o  Windows MS Visual Studio 2015 (v140): https://go.microsoft.com/fwlink/?LinkId=532606&clcid=0x409

 o  CUDA 8.0: https://developer.nvidia.com/cuda-downloads

 o  Install either of the opencv:
        
        o	OpenCV 3.x: https://sourceforge.net/projects/opencvlibrary/files/opencv-win/3.2.0/opencv-3.2.0-vc14.exe/download

        o	OpenCV 2.4.13: https://sourceforge.net/projects/opencvlibrary/files/opencv-win/2.4.13/opencv-2.4.13.2-vc14.exe/download

Unzip them and change the folder name to opencv_3.0 (for 3.x version) and name as opencv_2.4 (for 2.x version) Copy the folder and paste it in C:\ for visual studio to get these while building darknet.



 ![alt text](https://github.com/aditya-karampudi/yolov2-detection/blob/master/image/Capture3.JPG?raw=true)
 
 o  GPU CC >= 3.0 if you use cuDNN + CUDA:
    
        o	Download cudnn by registering in nvidia: https://developer.nvidia.com/rdp/cudnn-download
        o	Instructions to install cudnn: http://docs.nvidia.com/deeplearning/sdk/cudnn-install/index.html

### Now let’s build darknet for Non-GPU:

    	Go to C:\Users\mohanaditya\darknet\build\darknet (replace with your path), double-click on darknet_no_gpu.sln This should open Microsoft visual studio and in menu bar set x64 and Release and then select Build in menu bar and click Build darknet.

    	We have to copy few files in new paths so that darknet will pick them while executing: 

    	Copy the file opencv_world320.dll and opencv_ffmpeg320_64.dll which are present in C:\opencv_3.0\opencv\build\x64\vc14\bin and paste them in C:\Users\mohanaditya\darknet\build\darknet\x64\ (replace with your path). Basically the two open_cv files should be present in the folder where darknet.exe is present.

## Darknet for GPU:

If you have CUDA 8.0 and OpenCV3.0 then follow the steps:
           
    	Go to C:\Users\mohanaditya\darknet\build\darknet (replace with your path), double-click on darknet.sln This should open Microsoft visual studio and in menu bar set x64 and Release and then select Build in menu bar and click Build darknet.

    	We have to copy few files in new paths so that darknet will pick them while executing: 
    
    	Copy the file opencv_world320.dll and opencv_ffmpeg320_64.dll which are present in C:\opencv_3.0\opencv\build\x64\vc14\bin and paste them in C:\Users\mohanaditya\darknet\build\darknet\x64\ (replace with your path). Basically the two open_cv files should be present in the folder where darknet.exe is present.
    
    	If you want to build with CUDNN to speed up then:
        o	download and install cuDNN 6.0 for CUDA 8.0: https://developer.nvidia.com/cudnn
        o	add Windows system variable cudnn with path to CUDNN: https://hsto.org/files/a49/3dc/fc4/a493dcfc4bd34a1295fd15e0e2e01f26.jpg
        o	open \darknet.sln -> (right click on project) -> properties -> C/C++ -> Preprocessor -> Preprocessor Definitions, and add at the beginning of line: CUDNN;


If you have other version of CUDA (not 8.0) and openCV2.4 then

    	Open C:\Users\mohanaditya\darknet\build\darknet\darknet.vcxproj (replace with your path) by using Notepad, find 2 places with "CUDA 8.0" and change it to your CUDA-version.d
    	If you have OpenCV 2.4.13 instead of 3.0 then you should change paths after \darknet.sln is opened in visual studio
        o	(right click on project) -> properties -> C/C++ -> General -> Additional Include Directories: C:\opencv_2.4\opencv\build\include
        o	(right click on project) -> properties -> Linker -> General -> Additional Library Directories: C:\opencv_2.4\opencv\build\x64\vc14\bin
    	If you want to build with CUDNN to speed up then:
        o	download and install cuDNN 6.0 for CUDA 7.0: https://developer.nvidia.com/cudnn
        o	add Windows system variable cudnn with path to CUDNN: https://hsto.org/files/a49/3dc/fc4/a493dcfc4bd34a1295fd15e0e2e01f26.jpg
        o	open \darknet.sln -> (right click on project) -> properties -> C/C++ -> Preprocessor -> Preprocessor Definitions, and add at the beginning of line: CUDNN;

## Training custom images in linux/windows
Now we have the darknet installed in windows and linux. It is time to train custom images:

    The Yolo needs three types of files:
        1.)	Images in the form of .jpg (if the images are in .png format open cmd in the folder and type ren *.png *.jpg)
        2.)	Object co-ordinates in the images in .txt format
        3.)	The train and test split file containing the names of images
 
Images: Yolo needs 2000 images of each class to train. One can also start with less images.

Co-ordinates: We have to create a text file which should contain the class of the image, the xmin, ymin, xmax, ymax co-ordinates.

    This repository consists BBox multi-label folder which does the labelling part.
        	Clon the repository into your system, go to BBox-Label/Images/001 and paste the images which you want to label
        	Open the file boundaries.ipynb in jupyter notebook (use python 2.7)
        	Execute the file and a new window comes up:
        	Type 001 in the top box and press Enter. For labelling information check here: https://github.com/jxgu1016/BBox-Label-Tool-Multi-Class
        	On the top right there are classes. Change the class.txt file in BBox-Label folder to change the classes. 
        	Change the class on top right of the labelTool dialogbox and click confirm class to label multi-classes.
        	Once the labelling is finished the text files are generated in BBox-Label/label/001 they should look in the format.
 

 ![alt text](https://github.com/aditya-karampudi/yolov2-detection/blob/master/image/Capture22.JPG?raw=true)
 
 ![alt text](https://github.com/aditya-karampudi/yolov2-detection/blob/master/image/Captur12e.JPG?raw=true)
 
     	But this is not the format that we need so open file convert.ipynb in jupyter notebook present in BBox-Label folder. Execute this code and it will create files in BBox-Label/label/converted_labels.
     	Copy the files present in converted_labels and paste them in BBox-Label/Images/001
     	Now to create train and test split text file. Open train _test_split.ipynb present in \Dodge\BBox-Label\BBox-Label\Images\001. Execute it two times and then train.txt and test.txt files are generated. Change the value in line 10 to whatever percentage split one needs. By default the split is 90:10     
     	Now we have data and we have to upload all the files present in \Dodge\BBox-Label\BBox-Label\Images\001 to linux under darknet/data/hd/ and for windows create folder hd in C:\Users\mohanaditaya\darknet\build\darknet\x64\data (replace my name with the system name (mohanaditya)) and paste all the files in hd folder.
     	The hd folder should have the images, text files consisting boundaries information, train data and test data file


•	Need to make three changes in few yolo files
•	Go to darknet/cfg:  
    
    o	Create new text file and copy the data present in yolo-voc.2.0.cfg to the new file and do the following changes in the new text file
        	In Line 3 set batch=64
        	In Line 4 set subdivisions=8
        	In line 244 set classes=1
        	In line 237 set filters = (classes + 5)*5
    Save the file as yolo-obj.cfg

    o	Create new text file and type the following:
        	Type the name of the objects you want to detect
    Save the file as obj.names
    
    o	Create new text file type the following:
        	classes= 0  #number of classes
        	train  = data/hd/train.txt #path for train data
        	valid  = data/hd/test.txt  #path for test data
        	names = obj.names # names for displaying
        	backup = backup/
    Save the file as obj.data
    
•	For training the darknet we need to give the following command in darknet folder
**./darknet detector train cfg/obj.data cfg/yolo-obj.cfg**

The weights are stored in **backup/** folder

•   If training stops in the middle one can start training with pre-trained weights present in backup folder by running:
**./darknet detector train cfg/obj.data cfg/yolo-obj.cfg backup/yolo-obj_2000.weights**


•	For testing an image after 1000 iterations:
**./darknet detector test cfg/obj.data cfg/yolo-obj.cfg backup/yolo-obj_10000.weights data/hd/nameofimage.jpg**

• To save the detected image:
**./darknet detector test cfg/obj.data cfg/yolo-obj.cfg backup/yolo-obj_10000.weights data/hd/nameofimage.jpg -a**

•To predict on test images 
**./darknet detector valid cfg/obj.data cfg/yolo-obj.cfg backup/yolo-obj_10000.weights**
The output will be stored in **results/** as **comp3_test.txt** file which contains the ***name of image, probability of its detection, xmin, ymin, xmax, ymax***



Please site darknet if you use in your project:
@article{redmon2016yolo9000,
  title={YOLO9000: Better, Faster, Stronger},
  author={Redmon, Joseph and Farhadi, Ali},
  journal={arXiv preprint arXiv:1612.08242},
  year={2016}
}

**References:**
https://timebutt.github.io/static/how-to-train-yolov2-to-detect-custom-objects/

https://github.com/AlexeyAB/darknet

https://github.com/jxgu1016/BBox-Label-Tool-Multi-Class








