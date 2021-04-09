# ENGICAM BSP RELEASE

To get the BSP you need to have repo installed and use it as:

Install the repo utility:

    $: mkdir ~/bin
    $: curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
    $: chmod a+x ~/bin/repo

Download the BSP source:

    $: PATH=${PATH}:~/bin
    $: mkdir -p ~/yocto/gatesgarth
    $: cd ~/yocto/gatesgarth
    $: repo init -u https://github.com/engicam-stable/engicam-bsp-release.git -b gatesgarth-nxp -m engicam-bsp-release.xml
    $: repo sync

## Set enviroment variables

Enter Yocto folder and launch the script setting enviroment variables:

	DISTRO=<distro name> MACHINE=<machine name> source imx-setup-release.sh -b <build dir>

where ``<machine-name>`` corresponds to the module for which the operative system image will be compiled and ``<build-dir-name>`` is the bulding directory name chosen by the user, as in the following example:

	 DISTRO=eng-imx-xwayland MACHINE=imx8mp-icore source imx-setup-release.sh -b build

where a directory named ``build`` is created and enviroment variables are set to compile images for the module ``i.Core MX8M Plus``. Please notice that the available ``<machine-name>`` correspond to the names of the relative configuration files in ``/sources/meta-engicam-nxp/conf/machine``.

If the build directory already exists due to previous compilations it will be required to set the enviroment variables only executing the command:

	source setup-environment build

## Configure yocto layers

Add with bitbake the meta-engicam-nxp layer to the image layers:

	bitbake-layers add-layer ../sources/meta-engicam-nxp

## Compile and flash image on sdcard

Compile the desired image with bitbake using the command (in this example we compile the recipe ``engicam-evaluation-imagea.bb`` for ``i.Core MX8M Plus``):

	bitbake engicam-evaluation-image

Once the image is compiled it will be possible to find in the build directory a deploy folder with the image files. The relative path to this folder from the yocto directory will be:

	tmp/deploy/images/imx8mp-icore
