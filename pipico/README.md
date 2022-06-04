# pipico

To be able to access a device under /dev/usb from container:

1. A udev rule is set up for giving read/write access to my user on Raspberry devices

```shell
% cat /etc/udev/rules.d/raspberry.rules 
# RaspberryPi Pico
SUBSYSTEM=="usb", ATTRS{idVendor}=="2e8a", ATTRS{idProduct}=="0003", OWNER="viny", MODE="0600"
```

2. In the container, use **doas**

```shell
doas picotool info
```
