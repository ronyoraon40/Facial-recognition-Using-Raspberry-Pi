# Set up Raspberry Pi for Operating in Headless Mode:
Download Advanced IP Scanner and VNC Viewer

Flash Raspbian OS buster for OpenCV. Do not flash 32bit or 64 bit OS image.

OS Link: 
	
	https://www.raspberrypi.com/software/
Flashing Link:
	
	https://medium.com/digital-software-architecture/raspberry-pi-headless-configuration-ac0a3a31d184
	
# Prepare Raspberry Pi

Enable Pi Camera and VNC

	sudo raspi-config

  Go to Interfaces->
  
	Enable PiCamera
	  
	Enable VNC
    
Update and upgrade rapberry pi && Update the firmware
	
	sudo apt-get update && sudo apt-get upgrade && sudo rpi-update 
				-> Press 'y' when prompted for rpi-update
# Install Dependencies for OpenCV

Install CMake developer tool for installing OpenCV

  	sudo apt install cmake build-essential pkg-config git

Install image I/O packages that will add support for different image formats

  	sudo apt install libjpeg-dev libtiff-dev libjasper-dev libpng-dev libwebp-dev libopenexr-dev

Install video I/O packages that will allow us to read various video file formats from disk as well as work directly with video streams

  	sudo apt install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev libxvidcore-dev libx264-dev libdc1394-22-dev libgstreamer-plugins-base1.0-dev libgstreamer1.0-dev

Install GTK packages to display images on our computer and even develop GUI for our projects

  	sudo apt install libgtk-3-dev libqtgui4 libqtwebkit4 libqt4-test python3-pyqt5

Install the following dependencies for carrying out matrix operations. 

  	sudo apt install libatlas-base-dev liblapacke-dev gfortran

Install Hierarchical Data Format (HDF5) This package is used by OpenCV to manage data and development of QT GUIs

  	sudo apt install libhdf5-dev libhdf5-103
  
Install Python and numpy using the following command
  
  	sudo apt install python3-dev python3-pip python3-numpy
 
Now we will now need to temporarily increase the size of the swap space to help the process of compiling OpenCV on the Raspberry Pi

	sudo nano /etc/dphys-swapfile
	
Find: CONF_SWAPSIZE=100    
Replace 100 with 2048 and press: Ctrl X, Y, and <enter>
	
Start the swap using the command: 
	
	sudo systemctl restart dphys-swapfile

Next, let’s go ahead and clone the two OpenCV repositories we need to our Raspberry Pi. Running these two commands will retrieve the latest available version of OpenCV from their git repository

	git clone https://github.com/opencv/opencv.git && 	git clone https://github.com/opencv/opencv_contrib.git
	
Compile OpenCV into your Raspberry pi by creating and navigating to the following directory

	mkdir ~/opencv/build && cd ~/opencv/build
	
Inside the directory, use cmake to prepare OpenCV for compilation on your Raspberry Pi
	
	cmake -D CMAKE_BUILD_TYPE=RELEASE \
	-D CMAKE_INSTALL_PREFIX=/usr/local \
	-D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \
	-D ENABLE_NEON=ON \
	-D ENABLE_VFPV3=ON \
	-D BUILD_TESTS=OFF \
	-D INSTALL_PYTHON_EXAMPLES=OFF \
	-D OPENCV_ENABLE_NONFREE=ON \
	-D CMAKE_SHARED_LINKER_FLAGS=-latomic \
	-D BUILD_EXAMPLES=OFF ..
	
	Press <enter>. This will prepare a report for the dependencies that are installed and also show the python2 and 3 directory.
	
Start compiling using the following command:

	make -j4
	
Note: Compilation executes for 6-6.5 hrs for Pi3 and 4 hrs for Pi4

Once compilation is successful, run the following command to install OpenCV.

	sudo make install
This command will copy all the required files into there needed locations automatically.

Now we also need to regenerate the operating systems library link cache. Use the following command:

	sudo ldconfig
The Raspberry Pi won’t be able to find our OpenCV installation if we don’t run the following command.

# Cleaning up after Compilation
Restore the raspberry pi's memory swap as we no longer need to have such a large swap file.Replace 2048 with 100.

	sudo nano /etc/dphys-swapfile
	
Find: CONF_SWAPSIZE=2048   
Replace 2048 with 100 and press: Ctrl X, Y, and <enter>
	
Start the swap using the command: 
	
	sudo systemctl restart dphys-swapfile
	
# Test Opencv

Launch into the Python terminal by running the command below:
	
	python
By importing the module, check if OpenCV loads on your Pi.
	
	import cv2
If opencv is imported, it will generate a new line. To retrieve OpenCV’s version, use the following command:
	
	cv2.__version__
	
# Install Face Recognition and its Required Dependencies:
	
	pip install imutils
	pip install dlib
	pip install pillow
	pip install face-recognition --no-cache-dir

# Steps for Code Execution

# Collecting Data
Create folder named **dataset**. Navigate inside **dataset** folder. Create a folder by your name, for e.g., Helen.
	
	![Face-Recognition-System-Directories](https://user-images.githubusercontent.com/130435486/231690978-23da0406-5d27-4422-9d9c-3d8701352d8c.png)


Now open **dataset.py** code if you are using webcam (or) open **dataset_pi** if you are using Pi Camera. Both the codes execution are exactly the same.

Inside the code, type your exact folder name which is present inside dataset folder. 

Run the code using Geany editor. Upon running, press **spacebar** to capture the image. Take atleast 8-10 images with different profile angles. Press **Ctrl + C** to stop the execution.

# Training Model
After the images are saved in the **dataset** directory, open and run **train.py** code. This will process and generate facial recording encodings based on the captured images.

# Recognize
Finally run **facial_req.py**. Executing this code will detect your face with a box surrounded aroud your face and your name will appear on top of the box. You can change the color of the box according to your choice. 

If anyone else's face is detected, status will display **UNKNOWN**

# Future Purpose

You can add multiple applications on this code. Some of the applications are mentioned below:

	Bank Security
	Anti-theft alarm
	Smart Home Access
	Access Control
	Automobile Security
	Immigration
	Education
	Retail
	Healthcare
	Fleet Management
