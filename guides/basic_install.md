# Basic Install
## Preboot
* Configure UEFI if necessary
    Refer to your machine's owner's manual.

* Acquire image
    * Run `./scripts/basic/preboot <download_directory> <USB_device>`.
    * Reboot into the USB device.


## Postboot
* Connect to "T H E  I N T E R N E T"
    * Over ethernet: Should autoconnect.
    * Over wifi: `iwctl station wlan0 <network_essid> connect`.
        Iwd, as configured on the archiso image, will automatically run a DHCP client.

* Setup disks
    * Use `lsblk` and `cfdisk` to choose, define, and write partitions.
    * You'll want at least separate /efi and / partitions. If creating a swap partition, make sure it's at lease the full size of RAM and then some for good measure.
    * Create filesystems:
        * /: `mkfs.ext4 <path_to_partition>`.
        * EFI: `mkfs.vfat -F32 <path_to_partition>`.
        * swap: `mkswap <path_to_partition>`.
    * Mount filesystems:
        * /: `mount <path_to_partition> /mnt`.
        * EFI: `mount --mkdir <path_to_partition> /mnt/efi`.
        * swap: `swapon <path_to_partition>`.

* Basic system requirements
    * Run `./scripts/basic/postboot`.
    * CHRoot: `arch-chroot /mnt`.


## PostChroot
    * Run `./scripts/basic/postchroot <rootfs_partition> <hostname>`.
    * Exit the chroot.
    * Unmount the drives: `umont -R /mnt; swapoff <path_to_swap_partition>`
    * Reboot into fresh install: `shutdown -r now`
