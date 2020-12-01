---
title: "QNAP Moving System from HDD to SSD"
date: 2020-11-20T15:34:30-04:00
categories:
  - tech
tags:
  - qnap
  - ssd
  - ts-473
---

# WARNINGS
- There may be issues with apps and containers/vms post migration.
- Following these steps are at your own risk.
- Basic SSH and Linux CLI would be very helpful in making this change.

Pros of moving System to SSD:
- Snappier loading times of the GUI.

Cons of moving System to SSD:
- You may need to reinstall apps, reconfigure settings, etc.


# Steps

1. Back up everything important to external storage or cloud. (I personally ran the risk and didn't do this)
2. Shut down and back up VMs from Virtualization Station to a shared folder.
3. Back up system config via Control Panel.
4. Select "Safely Detach" for any storage pools you may have. (Note: Storage pool that has System cannot be detached).
5. Shut down NAS and remove all the drives, then power it up, log into QTS and do "Reinitialize NAS" via Control Panel.
6. Once the NAS is restarted, use Qfinder Pro to set up the NAS, or find out the IP address of the NAS on your network (if you know how).
  1. I had previously reserved the DHCP for the NAS so when the NAS booted up for the first time again, it got the same IP address.
7. Format SSDs as RAID1 and let QTS use it as the system volume.
8. Log in and restore the system config from previously saved file.
9. Shut down NAS, insert all the drives and boot it back up.
10. Go to Storage & Snapshots and do "Scan and recover storage space" on the NAS. The system should recover the storage pool and volumes. (Note: if there are duplicate folders between the old volume and new, there will be warnings and errors and the new folders will have a number appended).
11. Reinstall the necessary apps. Start up Virtualization Station and recover the VMs from the backups.


# Issues encountered & Fixes
## From Step 10: Duplicate folders + Unable to access folder
This can be restored by a couple different ways. The way I chose was to fix the `SymLinks` (or shortcuts) via [CLI/SSH][Link QNAP SSH].
1. When logged into the NAS via SSH, get to the shell command line and navigate to `/share`.
2. Run `ls -la`. This will display all the folders in the directory and you will see the folders and where it links to.
3. Example:
```bash
lrwxrwxrwx  1 admin administrators   24 2020-11-30 14:16 Container -> CACHEDEV2_DATA/Container/
lrwxrwxrwx  1 admin administrators   23 2020-11-30 14:16 Download -> CACHEDEV1_DATA/Download/
```
4. If you see a folder pointing to a Storage pool (`CACHEDEV1_DATA` or `CACHEDEV2_DATA`, etc.) that doesn't have that folder, you can simply create the folder so that on the GUI it will not throw the error.
5. To make sure that you want to continue using that, copy the files from the other Storage pools to the desired storage pool and delete the old one. To do this, you'll need to find out which storage pool has the desired files and do:
  1. Make the folder: `mkdir /share/CACHEDEV<newpool#>_DATA/<newfoldername>`
  2. Copy all the files from old to new: `cp -r /share/CACHEDEV<oldpool#>_DATA/<oldfolder> /share/CACHEDEV<newpool#>_DATA/<newfoldername>`
  3. Check on GUI or CLI that the files have copied over: `ls -al /share/CACHEDEV<newpool#>_DATA/<newfoldername>`
  3. Delete all the old files `rm -rf /share/CACHEDEV<oldpool#>_DATA/<oldfolder>`

## Unable to restart Containers in Container Station
Seems like when I had imported the files, there was a missing folder or something within the container folders. To fix this, I had to:
1. Navigate to `/share/CACHEDEV2_DATA/Container/container-station-data/<mycontainerid>` (You can find the container ID from the error message when trying to start the container)
2. Make the folder `merged` (`mkdir /share/CACHEDEV2_DATA/Container/container-station-data/<mycontainerid>/merged` ).
3. Try starting the container again.





[Link QNAP SSH]: https://www.qnap.com/en/how-to/knowledge-base/article/how-to-access-qnap-nas-by-ssh/
