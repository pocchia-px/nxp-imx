# ENGICAM BSP RELEASE

To get the BSP you need to have repo installed and use it as:

Install the repo utility:

    $: mkdir ~/bin
    $: curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
    $: chmod a+x ~/bin/repo

Download the BSP source:

    $: PATH=${PATH}:~/bin
    $: mkdir -p ~/yocto/${yocto-codename}
    $: cd ~/yocto/${yocto-codename}
    $: curl https://raw.githubusercontent.com/engicam-stable/engicam-bsp-release/${yocto-codename}/Dockerfile > Dockerfile
    $: repo init -u https://github.com/engicam-stable/engicam-bsp-release.git -b ${yocto-codename} -m engicam-bsp-release.xml    
    $: repo sync

| yocto-codename  |      modules       |
|:---------------:|:------------------:|
|      zeus       |  i.Core MX8M Plus  | 
|                 |  i.Core MX8M Mini  |
|                 |  i.Core MX8X       |
|     dunfell     |  MicroGEA STM32MP1 | 
