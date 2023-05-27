# MacOs format SD Card FAT32

```shell
diskutil list
sudo diskutil eraseDisk FAT32 SDCARD MBRFormat /dev/disk2
```