# Smarty_mob_foxy arm64
All the commands on this repository is for Ubuntu 20.05(focal fossa) foxy version. As I initialllly used the lastest humble version of ubuntu and turtlebot3 has no support for humble version, I had to convert to earlier foxy version of ubuntu.


# Ubtuntu (Deebian)
Debian packages for ROS 2 Foxy Fitzroy are currently available for Ubuntu Focal.


## Set locale
Make sure that you have a locale which supports ***UTF-8***. If you are in a minimal environment (such as a docker container), the locale may be something minimal like POSIX. We test with the following settings. However, it should be fine if you’re using a different UTF-8 supported locale.

```
akbarjon@ubuntu:~$ locale
LANG=en_US.UTF-8
LANGUAGE=
LC_CTYPE="en_US.UTF-8"
LC_NUMERIC="en_US.UTF-8"
LC_TIME="en_US.UTF-8"
```


```
akbarjon@ubuntu:~$ sudo apt update && sudo apt install locales
[sudo] password for akbarjon: 
Get:1 http://ports.ubuntu.com/ubuntu-ports focal-security InRelease [114 kB]
Hit:2 http://us.ports.ubuntu.com/ubuntu-ports focal InRelease             
Get:3 http://us.ports.ubuntu.com/ubuntu-ports focal-updates InRelease [114 kB]
Get:4 http://ports.ubuntu.com/ubuntu-ports focal-proposed InRelease [267 kB]
```

```
akbarjon@ubuntu:~$ sudo locale-gen en_US en_US.UTF-8
Generating locales (this might take a while)...
  en_US.ISO-8859-1... done
  en_US.UTF-8... done
Generation complete.
```

```
kbarjon@ubuntu:~$ sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
akbarjon@ubuntu:~$ export LANG=en_US.UTF-8
akbarjon@ubuntu:~$ locale
LANG=en_US.UTF-8
LANGUAGE=
LC_CTYPE="en_US.UTF-8"
LC_NUMERIC="en_US.UTF-8"
LC_TIME="en_US.UTF-8"
LC_COLLATE="en_US.UTF-8"
LC_MONETARY="en_US.UTF-8"
LC_MESSAGES="en_US.UTF-8"
LC_PAPER="en_US.UTF-8"
LC_NAME="en_US.UTF-8"
LC_ADDRESS="en_US.UTF-8"
LC_TELEPHONE="en_US.UTF-8"
LC_MEASUREMENT="en_US.UTF-8"
LC_IDENTIFICATION="en_US.UTF-8"
LC_ALL=
```

## Setup Sources
ROS 2 apt repositories needs to be added to your system
First, make sure that the Ubuntu Universe repository is enabled by checking the output of this command
```
kbarjon@ubuntu:~$ apt-cache policy | grep universe
```
There should output links like this:
```
 500 http://ports.ubuntu.com/ubuntu-ports focal-security/universe arm64 Packages
     release v=20.04,o=Ubuntu,a=focal-security,n=focal,l=Ubuntu,c=universe,b=arm64
 100 http://us.ports.ubuntu.com/ubuntu-ports focal-backports/universe arm64 Packag
 ```
 If you don’t see an output line like the one above, then enable the Universe repository with these instructions.
 ```
sudo apt install software-properties-common
sudo add-apt-repository universe
```

Adding ROS2 apt repositories to your system.
```
akbarjon@ubuntu:~$ sudo apt update && sudo apt install curl gnupg2 lsb-release
Hit:1 http://ports.ubuntu.com/ubuntu-ports focal-security InRelease     
Hit:2 http://ports.ubuntu.com/ubuntu-ports focal-proposed InRelease     
.
.
Processing triggers for libc-bin (2.31-0ubuntu9.9) ..
```
 
