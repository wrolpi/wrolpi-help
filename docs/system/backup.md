# Backup

## Backup from one WROLPi to another

As of the writing of this tutorial, WROLPi does not have an official way to back up a WROLPi. The current workaround
is to use rsync with a manual refresh.

Follow these steps to automate backup of your WROLPi.

1. SSH/login to the primary WROLPi, add a password for the "wrolpi" user
    - `sudo -u wrolpi passwd`
2. SSH/login into the backup WROLPi
    1. Switch to the "wrolpi" user:
        - `sudo su - wropi`
    2. Generate SSH keys for the wrolpi user:
        - `ssh-keygen`
    3. Copy ssh keys to the primary WROLPi (using the password from step 1)
        - `ssh-copy-id wrolpi@PRIMARY_IP_ADDRESS`
    4. Ensure the backup can login to the primary by ssh'ing into it from the backup
        - `ssh wrolpi@PRIMARY_IP_ADDRESS`
    5. Copy all files from the primary to the backup
        - `rsync -avrle ssh wrolpi@PRIMARY_IP_ADDRESS:/media/wrolpi/* /media/wrolpi`

Files are now synchronized, now you need to automate it. Copy/paste the following into the shell of the backup WROLPI,
it will create a bash script that will copy files from the primary to the backup WROLPi.

```shell
cat > /home/wrolpi/backup_wrolpi.sh << 'EOF'
#! /usr/bin/env bash
logfile=/home/wrolpi/wrolpi.log

echo >> ${logfile}
echo >> ${logfile}
echo start $(date +"%Y-%m-%d %H:%M:%S") >> ${logfile}
/usr/bin/rsync \
    --exclude="lost+found" \
    --exclude="tags" \
    -avue ssh \
    wrolpi@PRIMARY_IP_ADDRESS:/media/wrolpi/* \
    /media/wrolpi/ \
    2>&1 >> ${logfile}
echo end $(date +"%Y-%m-%d %H:%M:%S") >> ${logfile}

EOF
```

1. Modify the above file (at `/home/wrolpi/backup_wrolpi.sh`), replacing `PRIMARY_IP_ADDRESS` with the correct IP
   address.
2. Modify the crontab of the "wrolpi" user so this script runs daily
    - `sudo -u wrolpi crontab -e`
3. Add the following cron entry to run the backup script

```shell
0 4 * * * /bin/bash -l /home/wrolpi/backup_wrolpi.sh
```
