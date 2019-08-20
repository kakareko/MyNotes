##Copying .img file to sd card

```bash
# get list of devices and find name of your device like /dev/<DISK_IDENTIFIER>
diskutil list

# unmount the device (replace the <DISK_IDENTIFIER> with corresponding IDENTIFIER)
diskutil unmountDisk /dev/<DISK_IDENTIFIER>

# copy content of .img file to the device
sudo dd if=YOUR_IMG_FILE.img of=/dev/<DISK_IDENTIFIER> bs=1m
```

