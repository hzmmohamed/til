mount umask fstab setuid




https://linuxopsys.com/topics/linux-fstab-options
https://unix.stackexchange.com/questions/146620/difference-between-sync-and-async-mount-options
https://www.baeldung.com/linux/mount-user-rights
https://www.baeldung.com/linux/setuid-and-user-ids


> The standard form of the mount command, is `mount -t type device dir`. This tells the kernel to attach the filesystem found on device (which is of type type) at the directory dir. **The previous contents (if any) and owner and mode of dir become invisible**, and as long as this filesystem remains mounted, the pathname dir refers to the root of the filesystem on device.

`mount` to list all mounted filesystems. `mount -l` shows the labels as well.

In `fstab`, a file can be identified by:
1. Device node
2. UUID
3. Label



https://linuxopsys.com/topics/linux-fstab-options

TODO: Read the man page for `mount`