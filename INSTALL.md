#########################################################################################################
#
#                              HOW TO INSTALL YOLO WITH GPU ON LINUX
#                                        by Brian Duenas
# 
# Tested on Ubuntu 18.04
# Graphics card GTX 1060 mobile
# 
# I am not responsible for damages to your device use at your own risk. None of this software is mine
# I got them from all parts of the web and put them into one guide! 
# 
# Special thanks to sentex https://pythonprogramming.net/
# 
#########################################################################################################

# Follow these steps from "https://pjreddie.com/darknet/yolo/" and test if its working
$ git clone https://github.com/pjreddie/darknet
$ cd darknet
$ make

# If make command worked skip these steps
$ sudo apt update
$ sudo apt install build-essential
	#If build essentials doesnt install everything like it did for me in ubuntu
	$ sudo apt intsall gcc
	$ sudo apt install g++

# Download cuda toolkit as a .run file, cuDNN as a .tgz compressed file
Toolkit: "https://developer.nvidia.com/cuda-downloads"
cuDNN:   "https://developer.nvidia.com/cudnn"

# Give it permissions
$ chmod +x "cuda-toolkit.run-file"

# Clean up a couple of things before installing
follow all instructions here: 
"https://tutorials.technology/tutorials/85-How-to-remove-Nouveau-kernel-driver-Nvidia-install-error.html"

# Install all parts of toolkit 
$ sudo ./"cuda-toolkit.run-file"

# Extract cuDNN files
$ tar zxvf "cudnn-file.tgz"

# Go to directory where you extracted cuDNN presumably /Downloads and copy files over
$ cd ~/Downloads
$ sudo cp cuda/include/cudnn.h /usr/local/cuda/include
$ sudo cp cuda/lib64/* /usr/local/cuda/lib64

# Grant permissions
$ sudo chmod a+r /usr/local/cuda/lib64/libcudnn*

# Need to export the system path to CUDA elements:
$ sudo nano ~/.bashrc

# Go to the very end of this file, and add:
$ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64
$ export CUDA_HOME=/usr/local/cuda
$ export PATH=$PATH:/usr/local/cuda/bin

# Reload paths
$ source ~/.bashrc

# For python usage later on add these
$ sudo nano /etc/enviornment

# Reload changes
$ sudo ldconfig

# Now edit the 'Makefile' in darknet
$ sudo nano Makefile
-> GPU=1
-> CUDNN=1

# Restart computer 
$ sudo reboot

# Head back to darknet directory
$ make clean
$ make

# If the above did not work do the same steps for '~/.profile' as you did for '~/.bashrc'

