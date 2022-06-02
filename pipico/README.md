# pipico

To be able to access a device under /dev/usb from container:

1. A udev rule is set up for giving read/write access to my user on Raspberry devices

2. in the container, use **doas**

```shell
doas picotool info
```
