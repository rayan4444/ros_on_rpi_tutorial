# Installing ROS on a Raspberry Pi (3/3B+/4)

There are many ways to get ROS running on a Raspberry pi: I chose this specific one because it is the one that makes your code mostly Hardware agnostic, which means your installation won't be very different if you use a Raspberry Pi3B+, Raspberry Pi 4 or a beefier computer. 

### Get Ubuntu for Raspberry Pi
ROS is supported on different OSes but it loves ubuntu, so the first step to keep things simple is to get Ubuntu on your Raspberry pi. There are two main options here:
* [Ubuntu Mate](https://ubuntu-mate.org/) :  easier to install on a pi but doesn't work with Raspberry pi 4 yet (as of 20/05/2020)
* [Ubuntu Server/Core](https://ubuntu.com/download/raspberry-pi): recently added support for Raspberry Pi models. more complicated but more flexible. 

I chose to go ahead with Ubuntu server/core because we might use a Raspberry pi 4. 

#### Instructions:
* You can get the ubuntu image for the Raspberry pi [here](https://ubuntu.com/download/raspberry-pi)
* Make sure you chose one that ROS can support: I chose ubuntu 18.0.4 because I plan to use [ROS Melodic](http://wiki.ros.org/melodic/Installation)
* Follow the official [intallation guide](https://ubuntu.com/download/raspberry-pi/thank-you?version=18.04&versionPatch=.4&architecture=arm64+raspi3). There are links to OS specific sections (MacOS, Windows, Linux) in the guide. 

>Note: Burning the image to the SD card with Windows didn't work for me for some mysterious reason(s) - it could boot up but not login. Burning the same image to the SD card with Linux worked fine.  People have recommended these other image burners which I haven't tested yet: [balena etcher](https://www.balena.io/etcher/)                           

#### Other methods: 
* Follow [other set of official instructions](https://ubuntu.com/tutorials/how-to-install-ubuntu-on-your-raspberry-pi#1-overview)
* Or this [tutorial](https://maker.pro/raspberry-pi/projects/install-ubuntu-18044-lts-on-your-raspberry-pi-board)

#### Desktop or no Desktop?

Especially because the Pi is going to be used inside a robot, there is no real point in installing a desktop. If you chose to install a desktop anyways - the default Unity or more lightweight options like lubuntu, xubuntu , etc. - you can follow the steps in any of the methods above.
> Note: I tried installing lubuntu but it didn't work on my Raspberry Pi  

### Install ROS Melodic

#### Overview:
* Make sure ubuntu is up to date:
```
sudo apt update
sudo apt upgrade
```
> If you have poor internet connection or happen to be in China where some mirrors are really slow, the first upgrade may take some time (HAX office: 2-2.5h)

* Configure ubuntu repositories: You need to allow restricted, universe, and multiverse repositories.
```
sudo add-apt-repository universe
sudo add-apt-repository restricted
sudo add-apt-repository multiverse
```

* Setup sources
```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```

* Setup Repository keys 
```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```
Alternatively, you can use curl instead of the apt-key command, which can be helpful if you are behind a proxy server:
```
curl -sSL 'http://keyserver.ubuntu.com/pks/lookup?op=get&search=0xC1CF6E31E6BADE8868B172B4F42ED6FBAB17C654' | sudo apt-key add -
```

* update
```
sudo apt update
```
* install ROS

What most sources agree on is that choosing the Desktop-Full install on a single board computer is a bad idea. Most sources recommend going for ROS-base, which doesn't include any GUI tools. This makes even more sense if you are using the raspberry pi headless or/and haven't installed a desktop. 

```
sudo apt install ros-melodic-ros-base
```
> > If you have poor internet connection or happen to be in China where some mirrors are really slow, this step can take a long time (HAX office: )

* Setup your environment 
```
echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```
If you just want to change the environment of your current shell, instead of the above you can type:
```
source /opt/ros/melodic/setup.bash
```

* Setup and install your dependencies
```
sudo apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential
```
Before you can use many ROS tools, you will need to initialize ```rosdep```. ```rosdep``` enables you to easily install system dependencies for source you want to compile and is required to run some core components in ROS.
```
sudo apt install python-rosdep
sudo rosdep init
rosdep update
```

### Tutorial links:
* [From ROS](http://wiki.ros.org/melodic/Installation/Ubuntu)
* [Other from ROS](http://wiki.ros.org/ROSberryPi/Installing%20ROS%20Melodic%20on%20the%20Raspberry%20Pi)
* [Other source 1](https://www.instructables.com/id/Getting-Started-With-ROS-Melodic-on-Raspberry-Pi-4/)
* [Other source 2](https://roboticsbackend.com/install-ros-on-raspberry-pi-3/)


## Ubuntu images for Raspberry Pi with pre-installed ROS
ROS Melodic x ubuntu 18.04 x Raspberry Pi 4: 
* [here](https://jamesachambers.com/raspberry-pi-4-ubuntu-server-desktop-18-04-3-image-unofficial/): not tested yet
* [here](https://github.com/TheRemote/Ubuntu-Server-raspi4-unofficial/releases): not tested yet

Other
* [ubiquity robotics raspberry pi image](https://downloads.ubiquityrobotics.com/pi.html): recommended by Rakshak. Read [this](https://learn.ubiquityrobotics.com/image_no_magni) before use

## ROS Learning resources 
If this is your first ROS project, here are some resources to get started
* [Official ROS tutorials](http://wiki.ros.org/ROS/Tutorials): 
* [ROS course on youtube by ETH Zurich](https://www.youtube.com/watch?v=0BxVPCInS3M&list=PLE-BQwvVGf8HOvwXPgtDfWoxd4Cc6ghiP)
* [A gentle introduction to ROS textbook (chinese version available too)](https://www.cse.sc.edu/~jokane/agitr/) 
* [ROS for Beginners: Basics, Motion, and OpenCV](https://www.udemy.com/course/ros-essentials/). The author has made a couple of classes from this course freely available on youtube [here](https://www.youtube.com/playlist?list=PLSzYQGCXRW1H8R2Bok_K8wcsE12_49alQ)
* The Construct is another good learning resource, they give you an online ROS environment(complete with the Gazebo 3D simulator) all set up and ready to go. [link](https://www.theconstructsim.com/)

