# Brivo Software Engineer Embedded - Interview Assignment Yocto

Project branched from https://github.com/Motesque/yocto-interview.git

## Prerequisites
* Docker Engine
* Yocto Build Host (https://www.yoctoproject.org/docs/2.5.1/brief-yoctoprojectqs/brief-yoctoprojectqs.html)
* Git
All prerequisites are already installed on a Virtual Machine provided by Brivo

The login details for that machine are transmitted separately

## Explanation
This coding exercise uses Docker, Yocto and Qemu.  These will be useful in your actual role at Brivo, especially Docker and Yocto.  The gist of the exercise is to take a trivial program which uses a non-trivial library and port it to an embedded target through yocto.

## Assignment
A colleague of yours implementd a small C++ program using the Eigen Library (http://eigen.tuxfamily.org/index.php?title=Main_Page)
For your convenience, she created a Dockerfile which compiles the program "motesque-eigen" using CMake (https://cmake.org/) 

Your task is to deploy this program on an embedded Linux Distribution based on the Yocto Project. 
Since you do not have the actual hardware, we will use the **qemu** machine target. Please use the mainline branch. 
We will provide you with SSH access to a suitable build-host.

Estimated assingment completion time: less than 2 hours, work at your own pace

## Acceptance criteria
A tarball file containing the following:
* A new yocto layer "meta-motesque-interview" which contains all necessary files
* The modified local.conf and bblayers.conf file

The image can be run at ~/yocto-interview/poky/build$ runqemu qemux86-64 nographic

The `motesque-eigen` program should be installed in `/usr/local/bin` and produce the following output:
```
Motesque Magic Eigen
  3  -1
2.5 1.5
```

## Tips:
You can  familiarize yourself with the C++ program by using Docker on your local machine:
```
~% docker build -t yocto-interview .
~% docker run --rm yocto-interview motesque-eigen
```

You will need to make changes to the source to get it working in the Yocto image. 
This is common procedure in Yocto and well documented here:
https://wiki.yoctoproject.org/wiki/TipsAndTricks/Patching_the_source_for_a_recipe

## Background
We have created a build machine with some reasonable resources.  We have provided some example command lines to get you up and running in the virtual machine prior to doing the actual exercise.

The provider user is part of the sudoer list.  This virtual machine has the following already installed:
Git
Docker Engine
Yocto Crops Container (see https://github.com/crops/poky-container)

The virtual machine also has https://github.com/HorizonDefeated/yocto-interview.git already cloned to the path /home/interview/yocto-interview

The yocto source cloned to /home/interview/yocto_crops.  This code was cloned and compiled with the following commands.
[Replicating a clean build takes about an hour, hopefully it will be much faster since the machine has already downloaded and compiled everything]
interview@ubuntu-c-32-64gib-nyc1-01:~$ cd yocto_crops/
interview@ubuntu-c-32-64gib-nyc1-01:~/yocto_crops$ docker run --rm -it -v $(pwd):$(pwd) crops/poky --workdir=$(pwd)
pokyuser@b133aec52b78:/home/interview/yocto_crops$ cd poky
pokyuser@b133aec52b78:/home/interview/yocto_crops/poky$ source oe-init-build-env
…
pokyuser@b133aec52b78:/home/interview/yocto_crops/poky/build$ bitbake core-image-minimal
…
pokyuser@b133aec52b78:/home/interview/yocto_crops/poky/build$


After building the system you can exit the docker container and run the root filesystem with qemu.


pokyuser@b133aec52b78:/home/interview/yocto_crops/poky/build$ exit
interview@ubuntu-c-32-64gib-nyc1-01:~/yocto_crops$ cd poky
interview@ubuntu-c-32-64gib-nyc1-01:~/yocto_crops/poky$ source oe-init-build-env
...
interview@ubuntu-c-32-64gib-nyc1-01:~/yocto_crops/poky/build$ runqemu qemux86-64 nographic
...
qemux86-64 login: root
root@qemux86-64:~# 
<Ctrl-A X to exit qemu>



