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


How to install a **custom third-party SSL certificate on WordOps** is such a topic. While you can easily find plenty of tutorials and howto’s on how to install a SSL cert on nginx, these guides don’t take into account some specifics of the WordOps stack. Here’s an update-proof way to add a 3rd party SSL certificate to WordOps:

1. Copy your signed certificate, the CA certificate bundle (which contains the root and intermediate certificates) and the private key to `/etc/ssl/yoursite.com/` and change into the directory. Obviously replace `yoursite.com` with your WordOps site.

```
cd /etc/ssl/yoursite.com/
```

2. Combine the signed cert and the CA bundle:

```
cat 234567890.crt 234567890.ca-bundle >> yoursite.crt
```

3. Create the file `/var/www/yoursite.com/conf/nginx/ssl.conf` and add the following lines:

```
listen 443 ssl http2;
listen [::]:443 ssl http2;
ssl on;
ssl_certificate        /etc/ssl/yoursite.com/yoursite.crt;
ssl_certificate_key    /etc/ssl/yoursite.com/private.key;
```

4. In order to properly redirect http traffic to https, create the file `/etc/nginx/conf.d/force-ssl-yoursite.com.conf` and add the following lines:

```
server {
    listen 80;
    server_name yoursite.com www.yoursite.com;
    return 301 https://www.yoursite.com$request_uri;
}
```

5. Apply the new configuration to nginx and you’re done:

```
service nginx reload
```

I hope this helps.  sourse: irocknow.ch

## Find Executable Files Under All Directory

    find /var/www/ -type f -executable

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTcyMzc4NTI0NiwtMTQ5ODE3NjMzMCw5Nj
U2NDY4NDUsLTEyMzA1MzI0NTksOTY1NjkwODM1LC05MjIzNjMy
MzIsMTkwOTIyNzYzLC0xNzkyMDEyOTQ0LDE4NDUxNDQyMTYsMT
I3NDM1ODA2OCwzMjg5MDA3NDcsMjAxNzI1MzczLC0xNjI4NjQw
MTczLC0xOTAwNTA1MzQxLDk4MTk0NTcxMywxOTMxMTE1ODYsLT
IwOTM2MzQ2MzMsLTE0Mzk5MDM3MSwtNTMzNzQxNzA4XX0=
-->