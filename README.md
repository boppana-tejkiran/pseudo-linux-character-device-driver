# pseudo-linux-character-device-driver
This pseudo character device driver for Linux is used by me to learn 
writing charecter device drivers for Linux kernel.

This charecter device driver handles a single pseudo device.

Charecter driver accesses data from the device sequentially. i.e, byte by byte
like a stream of charecters (not as a chunk of data)
Ex: keyboard, serial port, sensors etc.

Devices are accessed as files in Unix/Linux systems. A device file gets populated
in /dev directory during kernel boot time or device hot plug events.

By using a device file, user application and driver communicate with each other.
Device files are managed as part of VFS (Virtual File Subsystem) of the Linux Kernel.
The device file creation is triggered by drivers and are created by udev.

In this project, I have written a charecter device driver that can handle
a pseudo charecter device which in our case is a memory buffer of some size.
The driver supports read(), write(), lseek() operations to the memory buffer.

Device Number = Major Number : Minor Number
dev_t is the data type provided by Linux to handle device numbers

Steps for Connection establishment between device file and the driver:
1) Create device number using - alloc_chardev_region()
2) Make char device registration with the VFS using - cdev_init() cdev_add()
3) Create device file using - class_create(), device_create()
4) Implement the driver's file operation methods for open, read, write, lseek

How to create a device number: Kernel APIs to be used in driver code to create device numbers

Creation of device file isdone in kernel initialization section.

The required header files needed for writing a charecter device driver are:
1) include/linix/fs.h
2) include/linux/cdev.h
3) include/linux/device.h
4) include/linux/uaccess.h
