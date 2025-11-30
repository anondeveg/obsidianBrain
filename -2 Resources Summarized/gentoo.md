2025-11-08 16:16

**Source material** : https://wiki.gentoo.org/wiki/Handbook:Main_Page

**Tags** : [[Linux]]

# gentoo Installation

- 1 the most common architictures are `x86` ,and `x86_64`(which is `amd64`) it's named x86_64 because it is compatible with x86
- `SoC` Stands for **system on a chip**

## partitioning
- it is theoretically possible to use an unpartitioned disk to host a  linux systsem, but that's rarely used IRL.

  ### partitioning technologies
	_The Handbook authors suggest using [GPT](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/Disks#GPT) whenever possible for Gentoo installations._
###  GPT
-  GPT stands for [[GUID Partition Table]]
		 - its tied with the [[UEFI]] boot sytem
		 - it has advantages on [[MBR]] like
			 - support for more than 4 primary tables
			 - It uses 64-bit logical block addressing, allowing much larger disks — up to **8 ZiB (≈9.4 ZB)** with 512-byte sectors, or **64 ZiB (≈75 ZB)** with 4 KB sectors.
		- it uses Globally Unique Identifiers (hence the G in GPT) 
		- all modern computer OSs support GPT (windows supports it only in an UEFI system (another L for windows))
		- When a system's software interface between the operating system and firmware is UEFI (instead of BIOS), GPT is almost mandatory as compatibility issues will arise with DOS disklabel.
		- GPT also takes advantage of checksumming and redundancy. It carries CRC32 checksums to detect errors in the header and partition tables and has a backup GPT at the end of the disk. This backup table can be used to recover damage of the primary GPT near the beginning of the disk.
	
#### MBR(DOS)
- MBR stands for [[Master Boot Record]]

- was first introduced in 1983

- MBR uses 32-bit identifiers for the start sector and length of the partitions, and supports three partition types: `primary`, `extended`, and `logical`.

- Primary partitions have their information stored in the master boot record itself - a very small (usually `512 bytes`) location at the very beginning of a disk. **Due to this small space, only four primary partitions are supported (for instance, /dev/sda1 to /dev/sda4)**

- In order to support more partitions, one of the primary partitions in the MBR can be marked as an _extended_ partition. This partition can then contain additional logical partitions (partitions within a partition).

- Due to using 32-bit identifiers, partition tables in the MBR cannot address storage space that is larger than 2 TiBs in size.


## **References**:

- 
- 