Then add the repository to your source list
```
akbarjon@ubuntu:~$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(source /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

# Install ROS1 packages
Update your apt repository caches after setting up the repositories.
```
akbarjon@ubuntu:~$ sudo apt update
Hit:1 http://us.ports.ubuntu.com/ubuntu-ports focal InRelease           
Hit:2 http://us.ports.ubuntu.com/ubuntu-ports focal-updates InRelease   
Hit:3 http://us.ports.ubuntu.com/ubuntu-ports focal-backports InRelease
```
ROS 2 packages are built on frequently updated Ubuntu systems. It is always recommended that you ensure your system is up to date before installing new packages.
```
akbarjon@ubuntu:~$ sudo apt upgrade
Reading package lists... Done
Building dependency tree       
Reading state information... Done
.
.
Processing triggers for dbus (1.12.16-2ubuntu2.2) ...
Processing triggers for desktop-file-utils (0.24-1ubuntu3) ...
```

```
akbarjon@ubuntu:~$ sudo apt update -y
Get:1 http://ports.ubuntu.com/ubuntu-ports focal-security InRelease [114 kB]                                 
Get:2 http://packages.ros.org/ros/ubuntu focal InRelease [4,679 B]                                           
.
.
Fetched 7,765 kB in 9s (900 kB/s)                                                                                                                    
Reading package lists... Done
Building dependency tree       

```
```
akbarjon@ubuntu:~$ sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" >
> /etc/apt/sources.list.d/ros-latest.list'
[sudo] password for akbarjon: 
sh: 2: Syntax error: newline unexpected
akbarjon@ubuntu:~$ sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" >/etc/apt/sources.list.d/ros-latest.list'
akbarjon@ubuntu:~$ sudo apt install curl
Reading package lists... Done
Building dependency tree       
Reading state information... Done
curl is already the newest version (7.68.0-1ubuntu2.14).
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
akbarjon@ubuntu:~$ curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
OK
akbarjon@ubuntu:~$ sudo apt update -y
Get:1 http://ports.ubuntu.com/ubuntu-ports focal-security InRelease [114 kB]                                 
Get:2 http://packages.ros.org/ros/ubuntu focal InRelease [4,679 B]                                           
Hit:3 http://us.ports.ubuntu.com/ubuntu-ports focal InRelease           
```
Desktop Install (Recommended): ROS, RViz, demos, tutorials.
```
akbarjon@ubuntu:~$ sudo apt install ros-foxy-desktop python3-argcomplete
[sudo] password for akbarjon: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done

```
ROS-Base Install (Bare Bones): Communication libraries, message packages, command line tools. No GUI tools.
```
akbarjon@ubuntu:~$ sudo apt install ros-foxy-desktop python3-argcomplete
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  autoconf automake autotools-dev blt cmake cmake-data cpp-8 cppcheck cython3 dbus dbus-x11 default-libmysqlclient-dev docutils-common fonts-lyx
  freeglut3 gcc-8 gcc-8-base gdal-data gfortran gfortran-8 gfortr...
  ```
  <img width="1361" alt="image" src="https://user-images.githubusercontent.com/76453238/198311604-2dc42095-7b2f-414e-9bd6-7daec9b1c5fe.png">

  
##Environment setup
Sourcing the setup script

Set up your environment by sourcing the following file.
```
# Replace ".bash" with your shell if you're not using bash
# Possible values are: setup.bash, setup.sh, setup.zsh
source /opt/ros/foxy/setup.bash
```
## Lets try some examples
If you installed ros-foxy-desktop above you can try some examples.

In one terminal, source the setup file and then run a C++ talker:

```
akbarjon@ubuntu:~$ source /opt/ros/foxy/setup.bash
akbarjon@ubuntu:~$ ros2 run demo_nodes_cpp talker
[INFO] [1666880893.900723534] [talker]: Publishing: 'Hello World: 1'
[INFO] [1666880894.904714803] [talker]: Publishing: 'Hello World: 2'
[INFO] [1666880895.900497974] [talker]: Publishing: 'Hello World: 3'
[INFO] [1666880896.900471760] [talker]: Publishing: 'Hello World: 4'
[INFO] [1666880897.902563533] [talker]: Publishing: 'Hello World: 5'
```
<img width="669" alt="image" src="https://user-images.githubusercontent.com/76453238/198364570-06bea6f6-88a9-49af-964d-191c57cff44e.png">

In another terminal source the setup file and then run a Python listener:
```
akbarjon@ubuntu:~$ source /opt/ros/foxy/setup.bash 
akbarjon@ubuntu:~$ ros2 run demo_nodes_py listener
[INFO] [1666880931.915788012] [listener]: I heard: [Hello World: 39]
[INFO] [1666880932.899806043] [listener]: I heard: [Hello World: 40]
[INFO] [1666880933.903126481] [listener]: I heard: [Hello World: 41]
[INFO] [1666880934.899787578] [listener]: I heard: [Hello World: 42]
[INFO] [1666880935.901169540] [listener]: I heard: [Hello World: 43]

