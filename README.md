# Caffe_Jetson_Installation


OpenCV
$ sudo apt install python3-opencv
ATLAS Or BLAS
# BLAS
`sudo apt-get install libatlas-base-dev `# Atlas
or 
`sudo apt-get install libopenblas-dev` # OpenBLAS
Other dependencies,
# Other dependencies
`sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler`
` sudo apt-get install — no-install-recommends libboost-all-dev`
` sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev`
` sudo pip3 install protobuf`
` sudo apt-get install the python3-dev`
Step 2: Go to the folder where you want to install Caffe (I am using ~/), then clone the latest git repository by issuing the following command
` git clone https://github.com/BVLC/caffe.git`
Then, go to the Caffe directory,
` cd caffe`
Step 3: Make a copy of Makefile.config.example and rename it as Makefile.config
` cp Makefile.config.example Makefile.config`
Step 4: Make the following changes in Makefile.config file.
`OPENCV_VERSION := 3` # if you are using OpenCV 3 or above
For CUDA version 10, you can use the below changes.
`CUDA_ARCH := 
# -gencode arch=compute_20,code=sm_20 \
# -gencode arch=compute_20,code=sm_21 \
 -gencode arch=compute_30,code=sm_30 \
 -gencode arch=compute_35,code=sm_35 \
 -gencode arch=compute_50,code=sm_50 \
 -gencode arch=compute_52,code=sm_52 \
 -gencode arch=compute_60,code=sm_60 \
 -gencode arch=compute_61,code=sm_61 \
 -gencode arch=compute_61,code=compute_61`
Whichever, you installed above,
`BLAS := atlas` # if you’ve installed Atlas (default)
or
`BLAS := open` # if you’ve installed OpenBLAS
We are using python3 here so need for python2 lines,
#PYTHON_INCLUDE := /usr/include/python2.7 \
# /usr/lib/python2.7/dist-packages/numpy/core/include
We are using python3,
`PYTHON_LIBRARIES := boost_python3 python3.6m
PYTHON_INCLUDE := /usr/include/python3.6m \
/usr/lib/python3.6/dist-packages/numpy/core/include`
This line is necessary for building the hdf5,
INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include /usr/include/hdf5/serial
LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib/aarch64-linux-gnu/hdf5/serial
All the above changes are mentioned in this Makefile.config file.
Step 5: Install Caffe by issuing the following commands. Make sure you are in the caffe root directory.
` make all -j4 `# 4 represents number of CPU Cores
` make pycaffe -j4 `# 4 represents number of CPU Cores
Note: If you encounter any error then don’t forget to REMOVE BUILD every time you resolve the error by running the following command and then try rebuilding.
` make clean`
Step 6: Add the path of caffe/python directory to ~/.bashrc
`export PYTHONPATH=~/caffe/python:$PYTHONPATH`
Restart the system
Step 7: Check by importing Caffe in the python interpreter.
` python3`
>>> import caffe
If anyone faced any error they can comment and I’ll be happy to help. 
