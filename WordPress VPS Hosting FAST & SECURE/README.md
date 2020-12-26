## WordPress Server Infrastructure

Modern WordPress Server Stack

    enter code here

<pre>
                                                      Network

+-------------------------------------------------------------------------------------------------------------------+
|                                                                                                                   |
|                                                                                                                   |
|                                                                                                                   |
|                                                                                                                   |
|                   App Server                                                    DB Server                         |
|                                                                                                                   |
|        +--------------------------------+                             +------------------------------+            |
|        |                                |                             |                              |            |
|        |                                |                             |                              |            |
|        |       Nginx                    |                             |      MariaDB                 |            |
|        |                                |                             |                              |            |
|        |       PHP                      |                             |                              |            |
|        |                                |                             |                              |            |
|        |       Fail2ban                 |                             |                              |            |
|        |                                |                             |                              |            |
|        |       WP-CLI                   |                             |                              |            |
|        |                                |                             |                              |            |
|        |       Redis                    |                             |                              |            |
|        |                                |                             |                              |            |
|        |       Netdata                  |                             |                              |            |
|        |                                |                             |                              |            |
|        |       PhpMyadmin               |            DB Conn: 3306    |                              |            |
|        |                                |                             |                              |            |
|        |                                +---------------------------->+                              |            |
|        |                                |                             |                              |            |
|        |                                |                             |                              |            |
|        |                                |                             |                              |            |
|        |                                |                             |                              |            |
|        |                                |                             |                              |            |
|        |                                |                             |                              |            |
|        |                                |                             |                              |            |
|        |                                |                             |                              |            |
|        |                                |                             |                              |            |
|        |                                |                             |                              |            |
|        |                                |                             |                              |            |
|        |                                |                             |                              |            |
|        |                                |                             |                              |            |
|        |                                |                             |                              |            |
|        |                                |                             |                              |            |
|        |                                |                             |                              |            |
|        +--------------------------------+                             +------------------------------+            |
|                                                                                                                   |
|             Local IP: 10.0.0.2                                              Local IP: 10.0.0.3                    |
|                                                                                                                   |
|             Public IP: x.x.x.x                                              Public IP: x.x.x.x                    |
|                                                                                                                   |
|                                                                                                                   |
|                                                                                                                   |
|                                                                                                                   |
|                                                                                                                   |
|                                                                                                                   |
+-------------------------------------------------------------------------------------------------------------------+

</pre>


## AFTER INSTALLITION
### CRON TASKS
By default WordPress is setup to call wp-cron.php everytime someone visits your WordPress website when a scheduled task is present, to basically ask "is it time to do anything yet?".

On low traffic sites this is perfectly fine, but when your site visits start to increase, checking multiple times for scheduled tasks can be very inefficient and lead to resource usage problems for the server, this will in turn make your website load slower.

You should disable cron on wp-config.php 

    define('DISABLE_WP_CRON', 'true');
**Setup manual cron job with wp-cli**

    crontab -e
Paste:

  */10 * * * * cd /var/www/SITE-FOLDER/htdocs/; wp cron event run --due-now --allow-root
  
if you want to log cron events seperately edit this file:

    nano /etc/rsyslog.d/50-default.conf
uncomment **cron.*** line and restart the service

    sudo service rsyslog restart

### Backup

    #!/bin/sh
    zaman=$(date +%Y-%m-%d-%H%M%S)
    site=egitim_wpokulu_co
    wp_site_path=/var/www/egitim.wpokulu.co/htdocs
    site_root_path=/var/www/egitim.wpokulu.co
    backup_path=/mnt/wpkulup-backup
    
    /usr/local/bin/wp db export --allow-root --path=$wp_site_path - | gzip > $backup_path/db_$site-backup-$zaman.sql.gz 
    gdrive upload $backup_path/db_$site-backup-$zaman.sql.gz
    tar --create --gzip --absolute-names --file=$backup_path/wp_$site-backup-$zaman.tar.gz --exclude=*.tar.gz $site_root_path
    gdrive upload $backup_path/wp_$site-backup-$zaman.tar.gz 

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyODYwMjQyMjYsMTQxNzYwMTc3NywxOT
M3MzM2MzQ0LC0xMTQyODE1MzIxLC04OTU4MDA5NzJdfQ==
-->