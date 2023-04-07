# Depedencies

## Pangolin

Clone the repo and follow the build instructions provided

```
git clone -b v0.6 --single-branch git@github.com:stevenlovegrove/Pangolin.git
```

## OpenCV

```
git clone -b 4.7.0 --single-branch git@github.com:opencv/opencv.git
git clone -b 4.7.0 --single-branch git@github.com:opencv/opencv_contrib.git

cd opencv
mkdir -p build && cd build

# Configure
cmake -DOPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules ..

# Build
cmake --build .
```

## Depthai-Core

Clone the repo and follow the build instructions provided

```
git clone -b v2.21.2 --single-branch git@github.com:luxonis/depthai-core.git
```

# Building
Run the following instructions in the root directory of the repository

```
mkdir build && cd build
cmake ..
cmake --build .
```