`lsblk` - list blocks
- List block storage devices on the system
`file -s <device name (/dev/nvme1n1)>` 
- Check the format of the block storage system
- `data` = no format

`mkfs -t <format (xfs)>` - make filesystem
- Formats the block storage device with 

`mount <device name> <mount folder>` - mount device onto folder

`blkid` - get information (including ID) of block storage devices on system

`/etc/fstab` - automatic device mounting
`UUID=<uuid> <path> <format> defaults,nofail`

`df -k` - mounted storage devices