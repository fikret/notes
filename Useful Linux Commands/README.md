## Useful Linux commands that I always forget

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


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwOTM2MzQ2MzMsLTE0Mzk5MDM3MSwtNT
MzNzQxNzA4XX0=
-->