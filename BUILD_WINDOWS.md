# Windows

These are the steps to build all you need for the TP.



## Prerequisites

The building process requires CMake and MS Visual Studio. 
You may already have it installed on your machine since the opengl tp of last semester.

If it is not the case:

* download and install the latest version of CMake

   * download here (choose "Windows x64 Installer:"): https://cmake.org/download/

   * :warning: When installing make sure that the checkbox "ne pas ajouter cmake au PATH" is **NOT** checked
 

* if you don't have it already, download and install MS Visual Studio Community Edition (free for students): https://visualstudio.microsoft.com/downloads/

    * install instructions here: https://docs.microsoft.com/en-us/cpp/build/vscpp-step-0-installation?view=vs-2019
    
    * :warning: install the "Desktop development with C++"
    
    * If you have VS already installed, you can go in **Tools** --> **Get Tools and Features...** to install "Desktop development with C++" if it is missing.


## Setting up your working environment

* create a folder `tpAR` where you will have all the dependencies and the sources of the tp.
  > [!WARNING]  
  > Place the folder in a path that does not contain **spaces**, **weird characters** or **accents**.

* to make your life easier, set up an environment variable that refer to this location

  * from the prompt (`cmd.exe`) execute `c:\Windows\System32\SystemPropertiesAdvanced.exe `

  * click `Environment Variables...`  (`Variables d'environnement...`)

  * in `User Variables for ...` ( `Variables utilisateur pour...`) click `New...` and set a new variable named
  `tpARBasePath` and set its value to the full path to the working directory, e.g. `C:\Users\Simone\source\tpAR`

  * once you set it, in order to be usable at command line you need to open a new session of prompt/powershell

  * if you open the session you can check it is working by running `echo %tpARBasePath%`  in command prompt (or `$env:tpARBasePath` in powershell)
    This should display the whole path to tpAR.


## freeglut

The library is necessary for the opengl rendering of the virtual object. 
To install it:

* download the libraries from here https://github.com/simogasp/tpAR_depedencies/raw/main/freeglut-MSVC-3.0.0-2.mp.zip

* unzip the file into `%tpARBasePath%` so that a `freeglut` directory appears, inside you find the usual structure of directories `bin`, `include` and `lib` etc.


## glm

GLM is a C library that reads 3D models from .obj files and render them using opengl directives.
To install it:

* download the library from the repository https://github.com/simogasp/glm/archive/win.zip

* unzip the file into `%tpARBasePath%` so that a `glm-win` directory appears.

* go to `%tpARBasePath%\glm-win` and create a `build` directory (`mkdir build`)

* from the terminal/prompt, go to `%tpARBasePath%\glm-win\build` and execute the following:

    ```
    cmake .. -G "Visual Studio 16 2019" -A x64 -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX:PATH=%tpARBasePath%\glm-win\build\install -DGLUT_ROOT_PATH:PATH=%tpARBasePath%\freeglut -DBUILD_EXAMPLES:BOOL=OFF  -Wno-dev
    ```
    or, if you are using PowerShell, rememeber that the enviromental variables are written as e.g. `$env:tpARBasePath`, so:
    ```
    cmake .. -G "Visual Studio 16 2019" -A x64 -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX:PATH=$env:tpARBasePath\glm-win\build\install -DGLUT_ROOT_PATH:PATH=$env:tpARBasePath\freeglut -DBUILD_EXAMPLES:BOOL=OFF  -Wno-dev
    ```

> [!NOTE] 
> if you had a different version of VS installed (not the latest) you may need to adapt the string `Visual Studio 16 2019` to your version: e.g. `Visual Studio 15 2017`, `Visual Studio 14 2015`, `Visual Studio 12 2013` etc
    
* then execute

    ```
    cmake --build . --config Release --target install
    ```

  this should compile the sources and install the library in `%tpARBasePath%\glm-win\build\install`.


## OpenCV

OpenCV is a computer vision library that contains some of the algorithms we are using for image processing and pose estimation.
To install it:

* download the library from the repository https://github.com/opencv/opencv/archive/2.4.13.4.zip

* unzip the file into %tpARBasePath% (a folder named `opencv-2.4.13.4` should appear).

* from `%tpARBasePath%\opencv-2.4.13.4` create a `build` directory (`mkdir build`)

* from the terminal/prompt, go to `%tpARBasePath%\opencv-2.4.13.4\build` and execute the following:

    ```
    cmake .. -G "Visual Studio 16 2019" -A x64 -DCMAKE_BUILD_TYPE=Release -DWITH_CUDA:BOOL=OFF -DBUILD_PERF_TESTS:BOOL=OFF -DBUILD_TESTS:BOOL=OFF -DWITH_OPENEXR:BOOL=OFF -DWITH_OPENCL:BOOL=OFF -DBUILD_opencv_ts:BOOL=OFF
    ```

> [!NOTE] 
> if you had a different version of VS installed (not the latest) you may need to adapt the string `Visual Studio 16 2019` to your version: e.g. `Visual Studio 15 2017`, `Visual Studio 14 2015`, `Visual Studio 12 2013` etc
    
* then execute

    ```
    cmake --build . --config Release 
    ```

  and go grab a cup of coffee or a beverage of your choice ;-)


## Setting up the runtime environment variables

The last step before start working on the TP is to set up the environment variables that allows the system to find the libraries you just installed/built.

* from the prompt execute `c:\Windows\System32\SystemPropertiesAdvanced.exe `

  * click `Environment Variables...`  (`Variables d'environnement...`)

  * in `User Variables for ...` (`Variables utilisateur pour...`), select the variable `Path` and then click `Edit...` 

  * add at the bottom of the list the following paths:

    * `%tpARBasePath%\opencv-2.4.13.4\build\bin\Release`

    * `%tpARBasePath%\freeglut\bin\x64\`

