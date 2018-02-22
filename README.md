opencvp
=======

**OpenCV Practice Repository**

For OpenCV (> 3.x.x) on Ubuntu (> 14) check this: [Ubuntu 16.04](https://github.com/milq/milq/blob/master/scripts/bash/install-opencv.sh) AND after building put

```
sudo /bin/bash -c 'echo "/usr/local/lib" > /etc/ld.so.conf.d/opencv.conf'
```



Installing OpenCV on Linux platform (Ubuntu)
---------------------------------------------
**Credits**:
[http://www.raben.com/book/export/html/3]
[http://karytech.blogspot.in/2012/05/opencv-24-on-ubuntu-1204.html]

- Install developer environment to build OpenCV source code:

```
sudo apt-get install build-essential cmake pkg-config
```
- Install Image I/O libraries:

```
sudo apt-get install libjpeg62-dev libpng-dev
sudo apt-get install libtiff5-dev libjasper-dev
```

- Install Python development environment:

```
sudo apt-get install python-dev python-numpy
```

- Install Video I/O libraries:

```
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libdc1394-22-dev libxine2-dev libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev libv4l-dev
```

**Optional**

- Install Intel TBB for OpenCV parallelism library:

```
sudo apt-get install libtbb-dev
```

- Install GUI backend-GTK or QT:

```
sudo apt-get install libqt5-dev libgtk2.0-dev
sudo apt-get install qt5-default
```

**Get OpenCV Source Code:**

Get latest version using Git:

```
cd ~/path/to/working/directory
git clone https://github.com/Itseez/opencv.git
```

Or get the source package from http://opencv.org/downloads.html, extract and create build directory inside opencv directory:
(Replace * with numbers as per requirement)
```
tar -xvf OpenCV-*.*.*.tar.bz2
cd OpenCV-*.*.*
mkdir build
cd build
```

- Now is the time to generate configure OpenCV build using Cmake. Last two dots are for source directory of OpenCV (Parent Directory here):

```
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local
    -D WITH_TBB=ON -D BUILD_NEW_PYTHON_SUPPORT=ON -D WITH_V4L=ON
    -D INSTALL_C_EXAMPLES=ON -D INSTALL_PYTHON_EXAMPLES=ON
    -D BUILD_EXAMPLES=ON -D WITH_QT=ON -D WITH_OPENGL=ON ..
```

- Compiling: (add -j3 or -j4 to make compiling faster)

```
make
```
- Install:

```
sudo make install
```

Add following line at the end of **/etc/ld.so.conf** to link OpenCV library at run-time:

```
/usr/local/lib
```

Now configure dynamic linker run-time bindings:

```
sudo ldconfig
```


 

**Using OpenCV in your project:**

- First using following command to find out the locations of OpenCV files for **include path(-l)**

```
pkg-config --cflags opencv
```

which gives results like this:

```
-I/usr/local/include/opencv -I/usr/local/include
```
So include path is: **/usr/local/include/opencv**

- Now we find libraries path using following command:

```
pkg-config --libs opencv
```

which gives result like this:

```
/usr/local/lib/libopencv_bioinspired.so /usr/local/lib/libopencv_calib3d.so ...

```
So Library search path (-L) is: **/usr/local/lib**

These path can be included in Compiler Settings of IDEs.

**Uninstalling:**

```
cd /path/to/OpenCV-*.*.*/build
sudo make uninstall
```

**Compiling C++ File using command line:**

```
g++ prog.cpp -o prog `pkg-config --cflags --libs opencv`

```

Installation on Windows
-----------------------------

##### Step 1: Install MinGW

- Download MinGW.
- Install it in the **C** drive as **C:\MinGW** .
- While installing select options: **mingw32-base** and **mingw32-gcc-g++** (required).
- Add **C:\MinGW\bin** to the System Environment PATH variable. Make sure you separate this entry from the last entry using a semicolon (;), like: **lastentry_xyz;C:\MinGW\bin** .
- Verify path variable through path command in the shell.

##### Step 2: Install Code::Blocks IDE

- Download and install with default procedure.
- Go to **Settings -> Compiler and Debugger**
- Select **GNU GCC Compiler** as default compiler and select auto-detect. It'll detect **C:\MinGW**
- Save all the changes.
- You can test the compiler using a simple Hello_World.cpp program.

##### Step 3: Building OpenCV from source using CMake

- Download and install CMake.
- Download OpenCV and extract source at **C:\opencv** 
- Launch CMake and select **C:\opencv** as a source directory and **C:\opencv\build\x86\mingw** as the destination directory.
- Click configure > Choose minGW makefiles then generate. Make sure it is done.
- Open command window in the destination directory: **C:\opencv\build\x86\mingw** 
- Type following command (add **-j3** on dual core processor to accelerate building process):

```
mingw32-make
```

- Compiling process does take long time. When compiling is over, type this command:

```
mingw32-make install
```

- Add **C:\opencv\build\x86\mingw\bin** to the system PATH exactly in the same manner as we did for **C:\MinGW\bin** .
- To check both OpenCV and MinGW have been correctly added to system path, type following command in your shell:
```
path
```
which must show **C:\MinGW\bin** and **C:\opencv\build\x86\mingw\bin** .

##### Step 4: OpenCV Project configuration on Code::Blocks IDE:

- Create a new console project.
- In the editor's project tree, right click on the Project's name and click on **Build Options**.
- Go to **search directories** tab, click on **compiler** sub-tab, and add the path **C:\opencv\build\include** .
- Now go-to **linker** sub-tab and add the path **C:\opencv\build\x86\mingw\lib** .
- Now go-to **Linker Settings** tab, and add all \*.dll.a libraries through browsing to **C:\opencv\build\x86\mingw\lib** .
- Save the changes. We're done! :-)



Helpful Links [Link1](http://www.iitg.ernet.in/cse/robotics/?page_id=1115)

[Link2](http://www.laganiere.name/opencvCookbook/chap1s1_2.shtml)