```
<img width="679" alt="Screen Shot 2022-10-28 at 3 02 31 AM" src="https://user-images.githubusercontent.com/76453238/198364945-7edc51fe-b53e-49dd-a0c0-ae7ac28a70ef.png">
 
 
 Press Control/Command+C to stop
 
 
 #Configuring environment
 ```
 akbarjon@ubuntu:~$ source /opt/ros/foxy/s
setup.bash  setup.sh    setup.zsh   share/      src/
akbarjon@ubuntu:~$ source /opt/ros/foxy/setup.bash 
akbarjon@ubuntu:~$ printenv | grep -i ROS
ROS_VERSION=2
ROS_PYTHON_VERSION=3
AMENT_PREFIX_PATH=/opt/ros/foxy
PYTHONPATH=...
LD_LIBRARY_PATH=...
ROS_LOCALHOST_ONLY=0
PATH=/opt...
ROS_DISTRO=foxy
akbarjon@ubuntu:~$ export ROS_DOMAIN_ID=<your_domain_id>
bash: syntax error near unexpected token `newline'
akbarjon@ubuntu:~$ export ROS_DOMAIN_ID=<your_domain_id>
bash: syntax error near unexpected token `newline'
akbarjon@ubuntu:~$ export ROS_DOMAIN_ID=<0>
bash: syntax error near unexpected token `0'
akbarjon@ubuntu:~$ export ROS_DOMAIN_ID=<101>
bash: syntax error near unexpected token `101'
akbarjon@ubuntu:~$ export ROS_LOCALHOST_ONLY=1
akbarjon@ubuntu:~$ echo "export ROS_LOCALHOST_ONLY=1" >> ~/.bashrc
```

# Turtlesim installation
Install the ROS@ packages for your distro
```
akbarjon@ubuntu:~$ sudo apt update
[sudo] password for akbarjon: 
Get:1 http://ports.ubuntu.com/ubuntu-ports focal-security InRelease [114 kB]
Hit:2 http://packages.ros.org/ros/ubuntu focal InRelease               
.
Building dependency tree 
Reading state information... Done

akbarjon@ubuntu:~$ sudo apt install ros-foxy-turtlesim
Reading package lists... Done
Building dependency tree       
Reading state information... Done
ros-foxy-turtlesim is already the newest version (1.2.6-1focal.20221013.002018).
ros-foxy-turtlesim set to manually installed.

