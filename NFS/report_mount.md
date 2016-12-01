# Report of NFS Server Lab

* 1. NULL CALL

![nfs_1](https://github.com/jiexray/Network/blob/master/NFS/pictures/nfs_1.png)
Local asked remote server `Whether Port 111 for Portmap is available`
***

* 2. GETPORT

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/nfs_2.png)
Local asked remote `port 111`(**Portmap**), what are port numbers of services `MOUNT` and `NFS`.
And `Portmap` at remote port 111 repeat `2049` for **NFS** and `56172` for **MOUNT**
***

* 3. NULL CALL

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/nfs_3.png)
Local asked remote server `Whether Port 2049 for NFS is available`
***

* 4. MNT Call

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/nfs_4.png)
Local asked remote `port 56172`(MOUNT) `How to mount /home/jiexray/nfs`
**MOUNT** replied with *OK*, and give a file handle.

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/file_handle.png)
***

* 5. GETATTR

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/nfs_5.png)
Local asked remote for file attributes
**NFS** replied `Mode uid gid`
*NFS only use uid for security.*
***

* 6. FSINFO

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/nfs_6.png)
Local asked remote for static file system Information with its file handle(nonvolatile file system state
information and general information about the NFS version
3 protocol server implementation)
**NFS** replied `The attributes of the file system object specified in fsroot.`
***

* 7. PATHINFO

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/nfs_7.png)
Local asked remote for pathconf with file handle
**NFS** relied information below:

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/pathinfo.png)
***

* 8. FSSTAT

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/nfs_8.png)
Local ask remote for dynamic file system information with file handle(retrieves volatile file system state information)
**NFS** replied information below: t--total, f--free, a--available

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/fsstat.png)
***

* 9. ACCESS

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/nfs_9.png)
Local ask remote for check in with file handle and a `access` bitmask
**NFS** replied a `access` bitmask below:

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/access.png)


