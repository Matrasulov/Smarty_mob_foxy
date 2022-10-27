# Smarty_mob_foxy arm64
All the commands on this repository is for Ubun 20.05(focal fossa) foxy version. As I initialllly used the lastest humble version of ubuntu and turtleot3 has no support for humble version, I had to convert to earlier foxy version of ubuntu.


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
 
