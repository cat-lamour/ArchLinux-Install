# Basic Install
* Acquire image
    * Check for tools: Run `./scripts/tool_check`.
    * Download and verify archiso: Run `./scripts/download_archiso`.

* Connect to "T H E  I N T E R N E T"
    * Over ethernet: `dhclient eth0`.
    * Over wifi: `iwctl station wlan0 <network_essid> connect; dhclient wlan0`.

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

* Base system
    * Pacstrap: `./scripts/install_packages`.
    * FSTab: `genfstab -U /mnt >> /mnt/etc/fstab`
    * CHRoot: `arch-chroot /mnt`.
    * Locale: `./scripts/setup_locale`.
    * Set hostname: `echo '<hostname>' > /etc/hostname`.

* UKI via Dracut
    * Dracut configs
    * Run `./scripts/make_bootable`.

* Reboot into fresh install
    * Exit the chroot.
    * `umount -R /mnt; swapoff <path_to_partition>`
    * `shutdown -r now`