```
check that the package iinstalled
```
akbarjon@ubuntu:~$ source /opt/ros/foxy/setup.bash
akbarjon@ubuntu:~$ ros2 pkg executables turtlesim 
```
the above. command should return the list of turtlesim executeables
```
turtlesim draw_square
turtlesim mimic
turtlesim turtle_teleop_key
turtlesim turtlesim_node
```

## Starting the turtlesim

In order to start the turtlesim enter the following command in your terminal
```
akbarjon@ubuntu:~$ ros2 run turtlesim turtlesim_node
[INFO] [1666904439.121519095] [turtlesim]: Starting turtlesim with node name /turtlesim
[INFO] [1666904439.125220296] [turtlesim]: Spawning turtle [turtle1] at x=[5.544445], y=[5.544445], theta=[0.000000]
```
The simulator windows shou;d illustrate random turtle in the centre like this:

<img width="511" alt="Screen Shot 2022-10-28 at 6 02 22 AM" src="https://user-images.githubusercontent.com/76453238/198397394-9a2183ce-c227-40b8-933b-1bea1224ab9d.png">


## Use turtlesim

Open a new terminal and source ROS 2 again.

Now you will run a new node to control the turtle in the first node
```
akbarjon@ubuntu:~$ source /opt/ros/foxy/setup.bash
akbarjon@ubuntu:~$ ros2 run turtlesim turtle_teleop_key
Reading from keyboard
---------------------------
Use arrow keys to move the turtle.
Use G|B|V|C|D|E|R|T keys to rotate to absolute orientations. 'F' to cancel a rotation.
'Q' to quit.
 ```
 <img width="1061" alt="Screen Shot 2022-10-28 at 6 14 28 AM" src="https://user-images.githubusercontent.com/76453238/198399484-fed8cb26-06de-45a3-a616-86df3408310f.png">

At this point you should have three windows open: a terminal running turtlesim_node, a terminal running turtle_teleop_key and the turtlesim window. Arrange these windows so that you can see the turtlesim window, but also have the terminal running turtle_teleop_key active so that you can control the turtle in turtlesim.

Use the arrow keys on your keyboard to control the turtle. It will move around the screen, using its attached “pen” to draw the path it followed so far.

<img width="499" alt="Screen Shot 2022-10-28 at 6 15 15 AM" src="https://user-images.githubusercontent.com/76453238/198399612-6a56f990-e236-49cd-810e-887480342f91.png">


# Use rqt

After running rqt the first time, the window will be blank. No worries; just select Plugins > Services > Service Caller from the menu bar at the top.

Use the refresh button to the left of the Service dropdown list to ensure all the services of your turtlesim node are available.

Click on the Service dropdown list to see turtlesim’s services, and select the /spawn service.

# 5.1 Try the spawn service

Let’s use rqt to call the /spawn service. You can guess from its name that /spawn will create another turtle in the turtlesim window.

Give the new turtle a unique name, like turtle2 by double-clicking between the empty single quotes in the Expression column. You can see that this expression corresponds to the name value, and is of type string.

Enter new coordinates for the turtle to spawn at, like x = 1.0 and y = 1.0.
<img width="603" alt="Screen Shot 2022-10-31 at 10 27 29 PM" src="https://user-images.githubusercontent.com/76453238/199018796-fb69256c-0445-4947-8f03-df82e6895892.png">


To spawn turtle2, you have to call the service by clicking the Call button on the upper right side of the rqt window.

You will see a new turtle (again with a random design) spawn at the coordinates you input for x and y.

If you refresh the service list in rqt, you will also see that now there are services related to the new turtle, /turtle2/…, in addition to /turtle1/….


# Try the set_pen service

Now let’s give turtle1 a unique pen using the /set_pen service:

<img width="610" alt="Screen Shot 2022-11-01 at 9 50 33 AM" src="https://user-images.githubusercontent.com/76453238/199135497-bbd1a0c2-687d-4b97-9549-6ee9d8c3003e.png">

The values for r, g and b, between 0 and 255, will set the color of the pen turtle1 draws with, and width sets the thickness of the line.

To have turtle1 draw with a distinct red line, change the value of r to 255, and the value of width to 5. Don’t forget to call the service after updating the values.

If you return to the terminal where turtle_teleop_key is running and press the arrow keys, you will see turtle1’s pen has changed.


