---
date: 26-03-2022
title: exFAT FS is bad but necessary.
tags: ['file-system']
---
### You Can't Resize An exFAT Partition

exFAT partitions cannot be resized. See [this reddit post](https://www.reddit.com/r/filesystems/comments/m9br9r/why_cant_exfat_partitions_be_resized_using/) and a bunch others around the web. That's the ugly truth about the only file system with native support across all operating systems. This is important to remember, for I learned the hard way.

I spent two days consolidating and moving my data from three existing exFAT paritions on a drive. Moving a 300GB partition to the end disk took 9 hours. All that was for the goal of copying my files to a partition at the start of the disk,** then expand it to fill the whole disk**. And now, it turns out there is not way but copying the files out of the disk and creating a new partition with an empty disk.

I wonder what file systems have and don't have support for resizing. I know that ext4 supports resizing.


## 777 everywhere
exFAT doesn't support POSIX permissions (ref: https://superuser.com/a/365756/1784432). All file permissinos default to 777, giving all permissions to all users, which may be a security risk in some situations.