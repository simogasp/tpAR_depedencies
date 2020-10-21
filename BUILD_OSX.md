# OSX

These are the steps to build all you need for the TP.


## Prerequisites

In order to develop in C++ and OpenGL check if 

```
ls  /System/Library/Frameworks/
```
contains OpenGL and GLUT frameworks.
If not, you need to install XCode  from the `Mac App Store`, see here for more details https://developer.apple.com/support/xcode/

* everything will be smoother if you have homebrew installed (https://brew.sh/): it is a package manager similar in spirit to the one you find in Linux.

    * `brew install automake cmake` will install everything you need for building the code.

    * if you don't have homebrew you can install CMake by downloading https://github.com/Kitware/CMake/releases/download/v3.17.1/cmake-3.17.1-Darwin-x86_64.dmg

## Setting up your working environment

* create a folder `tpAR` where you will have all the dependencies and the sources of the tp.
  Please avoid paths containing spaces, weird characters or accents.

* to make your life easier, set up an environment variable that refer to this location

  * You can define it for a single session with (e.g.) `export tpARBasePath=/home/sgaspari/dev/tpAR`

  * or you can define it once for all by adding the previous instruction to your `~/.profile` file, so that you don't need to run the instruction for each terminal session.

  * you can verify that the variable is set with `echo ${tpARBasePath}`


## opencv

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


* in order to run the tp code later on you have to add the built libraries to the `DYLD_LIBRARY_PATH` environment variable.

    ```
    export DYLD_LIBRARY_PATH=${tpARBasePath}/opencv-2.4.13.4/build/install/lib:$DYLD_LIBRARY_PATH
    ```

  Again, you can add this to your `~/.profile` file so that you have it available for all shell sessions.