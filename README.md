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




