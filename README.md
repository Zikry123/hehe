<img width="91" alt="va logo 2" src="https://user-images.githubusercontent.com/39509760/40403375-37fbc738-5e84-11e8-88d3-f04d9b7f21a3.PNG">
&nbsp;
&nbsp;
&nbsp;
&nbsp;  
&nbsp; 

#  **Overview**

Smart cameras are able to track assets and people in order to maximise business revenues and reduce leakages by being "aware" of their surroundings.

### Features

- Tracks valuable assets to prevent any damages or misplacement.

- Tracks the number of customer footfall for each attraction.

- Ensure that the duration of the usage of assets adhere to the stipulated timing imposed to the customer.

- Immediate notice on which attraction require crowd control.

- Potentially alert lifesaving services in an event of a crisis.


### System requirements

- Ubuntu 18.04 LTS

- Nvidia Drivers

- CUDA Toolkit 9.1

- OpenCV 3.4.0
   gcc-<=6 and g++<=6, required for compiling CUDA within OpenCV (Ubuntu 18.04 LTS comes with gcc-7 and g++-7 as default)
  
- Darknet Yolo v3 (Specific version required) --> https://github.com/pjreddie/darknet/tree/yolov3  
   

-----------------------

#  **Animated Tutorial**

<div style="float:left; width:100%">
    <img src="https://raw.githubusercontent.com/facerecog/auto-ssh-tunnel/gh-pages/images/intro_video.gif" align="left" width=540px height=310px  /> 
</div>


&nbsp;
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  

-----------------------

# **Getting started** 



### Download

Clone the latest repository version from Github (recommended):  
`$ git clone https://github.com/facerecog/auto-ssh-tunnel.git`  

Alternatively, download the .tar.gz  file from the top of this page and unpack it:  
`$ wget https://github.com/facerecog/auto-ssh-tunnel/tarball/master  -O - | tar -xz `  


Now `cd` into the newly extracted directory.


### Installation 

0. Install Ubuntu 18.04 LTS
1. Install Nvidia Drivers
   - Reboot
2. Install gcc-<=6 and g++<=6, required for compiling CUDA within OpenCV:
    $ sudo apt-get install gcc-6
    $ sudo apt-get install g++-6

    $ sudo su
    $ cd /usr/bin/
    $ rm gcc
    $ rm gcc-ar
    $ rm gcc-nm
    $ rm gcc-ranlib
    $ rm g++

    $ ln -s gcc-6 gcc
    $ ln -s gcc-ar-6 gcc-ar
    $ ln -s gcc-nm-6 gcc-nm
    $ ln -s gcc-ranlib-6 gcc-ranlib
    $ ln -s g++-6 g++

3. Install CUDA 9.1
  Download https://launchpad.net/ubuntu/+archive/primary/+files/nvidia-cuda-toolkit_9.1.85.orig.tar.gz from: https://launchpad.net/ubuntu/+source/nvidia-cuda-toolkit/9.1.85-3ubuntu1
    Add these to ~/.bashrc
    export PATH=/usr/local/cuda-9.1/bin${PATH:+:${PATH}}
    export LD_LIBRARY_PATH=/usr/local/cuda-9.1/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
    $ source ~/.bashrc
    add /usr/local/cuda-9.1/lib64 to /etc/ld.so.conf
    $ sudo ldconfig
4. Compile OpenCV following https://www.pyimagesearch.com/2016/10/24/ubuntu-16-04-how-to-install-opencv/ with some modifications:
    - in Step #1 change:
    $ sudo apt-get install libjpeg8-dev libtiff5-dev libjasper-dev libpng12-dev
     to
    $ sudo add-apt-repository "deb http://security.ubuntu.com/ubuntu xenial-security main"
    $ sudo apt update
    $ sudo apt install libjasper1 libjasper-dev
    $ sudo apt-get install libjpeg8-dev libtiff5-dev libpng-dev
    (https://stackoverflow.com/questions/43484357/opencv-in-ubuntu-17-04/44488374#44488374)

    - Compile OpenCV using the command:
    $ cmake -D CMAKE_BUILD_TYPE=RELEASE \
-D CMAKE_INSTALL_PREFIX=/usr/local \
-D WITH_CUDA=ON \
-D ENABLE_FAST_MATH=1 \
-D CUDA_FAST_MATH=1 \
-D CUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda-9.1 \
-D WITH_CUBLAS=1 \
-D INSTALL_PYTHON_EXAMPLES=ON \
-D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib-3.4.0/modules \
-D PYTHON_EXECUTABLE=~/.virtualenvs/cv3/bin/python \
-D CUDA_NVCC_FLAGS=--expt-relaxed-constexpr \
-D BUILD_EXAMPLES=ON \
-D INSTALL_PYTHON_EXAMPLES=ON \
-D INSTALL_C_EXAMPLES=OFF ..


# **How the script works**  

During installation, the script will automatically append the following lines to /etc/ssh/ssh_config:
```
ServerAliveInterval 30
ServerAliveCountMax 4
```
It will also append the following to /etc/ssh/sshd_config
```
ClientAliveInterval 30
ClientAliveCountMax 4
```

Upon boot, the client will run `connect.py`, which sets up a reverse ssh tunnel. The server may now ssh into the client even if the client resides behind a NAT firewall.

-------------------------

# **Verify that it works**  

* From the client, ssh into your server:  
`$ ssh <rootname>@<ip address>`  

* Once in, connect back to your client:  
`$ ssh <your username>@localhost -p <port number specified as above>`

* If successful, you have just ssh-ed back into your client. Congratulations and enjoy!

-------------------------

# **Reverse SSH Tunnel Diagram**  

<img src="https://raw.githubusercontent.com/facerecog/auto-ssh-tunnel/gh-pages/images/Client-server%20diagram.png"/>


-------------------------

# **Uninstall**  

To uninstall:
`$ sudo rm -rf /etc/init.d/connect.py /etc/auto-ssh-tunnel /usr/local/bin/connect.py /System/Library/StartupItems/auto-ssh-tunnel/`  


-------------------------

# **Support**  

If you want to support this project, please consider reaching out to me via  muhd.amrullah@facerecog.asia  


-------------------------  
Property of Facerecog Asia Pte. Ltd. and 26 Factorial
