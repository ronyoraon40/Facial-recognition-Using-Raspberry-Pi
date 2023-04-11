# Facial-recognition-Using-Raspberry-Pi
Detecting user face from pi camera and raspberry pi using OpenCV image processing algorithm.

#Enable Pi Camera and VNC

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

# Install Hierarchical Data Format (HDF5) This package is used by OpenCV to manage data and development of QT GUIs.

  	sudo apt install libhdf5-dev libhdf5-103
  
# Install Python and numpy using the following command
  
  	sudo apt install python3-dev python3-pip python3-numpy
  
# Now we will now need to temporarily increase the size of the swap space to help the process of compiling OpenCV on the Raspberry Pi.

	sudo nano /etc/dphys-swapfile
	
	Replace this file: **CONF_SWAPSIZE=100** 'with' CONF_SWAPSIZE=2048        #Press: Ctrl X, Y, and <enter>
