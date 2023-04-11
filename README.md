# Facial-recognition-Using-Raspberry-Pi

# Enable Pi Camera and VNC

sudo raspi-config

  Go to Interfaces->
  
	Enable PiCamera
	  
	Enable VNC
    
# Update and upgrade rapberry pi && Update the firmware

	sudo apt-get update && sudo apt-get upgrade && sudo rpi-update -> Press 'y' when prompted for rpi-update
  
# Install CMake developer tool for installing OpenCV

  	sudo apt install cmake build-essential pkg-config git

# Install image I/O packages that will add support for different image formats

  	sudo apt install libjpeg-dev libtiff-dev libjasper-dev libpng-dev libwebp-dev libopenexr-dev

# Install video I/O packages that will allow us to read various video file formats from disk as well as work directly with video streams

  	sudo apt install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev libxvidcore-dev libx264-dev libdc1394-22-dev libgstreamer-plugins-base1.0-dev libgstreamer1.0-dev

# Install GTK packages to display images on our computer and even develop GUI for our projects

  	sudo apt install libgtk-3-dev libqtgui4 libqtwebkit4 libqt4-test python3-pyqt5

# Install the following dependencies for carrying out matrix operations. 

  	sudo apt install libatlas-base-dev liblapacke-dev gfortran

# Install Hierarchical Data Format (HDF5) This package is used by OpenCV to manage data and development of QT GUIs

  	sudo apt install libhdf5-dev libhdf5-103
  
# Install Python and numpy using the following command
  
  	sudo apt install python3-dev python3-pip python3-numpy
 
# Now we will now need to temporarily increase the size of the swap space to help the process of compiling OpenCV on the Raspberry Pi

	sudo nano /etc/dphys-swapfile
	
	Find: CONF_SWAPSIZE=100    
	Replace 100 with 2048 and press: Ctrl X, Y, and <enter>
	
	Start the swap using the command: sudo systemctl restart dphys-swapfile

# Next, let’s go ahead and clone the two OpenCV repositories we need to our Raspberry Pi. Running these two commands will retrieve the latest available version of OpenCV from their git repository

	git clone https://github.com/opencv/opencv.git && 	git clone https://github.com/opencv/opencv_contrib.git
	
# Compile OpenCV into your Raspberry pi by creating and navigating to the following directory

	mkdir ~/opencv/build && cd ~/opencv/build
	
# Inside the directory, use cmake to prepare OpenCV for compilation on your Raspberry Pi
	
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
	
# Start compiling using the following command

	make -j4
	
Note: Compilation executes for 6-6.5 hrs for Pi3 and 4 hrs for Pi4

# Once compilation is successful, run the following command to install OpenCV

	sudo make install

# 
