# Physical Access

## Physical access to machine <a id="physical-access-to-machine"></a>

So if you have physical access to a machine that is not encrypted it is really trivial to gain access to the hard-drive and all files on it.

This is how you do it

### Create linux-usb <a id="create-linux-usb"></a>

Just follow this guide for ubuntu  
[http://www.ubuntu.com/download/desktop/create-a-usb-stick-on-ubuntu](http://www.ubuntu.com/download/desktop/create-a-usb-stick-on-ubuntu)

### Boot into live-usb on victim machine <a id="boot-into-live-usb-on-victim-machine"></a>

If the machine doesn't automatically detect the usb you might have to enter into the bios. This can usually be done by pressing F12 or F1 on boot. Bios looks different from machine to machine. But you need to just choose to boot from the USB-device.

### Mount disk <a id="mount-disk"></a>

Now you have booted into the live-usb, now we need to mount the hard-drive to the usb-linux-filesystem.  
First we want to find out what partitions we have:

```text
sudo su
fdisk -l
```

This will give you a list of partitions. They will look something like this

```text
/dev/sda1
/dev/sda2
```

Identify from the list the partition you want to mount.

Here we create a space for where we want to mount the partition.

```text
mkdir /media/windows
```

```text
mount -t ntfs /dev/sda1 /media/windows
```

`-t`means type, and refers to the filesystem-type. And we choose ntfs which is the windows-filesystem.

Now you can access all the files from the harddrive in `/media/windows`

### Umount the disk <a id="umount-the-disk"></a>

Notice that is is `umount` and not unmount.

```text
umount /media/windows
```

### Quick Version <a id="quick-version"></a>

```text
F12
mkdir /mnt/windows
ntfs-3g /dev/sda1 /mnt/windows -o force
cd /mnt/windows/windows
cd /users/[*]/AppData/Roaming/Microsoft/Windows/Start Menu/Programs/Startup
cd payload.exe -> ..../Startup

location of sploit
lib/live/mount/medium/tools/payload.exe
```

### 

### Dump the hashes <a id="dump-the-hashes"></a>

[https://prakharprasad.com/windows-password-cracking-using-john-the-ripper/](https://prakharprasad.com/windows-password-cracking-using-john-the-ripper/)

#### Misc. Physical access to facilities: <a id="misc-physical-access-to-facilities"></a>

Notes:

gates

fences

cameras

guard force

doors

badge requirements

hours

barriers

night infiltration

cover infiltration

id cloning

gather info on google maps

gather info on Linkedin

site owner sites may list / show pictures of common work space

