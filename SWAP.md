## SWAP
### Swap files and partitions

Swap space in Linux is used when the amount of physical memory (RAM) is full. If the system needs more memory resources and the RAM is full, inactive pages in memory are moved to the swap space. While swap space can help machines with a small amount of RAM, it should not be considered a replacement for more RAM. Swap space is located on hard drives, which have a slower access time than physical memory. Swap space can be a dedicated swap partition (recommended), a swap file, or a combination of swap partitions and swap files. Note that Btrfs does not support swap space.

From the end-user perspective, swap files in versions 2.6.x and later of the Linux kernel are virtually as fast as swap partitions; the limitation is that swap files should be contiguously allocated on their underlying file systems. To increase performance of swap files, the kernel keeps a map of where they are placed on underlying devices and accesses them directly, thus bypassing the cache and avoiding filesystem overhead. Regardless, Red Hat recommends swap partitions to be used. When residing on HDDs, which are rotational magnetic media devices, one benefit of using swap partitions is the ability to place them on contiguous HDD areas that provide higher data throughput or faster seek time. However, the administrative flexibility of swap files can outweigh certain advantages of swap partitions. For example, a swap file can be placed on any mounted file system, can be set to any desired size, and can be added or changed as needed. Swap partitions are not as flexible; they cannot be enlarged without using partitioning or volume management tools, which introduce various complexities and potential downtimes.
### Swappiness

Swappiness is a Linux kernel parameter that controls the relative weight given to swapping out of runtime memory, as opposed to dropping pages from the system page cache, whenever a memory allocation request cannot be met from "free" memory. Swappiness can be set to values between 0 and 100 inclusive. A low value causes the kernel to prefer to evict pages from the page cache; a higher value causes the kernel to prefer to swap out "cold" memory pages. The default value is 60; setting it higher will increase overall throughput (particularly disk IO) at the risk of occasional high latency if cold pages need to be swapped back in, while setting it lower (even 0) may provide more consistently low latency. Certainly the default values work well in most workloads, but desktops and interactive systems with more than adequate RAM for any expected task may want to lower the setting while batch processing and less interactive systems may want to increase it.

Swap size configuration:

https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/ch-swapspace.html

SWAP size
<img src = "https://elearn.epam.com/assets/courseware/v1/6a05a56fcc04a86099634fa1ee21f552/asset-v1:RD_CIS+DOBCLinux+0422+type@asset+block/ram_swap.png">  

Official recommendation:

https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/ch-swapspace.html

Swap space is located on hard drives, which have a slower access time than physical memory.

Swap space can be:

- a dedicated swap partition (recommended)
- a swap file
- a combination of swap partitions and swap files

To check if swap is activated run:

$ cat /proc/swaps
$ free -h

### Adding SWAP as an LVM logical volume

To add a swap volume group 2 GB in size, assuming /dev/VolGroup00/LogVol02 is the swap volume you want to add: 

    Create the LVM2 logical volume of size 2 GB:

        $ lvcreate VolGroup00 -n LogVol02 -L 2G

    Format the new swap space:

        $ mkswap /dev/VolGroup00/LogVol02

    Add the following entry to the /etc/fstab file:
                    /dev/VolGroup00/LogVol02 swap swap defaults 0 0
    Regenerate mount units so that your system registers the new configuration:

        $ systemctl daemon-reload

    Activate swap on the logical volume:

        $ swapon -v /dev/VolGroup00/LogVol02

### Creating a swap file

    Determine the size of the new swap file in megabytes and multiply by 1024 to determine the number of blocks. For example, the block size of a 64 MB swap file is 65536.
    Create an empty file, replacing count with the value equal to the desired block size

        $ dd if=/dev/zero of=/swapfile bs=1024 count=65536

    Set up the swap file with the command:

        $ mkswap /swapfile

    Change the security of the swap file so it is not world readable.

        $ chmod 0600 /swapfile

    To enable the swap file at boot time, edit /etc/fstab as root to include the following entry:
    /swapfile swap swap defaults 0 0
    Regenerate mount units so that your system registers the new /etc/fstab configuration:

        $ systemctl daemon-reload

    To activate the swap file immediately:

        $ swapon /swapfile

    To test if the new swap file was successfully created and activated, inspect active swap space:

$ cat /proc/swaps
$ free -h

### Removing a swap file

To remove a swap file:

    At a shell prompt, execute the following command to disable the swap file (where /swapfile is the swap file):

        $ swapoff -v /swapfile

    Remove its entry from the /etc/fstab file.

        $ vi /etc/fstab

    Regenerate mount units so that your system registers the new configuration:

        $ systemctl daemon-reload

    Remove the actual file:

        $ rm /swapfile

