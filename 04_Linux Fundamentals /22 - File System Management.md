# File System Management

## 1. What is a File System?

A **file system** is the method and data structure that an operating system uses to control how data is stored and retrieved on a storage device (like a hard drive or SSD). It's the "filing cabinet" that organizes all the data.

### Common Linux File Systems

| File System | Key Characteristics |
| :--- | :--- |
| **ext4** | **(Fourth Extended Filesystem)**. The **default** for most modern Linux distributions. It is a journaling file system, offering an excellent balance of performance, reliability, and features. |
| **Btrfs** | **(B-tree File System)**. A modern file system with advanced features like built-in snapshots, data integrity checks (checksums), and integrated volume management. |
| **XFS** | A high-performance file system that excels at handling very large files and parallel I/O operations. Often used in servers for scientific computing or media storage. |
| **NTFS** | **(New Technology File System)**. The primary file system used by Windows. Linux supports NTFS for compatibility, allowing users to read and write to drives from dual-boot systems or external Windows-formatted drives. |
| **ext2 / ext3** | Older versions of the ext filesystem. `ext3` introduced journaling, a key feature for crash recovery. Both are largely superseded by `ext4`. |

---

## 2. The Role of Inodes

The **inode (index node)** is a fundamental data structure in Unix-like file systems. Every file and directory on the system has a corresponding inode.

*   **Analogy:** An inode is like an **index card in a library's card catalog**.
*   **What it Stores (Metadata):**
    *   File permissions (owner, group, etc.)
    *   Timestamps (creation, modification, access)
    *   File size
    *   Pointers to the actual data blocks on the disk where the file's content is stored.
*   **What it DOES NOT Store:** The inode **does not** contain the filename or the file's actual data. The filename is stored in the directory's data blocks, which maps the name to an inode number.

To view the inode number of files, use the `-i` flag with `ls`.
```shell
hacker@htb[~]$ ls -li
10678872 -rw-r--r-- 1 hacker htb 234123 Feb 14 19:30 myscript.py

```
## 3. Disks, Partitions, and Mounting

### Disks and Partitions

- **Disk:** The physical storage device (e.g., /dev/sda).
    
- **Partition:** A logical division of a physical disk. A single disk can be split into multiple partitions (e.g., /dev/sda1, /dev/sda2). Each partition can be formatted with its own file system.
    
- **fdisk:** A primary command-line tool for viewing and managing disk partitions.

```shell
# List all disks and their partition tables
sudo fdisk -l
```

### Mounting

**Mounting** is the process of attaching a storage device or partition to a specific directory in the filesystem hierarchy, making its contents accessible.

- **Mount Point:** The directory where the device is attached (e.g., /mnt/usb).
    

#### Key Commands and Files

- **mount command:** Used to view currently mounted filesystems or to manually mount a new one.
```shell
# View all currently mounted filesystems
mount

# Manually mount a device to a directory
sudo mount /dev/sdb1 /mnt/usb
```

- **/etc/fstab file:** A configuration file that defines which filesystems should be **mounted automatically at boot time**.
    
- **umount command:** Used to safely detach (unmount) a filesystem. You cannot unmount a device if any file on it is currently in use.

```shell
sudo umount /mnt/usb
```

- **lsof command:** (List Open Files). Can be used to see which processes are using a file on a filesystem, which is useful for troubleshooting before unmounting.

## 4. Swap Space

**Swap space** is a portion of a hard drive that is used as virtual memory when the physical RAM (Random Access Memory) is full.

- **Purpose:**
    
    1. **Extending RAM:** The kernel moves inactive memory pages from RAM to the swap space to free up RAM for active processes.
        
    2. **Hibernation:** The entire system state can be saved to the swap space, allowing the computer to power off completely and then resume exactly where it left off.
        
- **Creation:**
    
    - mkswap: Formats a partition or file to be used as swap.
        
    - swapon: Activates the swap space for the system to use.



