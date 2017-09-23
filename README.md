# Initialize LUKS File Container

### Create a container file (~16GB)
```
dd if=/dev/zero bs=1M count=16000 of=~/luks-file-container.lux
```

### Format the container with LUKS
```
sudo cryptsetup luksFormat ~/luks-file-container.lux
```
Enter Pass Phrase
Enter UPPERCASE YES

### Create virtual device under /dev/mapper
Mounts the file container as device mapper
```
sudo cryptsetup luksOpen ~/luks-file-container.lux devlux
```
Check if exists /dev/mapper/devlux


### Create file system
```
sudo mkfs.ext4 /dev/mapper/devlux
```

### Mount the Luks device to mount point
```
mkdir ~/mntlux
sudo mount /dev/mapper/devlux ~/mntlux
```

### Unmount
```
sudo umount ~/mntlux
sudo cryptsetup luksClose devlux
rmdir ~/mntlux
```

# Day to day useage
```
mkdir ~/mntlux
sudo cryptsetup luksOpen ~/luks-file-container.lux devlux
sudo mount /dev/mapper/devlux ~/mntlux
```

# TODO 
* Create open and close scripts
