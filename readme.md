### Debos build recipies

Android9 ubuntu touch build status: [![Build Status](https://oldpc.mrcyjanek.net:443/ci/job/ubports-gsi-rootfs-builder-debos-android9/badge/icon)](https://oldpc.mrcyjanek.net:443/ci/job/ubports-gsi-rootfs-builder-debos-android9/)

This uses debos to build (sdcard) images for devices


Supported devices:
 - Pine64 using lima (can be built with mali blobs also)
    - PinePhone (dev board and final version)
    - PineTab
    - PineBook
 - Raspberry pi (all version after 3)
 - Librem 5 (dev board)
 - Generic images (for qemu, virtual box)


To build images locally, run:
```
./debos-docker -m 5G (device).yaml
```

NOTE: this uses 5G of ram, you might be able to decreases this, but may run into
space issues if you do.

You will need docker installed and working.

If this is not working...

Prerequisites
-------------

* enabled virtualization:

  - check if you have `kvm` device node:

    ```
    ls /dev/kvm
    ```

  If not, enable virtualization in BIOS and check again.

  - add your user to kvm group:

    ```
    usermod -a -G kvm <your-user-name>
    ```

   Visit [linux-kvm FAQ](https://www.linux-kvm.org/page/FAQ) for more informations.

* `binfmt_misc` module loaded on the host machine:

```
modprobe binfmt_misc
```

Pull Docker image
-----------------

```
docker pull jbbgameich/debos-docker
```

Running
-------

```
./run.sh DEBOS_PARAMETERS
```

> Visit [debos repo](https://github.com/go-debos/debos) for tool usage

For easy access from any directory:

```
ln -s $(readlink -f run.sh) ~/bin/debos-docker
debos-docker DEBOS_PARAMETERS

git clone https://gitlab.com/ubports/core/rootfs-builder-debos.git
cd rootfs-builder-debos
debos-docker -m 5G <device>.yaml
For raspberry pi this means 
debos-docker -m 5G raspberrypi.yaml
