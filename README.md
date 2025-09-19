# Домашнее задание к занятию 3 «Резервное копирование» - `Уляшев Дима`




### Задание 1


 ![alt text](https://github.com/slav1power/haproxy/blob/main/img/1r.png)

Результат резервного копирования



### Задание 2

файл crontab:

```
  GNU nano 7.2                                /tmp/crontab.SuWjAM/crontab                                         
# Edit this file to introduce tasks to be run by cron.
# 
# Each task to run has to be defined through a single line
# indicating with different fields when the task will be run
# and what command to run for the task
# 
# To define the time you can provide concrete values for
# minute (m), hour (h), day of month (dom), month (mon),
# and day of week (dow) or use '*' in these fields (for 'any').
# 
# Notice that tasks will be started based on the cron's system
# daemon's notion of time and timezones.
# 
# Output of the crontab jobs (including errors) is sent through
# email to the user the crontab file belongs to (unless redirected).
# 
# For example, you can run a backup of all your user accounts
# at 5 a.m every week with:
# 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/
# 
# For more information see the manual pages of crontab(5) and cron(8)
# 
# m h  dom mon dow   command
0 2 * * * /home/dimidrol/rsync.sh



```

файл rsync.sh

```
  #!/bin/bash

log_message() {
    logger -t "$LOG_TAG" "$1"
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1"
}

if rsync -avh --delete --checksum --exclude='.*/' --exclude='.*' . /tmp/dackup/ > /tmp/backup.log 2>&1; then
    log_message "Backup completed successfully"
    exit 0
else
    ERROR_MSG=$(tail -n 5 /tmp/backup.log)
    log_message "ERROR: Backup failed. Last error: $ERROR_MSG"
    exit 1
fi


```

![alt text](https://github.com/slav1power/haproxy/blob/main/img/2r.png)

Результат выполнения скрипта



