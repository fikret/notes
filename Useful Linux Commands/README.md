## Useful Linux commands that I always forget

The numbers refer to the file descriptors (fd).

-   Zero is `stdin`
-   One is `stdout`
-   Two is `stderr`

`2>&1` redirects fd 2 to 1.
```
# Look for ERROR string in both stdout and stderr.
foo 2>&1 | grep ERROR
```

### How to sort directories (folders) by size    
    du -h --max-depth=1 | sort -hr

### Logs to troubleshoot system problems

    dmesg
### Show disks size

    df -H
### Show processes

    htop
### Change ownership a folder

    sudo chown -R www-data:www-data /var/www/xyz/htdocs/

### Get files name into a directory and process every item

    files=(*)
    for item in ${files[*]}; do echo "$item"; done

## SSH
**Generate SSH-Keys**
```
ssh-keygen -t ed25519
``` 
**Add SSH Public key to Remote Server**

You can use the following command to automatically add the public SSH Key to the server :

    ssh-copy-id -p 22 root@192.168.0.1
**SSH Login without password**

You should now be able to login from the server where you generated the SSH Keys to the other one without password :


    ssh -p 22 root@192.168.1.1 (Remote IP)






<!--stackedit_data:
eyJoaXN0b3J5IjpbMjAxNzI1MzczLC0xNjI4NjQwMTczLC0xOT
AwNTA1MzQxLDk4MTk0NTcxMywxOTMxMTE1ODYsLTIwOTM2MzQ2
MzMsLTE0Mzk5MDM3MSwtNTMzNzQxNzA4XX0=
-->