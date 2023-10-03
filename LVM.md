## Logical Volume Manager - LVM

**Advantages**

LVM gives you more flexibility than just using normal hard drive partitions:

- Use any number of disks as one big disk.
- Have logical volumes stretched over several disks.
- Create small logical volumes and resize them "dynamically" as they get more filled.
- Resize logical volumes regardless of their order on disk. It does not depend on the position of the LV within VG, there is no need to ensure surrounding available space.
- Resize/create/delete logical and physical volumes online. File systems on them still need to be resized, but some support online resizing.
- Online/live migration of LV being used by services to different disks without having to restart services.
- Snapshots allow you to backup a frozen copy of the file system, while keeping service downtime to a minimum.

**Disadvantages**

- Linux exclusive (almost). There is no official support in most other OS (FreeBSD, Windows..).
- Additional steps in setting up the system, more complicated.
- If you use the Btrfs file system, its Subvolume feature will also give you the benefit of having a flexible layout. In that case, using the additional Abstraction layer of LVM may be unnecessary.
<img src = "https://elearn.epam.com/assets/courseware/v1/38fa2a73eb88298d5dbbba72218304ba/asset-v1:RD_CIS+DOBCLinux+0422+type@asset+block/lvm.png">

### Overview

The following is a summary of the steps to perform to create an LVM logical volume:

- Initialize the partitions you will use for the LVM volume as physical volumes (this labels them)
- Create a volume group
- Create a logical volume

After creating the logical volume you can create and mount the file system.

### Physical volumes

pvcreate, pvdisplay, and pvscan – utilities to initialize and display physical volumes.
```bash
sudo pvcreate /dev/sdb1
```
Physical volume "/dev/sdb1" successfully created  

``` bash
sudo pvscan 
```
PV /dev/sda2 VG centos lvm2 [29.51 GiB / 0 free]  
PV /dev/sdb1 lvm2 [20.00 GiB]  
Total: 2 [49.51 GiB] / in use: 1 [29.51 GiB] / in no VG: 1 [20.00 GiB]  

```bash
 sudo pvdisplay 
```

--- Physical volume ---  
PV Name /dev/sda2  
VG Name centos  
...  

### Volume groups

**vgcreate** – create a volume group.

```bash
sudo vgcreate vg_newlvm /dev/sdb1
# create logical group from sdb1 volume.
```

```bash
sudo vgcreate vg_newlvm /dev/sdb1 /dev/sdc1 /dev/sdc2
# create logical group from multiple volumes.
```

**lvcreate** – create a logical volume inside logical group.

```bash
sudo lvcreate --name centos7_newvol -l 100%FREE vg_newlvm
# creates a logical volume called centos7_newvol that uses all of the unallocated space in the volume group vg_newlvm
```

**lvdisplay** – display a list of logical volumes.

```bash
lvdisplay 
```
--- Logical volume ---  
LV Path /dev/vg_newlvm/centos7_newvol  
LV Name centos7_newvol  
VG Name vg_newlvm  
LV UUID szlkNP-0lwe-f59Z-PJVU-X7pG-unBL-qN10D4  
LV Write Access read/write  
LV Creation host, time centos7.ehowstuff.local, 2015-01-25 15:15:48 +0800  
LV Status available # open 0 LV Size 20.00 GiB Current LE 5119  
Segments 1  
Allocation inherit  
Read ahead sectors auto  
...  

### Filesystem creation

**mkfs** – create a filesystem.

```bahs
sudo mkfs.ext4 /dev/vg_newlvm/centos7_newvol
# formats a logical volume called centos7_newvol into ext4 filesystem.
```
```bash
sudo mkfs.btrfs /dev/vg_newlvm/centos7_newvol
# formats a logical volume called centos7_newvol into btrfs filesystem. 
```
```bash
sudo mkfs.ntfs /dev/vg_newlvm/centos7_newvol
# formats a logical volume called centos7_newvol into ntfs filesystem.
```
