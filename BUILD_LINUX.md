# Linux

These are the steps to build all you need for the TP.


## Prerequisites

In order to develop in C++ some system packages are required (you may already have it installed on your machine since the opengl tp of last semester):

```
sudo apt-get install libglu1-mesa-dev freeglut3-dev build-essential mesa-common-dev libxi-dev libxmu-dev automake libgtk+2.0-dev pkg-config libgstreamer1.0-dev  libgstreamer-plugins-base1.0-dev  libgstreamer-plugins-good1.0-dev  libv4l-dev  gstreamer1.0-plugins-bad ubuntu-restricted-extras
```

### CMake

To build this code we use the CMake build system. 
You can install CMake from the system package manager but you need a recent version >= 3.10. 
Check the version that is provided by your linux distribution and if it is suitable usually you just need to


```shell
sudo apt-get install cmake
```

otherwise you can install the binaries from here (choose Linux x86_64):: https://cmake.org/download/
    
Once downloaded the latest version X.YY.Z, in order to install:

```shell
chmod +x cmake-X.YY.Z-Linux-x86_64.sh
sudo ./cmake-X.YY.Z-Linux-x86_64.sh --prefix=/usr/local/ --skip-license
```
  

## Setting up your working environment

* create a folder `tpAR` where you will have all the dependencies and the sources of the tp.
  Please avoid paths containing spaces, weird characters or accents.

* to make your life easier, set up an environment variable that refer to this location

  * You can define it for a single session with (e.g.) `export tpARBasePath=/home/sgaspari/dev/tpAR`

  * or you can define it once for all by adding the previous instruction to your `~/.bashrc` (or `~/.profile`) files, so that you don't need to run the instruction for each terminal session.

  * you can verify that the variable is set with `echo ${tpARBasePath}`


## OpenCV

OpenCV is a computer vision library that contains some of the algorithms we are using for image processing and pose estimation.
To install it:

* download the library from the repository https://github.com/opencv/opencv/archive/2.4.13.4.zip

* unzip the file into `${tpARBasePath}` (a folder named `opencv-2.4.13.4` should appear).

* from `${tpARBasePath}\opencv-2.4.13.4` create a `build` directory (`mkdir build`)

* from the shell, go to `${tpARBasePath}/opencv-2.4.13.4/build` and execute the following:

    ```
    cmake .. -DCMAKE_INSTALL_PREFIX:PATH=`pwd`/install -DCMAKE_BUILD_TYPE=Release -DWITH_CUDA:BOOL=OFF -DBUILD_PERF_TESTS:BOOL=OFF -DBUILD_TESTS:BOOL=OFF
    ```
    
* then build and install the library by running

    ```
    make install -j$(nproc) 
    ```
  and go grab a cup of coffee or a beverage of your choice ;-)


* in order to run the tp code later on you have to add the built libraries to the `LD_LIBRARY_PATH` environment variable.

    ```
    export LD_LIBRARY_PATH=${tpARBasePath}/opencv-2.4.13.4/build/install/lib:$LD_LIBRARY_PATH
    ```

  Again, you can add this to your `~/.bashrc` (or `~/.profile`) file so that you have it available for all shell sessions.
