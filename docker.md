

How to shrink a growing docker VHDX file.

After trying to remove unused images, hanging images and other cleanup storage tasks space was still not freed up.

Compact the VHDX with the following

1. Shutdown docker.
2. Run disk part - 
3.   select vdisk file="C:\Users\aaa\AppData\Local\Docker\wsl\data\ext4.vhdx"
4.   detail vdisk
5.   compact vdisk

C:\ diskpart

DISKPART> select vdisk file="C:\Users\aaa\AppData\Local\Docker\wsl\data\ext4.vhdx"

DiskPart successfully selected the virtual disk file.

DISKPART> detail vdisk

Device type ID: 0 (Unknown)
Vendor ID: {00000000-0000-0000-0000-000000000000} (Unknown)
State: Added
Virtual size:  256 GB
Physical size:   88 GB
Filename: C:\Users\aaa\AppData\Local\Docker\wsl\data\ext4.vhdx
Is Child: No
Parent Filename:
Associated disk#: Not found.

DISKPART> compact vdisk

  100 percent completed

DiskPart successfully compacted the virtual disk file.

DISKPART> detail vdisk

Device type ID: 0 (Unknown)
Vendor ID: {00000000-0000-0000-0000-000000000000} (Unknown)
State: Added
Virtual size:  256 GB
Physical size:   49 GB
Filename: C:\Users\aaa\AppData\Local\Docker\wsl\data\ext4.vhdx
Is Child: No
Parent Filename:
Associated disk#: Not found.

D

