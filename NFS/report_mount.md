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
***

*The scripts starting from here are taken from `NFS_test_all`*

* 10. READDIR

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/nfs_10.png)
Local ask for directory infomation use `file handle`, `cookie`, `cookieverf`, `count`

cookie: first request should be set 0, next time cookie from server. cookieverf alse.

count: The maximum size of the READDIR3resok structure(the package from server).

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/nfs_readdir_call.png)

**NFS** return dir `dir_attributes`, `cookieverf`, `reply`

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/nfs_readdir_reply.png)
***

* 11. LOOKUP

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/nfs_11.png)

Local searches a directory for a specific name and returns the file handle for the corresponding file
system object.

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/nfs_lookup_call.png)

**NFS** return `file handle`, `file attributes`, `dir attributes`

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/nfs_lookup_reply.png)
***

* 12. READ

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/nfs_12.png)

Local read data from file with `file handle`, `offset`, `count`

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/nfs_read_call.png)

Here we find the `count` is 32768, as a result, the server can only send 32768B data 
to us within a trasmit. However, we can modify this arg with command `-o rsize=524288` 
during mounting time.

**NFS** return `file attributes`, `count`(the number of bytes of data returned), `eof`, `data`

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/nfs_read_reply.png)
***

* 13. CREATE

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/nfs_13.png)

Local created a regular file with `where`, `how`, `mode`

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/nfs_create_call.png)

**NFS** reply with `file handle` of the newly created file, `obj attributes`, `dir_wcc`(this cause
modification for dir-information)

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/nfs_create_reply.png)
***

* 14. WRITE

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/nfs_14.png)

Local wrote data to a file with `file handle`,`offset`,`count`,`stable`,`data`

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/nfs_write_call.png)

**NFS** reply with `file_wcc`,`count`,`committed`,`verf`

![image](https://github.com/jiexray/Network/blob/master/NFS/pictures/nfs_write_reply.png)

In this lab, we use `async` in transmission, the `stable` and `commited` are both `unstable`.

