# yolov2 for custom object detection

This repo consists of steps needed for installing YOLOV2 on linux/windows and training for custom object detection.

## Installing YoloV2 and training Custom images for object detection
The procedure for executing darknet in linux and windows is almost identical except the installation.

First I will provide the guidance for installation of darknet in both OS and then I will dive into execution part.

This repo supports darknet for:

    •	both Windows and Linux

    •	both OpenCV 3.x and OpenCV 2.4.13

    •	both cuDNN 5 and cuDNN 6

    •	CUDA >= 7.5

    •	also create SO-library on Linux and DLL-library on Windows

Installation of darknet in LINUX (GPU version):

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
    o	git clone https://github.com/AlexeyAB/darknet.git
    o	#this will get the darknet data into linux
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

o	Now the darknet is ready for training custom images.


Installation of darknet in Windows (GPU and No-GPU version):
                                        
    o	To download darknet first install gitbash which is found here  https://git-scm.com/download/win 
    o	Open gitbash and type git clone https://github.com/AlexeyAB/darknet.git. 
    
    This should download the darknet and save it in C:\Users\mohanaditya\ (the name should be your system name). 
    
 ![alt text](https://github.com/aditya-karampudi/yolov2-detection/blob/master/image/Captureas.JPG?raw=true)
    
    
 Make sure you have the following dependencies installed (skip CUDA and Cudnn if you don’t have GPU):
 
   Windows MS Visual Studio 2015 (v140): https://go.microsoft.com/fwlink/?LinkId=532606&clcid=0x409

   CUDA 8.0: https://developer.nvidia.com/cuda-downloads

   Install either of the opencv:
        
        o	OpenCV 3.x: https://sourceforge.net/projects/opencvlibrary/files/opencv-win/3.2.0/opencv-3.2.0-vc14.exe/download

        o	OpenCV 2.4.13: https://sourceforge.net/projects/opencvlibrary/files/opencv-win/2.4.13/opencv-2.4.13.2-vc14.exe/download

Unzip them and change the folder name to opencv_3.0 (for 3.x version) and name as opencv_2.4 (for 2.x version) Copy the folder and paste it in C:\ for visual studio to get these while building darknet.



 ![alt text](https://github.com/aditya-karampudi/yolov2-detection/blob/master/image/Capture3.JPG?raw=true)
 
    GPU CC >= 3.0 if you use cuDNN + CUDA:
        o	Download cudnn by registering in nvidia: https://developer.nvidia.com/rdp/cudnn-download
        o	Instructions to install cudnn: http://docs.nvidia.com/deeplearning/sdk/cudnn-install/index.html
        
Now let’s build darknet for Non-GPU:
	Go to C:\Users\mohanaditya\darknet\build\darknet (replace with your path), double-click on darknet_no_gpu.sln This should open Microsoft visual studio and in menu bar set x64 and Release and then select Build in menu bar and click Build darknet.

	We have to copy few files in new paths so that darknet will pick them while executing: 

	Copy the file opencv_world320.dll and opencv_ffmpeg320_64.dll which are present in C:\opencv_3.0\opencv\build\x64\vc14\bin and paste them in C:\Users\mohanaditya\darknet\build\darknet\x64\ (replace with your path). Basically the two open_cv files should be present in the folder where darknet.exe is present.

