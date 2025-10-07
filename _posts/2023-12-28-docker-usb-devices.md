---
layout: post
title:  "Managing USB devices from a Docker container"
date:   2023-12-28 00:00:00 +0200
author: Odysseas
commentsId: 3
---


I recently had to work with a device that uses serial over USB to communicate with a Linux machine. While communicating with the device from the host machine is usually trivial, doing the same from a Docker container can be surprisingly tricky. Here are four ways to communicate with a USB device.

All examples assume a Linux host and container.

## 1. Passing a specific device

Docker allows devices to be passed to the container. However, if the device needs to be already connected when the container starts. Otherwise, Docker will throw an error and refuse to start the container.

Example 

```bash
docker run --device=/dev/ttyUSB0 ubuntu bash
```

or with Compose

```yaml
app:
    image: ubuntu
    devices:
      - "/dev/ttyUSB0:/dev/ttyUSB0"
```


## 2. Privileged container

If you want to access all available devices, regardless of when they are connected, you can use extended privileges.

Side effect is that now, the container has full root access to the host machine. In other words it can read all devices and the whole filesystem. This can be a security issue, so use proceed with caution.


Example 

```bash
docker run --privileged ubuntu bash
```

or with Compose

```yaml
app:
    image: ubuntu
    privileged: true
```


## 3. Share /dev as volume

In Linux, all devices create a file under `/dev`. Therefore it's simple to just share the whole folder. To actually access the device though, we also need to share the permission tables under `/run/udev`.

Side effect is that we are sharing all files in `/dev`. Depending on the distribution this can cause issues. Most notably the `/dev` folder of the host may contain symlinks that do not exist in the container.


Example 

```bash
docker run -v /dev:/dev -v /run/udev:/run/udev:ro ubuntu bash
```

or with Compose

```yaml
app:
    image: ubuntu
    volumes:
        - /dev:/dev
        - /run/udev:/run/udev:ro
```



## 4. Custom udev rules

If the drawbacks of the above solutions are not acceptable, there is a last, more complicated option. This involves passing a folder containing hard links to the devices. To break this down in steps:

1. Create a folder in the host machine named `/dev/dockerdevices`
2. Mount `/dev/dockerdevices` to the container as a volume
3. Create a hard link in `/dev/dockerdevices` to the USB device when it is connected to the host.

The compose file looks like this

```yaml
app:
    image: ubuntu
    volumes:
        - /dev/dockerdevices:/dev/dockerdevices
```

For the creation of the hard link, you can use udev rules in the host machine such as the following:

```
SUBSYSTEM=="tty", ATTRS{product}=="Serial Adapter", ACTION=="add" \
, RUN="/bin/bash -c '/bin/mkdir /dev/dockerdevices; /bin/ln $env{DEVNAME} /dev/dockerdevices/mydevice'"

SUBSYSTEM=="tty" ATTRS{product}=="Serial Adapter", ACTION=="remove", RUN="/bin/rm -f /dev/dockerdevices/mydevice'"
```

Of course you would have to adjust the rules above to the properties of your device.