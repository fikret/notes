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
	w
``` 
**Add SSH Public key to Remote Server**

You can use the following command to automatically add the public SSH Key to the server :

    ssh-copy-id -p 22 root@192.168.0.1
**SSH Login without password**

You should now be able to login from the server where you generated the SSH Keys to the other one without password :


    ssh -p 22 root@192.168.1.1 (Remote IP)
## SCP
Copy files between two servers via ssh
```
scp -P 2322 file.txt root@10.10.0.2:/remote/directory
```
Copy directory between two servers via ssh
```
scp -P 2322 -r /root/directory root@10.10.0.2:/remote/directory
```

## Cron Jobs
List cron jobs
```
crontab -l
```
Edit cron jobs
```
crontab -e
```
When you create cronjobs you should use exact path for all commands also you should use exact path in cron task file example:


    19 0 * * * "/etc/letsencrypt"/acme.sh --cron --home "/etc/letsencrypt" --config-home "/etc/letsencrypt/config" > /dev/null
    15 * * * * /usr/bin/sudo /usr/bin/wordopsAutomation.sh

chmod +x wordopsAutomation.sh

## Script for bulk web site

    for i in {1..30}
    do
       wo site create --wp ku$i.sb1.wpokulu.club --user=USERNAME --pass=PASSS --email=mail@mail.com -le
    done

## rsync

    rsync -avzh --progress 'ssh -p PORTNUMBER' --ignore-existing \ root@IP:/root/FOLDER/ \ /root/FOLDER/

## How to find and kill deleted PID (if disk is full)

```
#lsof +L1

```

Which will show the list of files that holding memory with deleted quote.

Note the  **pid**  ( Process id ) of the file

Kill the process

```
#kill <pid>

```

The memory will be released by the process

Check it by command

```
#df -h
```



<!--stackedit_data:
eyJoaXN0b3J5IjpbOTY1NjQ2ODQ1LC0xMjMwNTMyNDU5LDk2NT
Y5MDgzNSwtOTIyMzYzMjMyLDE5MDkyMjc2MywtMTc5MjAxMjk0
NCwxODQ1MTQ0MjE2LDEyNzQzNTgwNjgsMzI4OTAwNzQ3LDIwMT
cyNTM3MywtMTYyODY0MDE3MywtMTkwMDUwNTM0MSw5ODE5NDU3
MTMsMTkzMTExNTg2LC0yMDkzNjM0NjMzLC0xNDM5OTAzNzEsLT
UzMzc0MTcwOF19
-->