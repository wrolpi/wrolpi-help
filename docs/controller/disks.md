# Disk Management

The Controller provides tools for mounting and managing external drives and storage devices.

## Supported Filesystems

The following filesystem types can be mounted:

- **ext4** - Linux native filesystem (recommended)
- **btrfs** - Linux filesystem with advanced features
- **vfat** - FAT32, compatible with Windows/Mac
- **exfat** - Extended FAT, good for large files and cross-platform use

## Viewing Disks

The disk management section shows all detected block devices and partitions:

| Column      | Description                             |
|-------------|-----------------------------------------|
| Device      | Device path (e.g., /dev/sda1)           |
| Size        | Partition size                          |
| Filesystem  | Detected filesystem type                |
| Label       | Volume label (if set)                   |
| Mount Point | Where the drive is mounted (if mounted) |

## Mounting a Drive

1. Locate the drive in the disk list
2. Click the **Mount** button
3. Optionally specify a custom mount point (must be under `/media`)
4. The drive will be mounted and accessible

### Default Mount Points

If no mount point is specified, drives are mounted under `/media` using the device name or label.

### Filesystem Permissions

For exfat and vfat filesystems, the Controller automatically sets ownership to the `wrolpi` user
so files are accessible to WROLPi services.

## Unmounting a Drive

1. Find the mounted drive in the list
2. Click the **Unmount** button
3. The drive will be safely unmounted

**Note:** A drive cannot be unmounted if files are in use. Close any applications or processes
using files on the drive before unmounting.

## Persistent Mounts

Persistent mounts survive system reboots. The Controller manages these through the system's
fstab configuration.

### Making a Mount Persistent

1. Mount the drive
2. Enable the **Persistent** toggle for the mount
3. The mount will be added to fstab and restored on reboot

### Removing a Persistent Mount

1. Disable the **Persistent** toggle
2. The fstab entry will be removed
3. The drive will not auto-mount on next boot

## Protected Mount Points

The following system mount points cannot be modified:

- `/` (root filesystem)
- `/boot`
- `/boot/firmware`

Attempting to unmount these will be blocked to protect system stability.

## Mount Point Restrictions

For security, mount points are restricted to the `/media` directory. This prevents accidentally
mounting drives over system directories.

## Docker Mode

In Docker deployments, disk mounting must be handled on the host system. The Controller can
display disk information but cannot perform mount operations from within a container.
