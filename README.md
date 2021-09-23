# ENGICAM BSP RELEASE

To get the BSP you need to have repo installed and use it as:

Install the repo utility:

    $: mkdir ~/bin
    $: curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
    $: chmod a+x ~/bin/repo

Download the BSP source:

    $: PATH=${PATH}:~/bin
    $: mkdir -p ~/yocto/dunfell
    $: cd ~/yocto/dunfell
    $: curl https://raw.githubusercontent.com/engicam-stable/engicam-bsp-release/dunfell/Dockerfile > Dockerfile
    $: repo init -u https://github.com/engicam-stable/engicam-bsp-release.git -b dunfell-st-5.10-icore -m engicam-bsp-release.xml
    $: repo sync

| yocto-codename  |      modules       |
|:---------------:|:------------------:|
|     dunfell     |   iCore STM32MP1   |

## Install Docker Engine on Ubuntu

### Set up the repository

Update the apt package index and install packages to allow apt to use a repository over HTTPS:

    $ sudo apt-get update

    $ sudo apt-get install apt-transport-https ca-certificates \
        curl gnupg-agent software-properties-common

Add Docker’s official GPG key:

    $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

Verify that you now have the key with the fingerprint 9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88, by searching for the last 8 characters of the fingerprint.

    $ sudo apt-key fingerprint 0EBFCD88

    pub   rsa4096 2017-02-22 [SCEA]
          9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
    uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
    sub   rsa4096 2017-02-22 [S]

Use the following command to set up the stable repository:

    $ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable"

Install Docker Engine:

    $ sudo apt-get update
    $ sudo apt-get install docker-ce docker-ce-cli containerd.io

## Create a Docker Container

    $ sudo docker build -t dunfell_ubuntu_18_04 .
    $ sudo docker run -v `pwd`:`pwd` -w `pwd` -ti dunfell_ubuntu_18_04

## Set enviroment variables

Enter Yocto folder and launch the script setting enviroment variables:

	DISTRO=<distro name> MACHINE=<machine name> source layers/meta-st/scripts/envsetup.sh <build dir>

where ``<machine-name>`` corresponds to the module for which the operative system image will be compiled and ``<build-dir-name>`` is the bulding directory name chosen by the user, as in the following example:

	 DISTRO=openstlinux-weston MACHINE=stm32mp1-icore source layers/meta-st/scripts/envsetup.sh build

where a directory named ``build`` is created and enviroment variables are set to compile images for the module ``iCore STM32MP1``. Please notice that the available ``<machine-name>`` correspond to the names of the relative configuration files in ``/sources/meta-engicam-st/conf/machine``.

## Compile and flash image on sdcard

Compile the desired image with bitbake using the command (in this example we compile the recipe ``engicam-test-image.bb`` for ``iCore STM32MP1``):

	bitbake engicam-test-image

Once the image is compiled it will be possible to find in the build directory a deploy folder with the image files. The relative path to this folder from the yocto directory will be:

	tmp-glibc/deploy/images/stm32mp1-icore
