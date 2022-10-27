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

