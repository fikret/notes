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
uncomment cron.* line
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjA3MjEyOTE2LDE0MTc2MDE3NzcsMTkzNz
MzNjM0NCwtMTE0MjgxNTMyMSwtODk1ODAwOTcyXX0=
-->