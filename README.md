# Docker Machine NFS

This repo is a fork of [adlogix/docker-machine-nfs](https://github.com/adlogix/docker-machine-nfs) and bringing support to Windows Subsystem for Linux

## Windows 10 with WSL

* [Install WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
* [Install VirtualBox](https://www.virtualbox.org/wiki/Downloads)
* [Setup Docker-machine for WSL](https://www.paraesthesia.com/archive/2018/09/20/docker-on-wsl-with-virtualbox-and-docker-machine/)
* [Install haneWIN NFS server](https://hanewin.net/nfs-e.htm)
* [Install `docker-machine-nfs`](#standalone)
* Tested with these attributes: `docker-machine-nfs MACHINE-NAME --shared-folder=/c/Users/ --mount-opts="rw,vers=3,tcp,nolock,noacl,async"`

## Install

```sh
curl -s https://raw.githubusercontent.com/DzeryCZ/docker-machine-nfs/master/docker-machine-nfs.sh |
  sudo tee /usr/local/bin/docker-machine-nfs > /dev/null && \
  sudo chmod +x /usr/local/bin/docker-machine-nfs
```

## Supports

* Virtualbox

## Usage

* Create `docker-machine` as usual
* Run `docker-machine-nfs`

```sh


                       ##         .
                 ## ## ##        ==               _   _ _____ ____
              ## ## ## ## ##    ===              | \ | |  ___/ ___|
          /"""""""""""""""""\___/ ===            |  \| | |_  \___ \
     ~~~ {~~ ~~~~ ~~~ ~~~~ ~~~ ~ /  ===- ~~~     | |\  |  _|  ___) |
          \______ o           __/                |_| \_|_|   |____/
            \    \         __/
             \____\_______/


Usage: $ docker-machine-nfs <machine-name> [options]

Options:

  -f, --force               Force reconfiguration of nfs
  -n, --nfs-config          NFS configuration to use in /etc/exports. (default to '-alldirs -mapall=\$(id -u):\$(id -g)')
  -s, --shared-folder,...   Folder to share (default to /Users)
  -m, --mount-opts          NFS mount options (default to 'noacl,async')

Examples:

  $ docker-machine-nfs test

    > Configure the /Users folder with NFS

  $ docker-machine-nfs test --shared-folder=/Users --shared-folder=/var/www

    > Configures the /Users and /var/www folder with NFS

  $ docker-machine-nfs test --shared-folder=/var/www --nfs-config="-alldirs -maproot=0"

    > Configure the /var/www folder with NFS and the options '-alldirs -maproot=0'

  $ docker-machine-nfs test --mount-opts="noacl,async,nolock,vers=3,udp,noatime,actimeo=1"

    > Configure the /User folder with NFS and specific mount options.

  $ docker-machine-nfs test --ip 192.168.1.12

    > docker-machine will connect to your host machine via this address

```

## Credits

* Heavily inspired by @[mattes](https://github.com/mattes) ruby version
[boot2docker-nfs.rb](https://gist.github.com/mattes/4d7f435d759ca2581347).
* Fork of @[adlogix/docker-machine-nfs](https://github.com/adlogix/docker-machine-nfs)
* @[DzeryCZ](https://github.com/DzeryCZ) added support for Windows with WSL